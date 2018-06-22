---
title: ASP.NET Core Identity 소개
author: rick-anderson
description: ASP.NET Core 응용 프로그램과 함께 Id를 사용 합니다. 암호 요구 사항 설정 (RequireDigit, RequiredLength, RequiredUniqueChars 등) 포함 되어 있습니다.
ms.author: riande
ms.date: 01/24/2018
uid: security/authentication/identity
ms.openlocfilehash: 57d9abbf82aedadd4d8c5eaabd21a5d31d5c6c61
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272703"
---
# <a name="introduction-to-identity-on-aspnet-core"></a><span data-ttu-id="2529d-104">ASP.NET Core Identity 소개</span><span class="sxs-lookup"><span data-stu-id="2529d-104">Introduction to Identity on ASP.NET Core</span></span>

<span data-ttu-id="2529d-105">작성자:[Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway [Erik Reitan](https://github.com/Erikre), [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="2529d-105">By [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway, [Erik Reitan](https://github.com/Erikre), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="2529d-106">ASP.NET Core Identity는 응용 프로그램에 로그인 기능을 추가할 수 있는 멤버십 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-106">ASP.NET Core Identity is a membership system which allows you to add login functionality to your application.</span></span> <span data-ttu-id="2529d-107">사용자는 계정을 생성한 다음 사용자 이름과 비밀번호를 사용해서 로그인하거나 Facebook, Google, Microsoft Account, Twitter 같은 외부 로그인 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-107">Users can create an account and login with a user name and password or they can use an external login provider such as Facebook, Google, Microsoft Account, Twitter or others.</span></span>

<span data-ttu-id="2529d-108">ASP.NET Core Identity는 SQL Server 데이터베이스에 사용자 이름, 비밀번호 및 프로필 정보를 저장하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-108">You can configure ASP.NET Core Identity to use a SQL Server database to store user names, passwords, and profile data.</span></span> <span data-ttu-id="2529d-109">또는 Azure 테이블 저장소 같은 사용자 고유의 영구 저장소를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-109">Alternatively, you can use your own persistent store, for example, an Azure Table Storage.</span></span> <span data-ttu-id="2529d-110">이 문서는 Visual Studio 및 CLI를 사용하는 경우에 대한 지침을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-110">This document contains instructions for Visual Studio and for using the CLI.</span></span>

[<span data-ttu-id="2529d-111">예제 코드 살펴보기 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="2529d-111">View or download the sample code.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) [<span data-ttu-id="2529d-112">(다운로드 방법)</span><span class="sxs-lookup"><span data-stu-id="2529d-112">(How to download)</span></span>](xref:tutorials/index#how-to-download-a-sample)

## <a name="overview-of-identity"></a><span data-ttu-id="2529d-113">Identity 개요</span><span class="sxs-lookup"><span data-stu-id="2529d-113">Overview of Identity</span></span>

<span data-ttu-id="2529d-114">본문에서는 ASP.NET Core Identity를 이용해서 사용자를 등록하고, 로그인하고, 로그아웃하는 기능을 추가하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-114">In this topic, you'll learn how to use ASP.NET Core Identity to add functionality to register, log in, and log out a user.</span></span> <span data-ttu-id="2529d-115">ASP.NET Core Identity를 이용해서 응용 프로그램을 생성하는 보다 상세한 지침은 본문의 마지막 섹션인 다음 단계 섹션을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-115">For more detailed instructions about creating apps using ASP.NET Core Identity, see the Next Steps section at the end of this article.</span></span>

1. <span data-ttu-id="2529d-116">개별 사용자 계정으로 새로운 ASP.NET Core 웹 응용 프로그램 생성하기.</span><span class="sxs-lookup"><span data-stu-id="2529d-116">Create an ASP.NET Core Web Application project with Individual User Accounts.</span></span>

   # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2529d-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2529d-117">Visual Studio</span></span>](#tab/visual-studio)

   <span data-ttu-id="2529d-118">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-118">In Visual Studio, select **File** > **New** > **Project**.</span></span> <span data-ttu-id="2529d-119">그리고 **ASP.NET Core 웹 응용 프로그램**을 선택한 다음,**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-119">Select **ASP.NET Core Web Application** and click **OK**.</span></span>

   ![새 프로젝트 대화 상자](identity/_static/01-new-project.png)

   <span data-ttu-id="2529d-121">ASP.NET Core 2.x 용 ASP.NET Core**웹 응용 프로그램 (모델-뷰-컨트롤러)** 을 선택한 다음 **인증 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-121">Select an ASP.NET Core **Web Application (Model-View-Controller)** for ASP.NET Core 2.x, then select **Change Authentication**.</span></span>

   ![새 프로젝트 대화 상자](identity/_static/02-new-project.png)

   <span data-ttu-id="2529d-123">그러면 인증 방식을 선택할 수 있는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-123">A dialog appears offering authentication choices.</span></span> <span data-ttu-id="2529d-124">**개별 사용자 계정**을 선택하고 **확인**을 클릭해서 이전 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-124">Select **Individual User Accounts** and click **OK** to return to the previous dialog.</span></span>

   ![새 프로젝트 대화 상자](identity/_static/03-new-project-auth.png)

   <span data-ttu-id="2529d-126">이렇게 **개별 사용자 계정**을 선택하면 Visual Studio에게 프로젝트 템플릿의 일부로 인증에 필요한 모델, 뷰 모델, 뷰, 컨트롤러 및 기타 자산을 생성하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-126">Selecting **Individual User Accounts** directs Visual Studio to create Models, ViewModels, Views, Controllers, and other assets required for authentication as part of the project template.</span></span>

   # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="2529d-127">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="2529d-127">.NET Core CLI</span></span>](#tab/netcore-cli)

   <span data-ttu-id="2529d-128">.NET Core CLI를 사용하는 경우, `dotnet new mvc --auth Individual` 명령으로 새로운 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-128">If using the .NET Core CLI, create the new project using `dotnet new mvc --auth Individual`.</span></span> <span data-ttu-id="2529d-129">이 명령은 Visual Studio가 생성하는 것과 동일한 Identity 템플릿 코드를 사용하는 새로운 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-129">This command creates a new project with the same Identity template code Visual Studio creates.</span></span>

   <span data-ttu-id="2529d-130">생성된 프로젝트에는 [Entity Framework Core](https://docs.microsoft.com/ef/)를 이용해서 SQL Server에 Identity 데이터와 스키마를 저장하는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 패키지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-130">The created project contains the `Microsoft.AspNetCore.Identity.EntityFrameworkCore` package, which persists the Identity data and schema to SQL Server using [Entity Framework Core](https://docs.microsoft.com/ef/).</span></span>

   ---

2. <span data-ttu-id="2529d-131">Identity 서비스를 구성하고 `Startup`에서 미들웨어 추가하기.</span><span class="sxs-lookup"><span data-stu-id="2529d-131">Configure Identity services and add middleware in `Startup`.</span></span>

   <span data-ttu-id="2529d-132">Identity 서비스는 `Startup` 클래스의 `ConfigureServices` 메서드에서 응용 프로그램에 추가됩니다:</span><span class="sxs-lookup"><span data-stu-id="2529d-132">The Identity services are added to the application in the `ConfigureServices` method in the `Startup` class:</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2529d-133">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2529d-133">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   <span data-ttu-id="2529d-134">이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-134">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="2529d-135">`Configure` 메서드에서 `UseAuthentication` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-135">Identity is enabled for the application by calling `UseAuthentication` in the `Configure` method.</span></span> <span data-ttu-id="2529d-136">`UseAuthentication`은 요청 파이프라인에 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-136">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2529d-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2529d-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]

   <span data-ttu-id="2529d-138">이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-138">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>

   <span data-ttu-id="2529d-139">`Configure` 메서드에서 `UseIdentity` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-139">Identity is enabled for the application by calling `UseIdentity` in the `Configure` method.</span></span> <span data-ttu-id="2529d-140">`UseIdentity`는 요청 파이프라인에 쿠키 기반의 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-140">`UseIdentity` adds cookie-based authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]

   ---

   <span data-ttu-id="2529d-141">응용 프로그램 시작 과정에 대한 더 자세한 내용은 [응용 프로그램 시작](xref:fundamentals/startup)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-141">For more information about the application start up process, see [Application Startup](xref:fundamentals/startup).</span></span>

3. <span data-ttu-id="2529d-142">사용자 생성.</span><span class="sxs-lookup"><span data-stu-id="2529d-142">Create a user.</span></span>

   <span data-ttu-id="2529d-143">응용 프로그램을 실행한 다음, **Register** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-143">Launch the application and then click on the **Register** link.</span></span>

   <span data-ttu-id="2529d-144">이 작업을 처음 수행하는 경우, 마이그레이션을 실행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-144">If this is the first time you're performing this action, you may be required to run migrations.</span></span> <span data-ttu-id="2529d-145">그럴 경우, **이그레이션을 수행** 하라는 메시지가 응용 프로그램에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-145">The application prompts you to **Apply Migrations**.</span></span> <span data-ttu-id="2529d-146">필요한 경우 페이지를 새로 고침합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-146">Refresh the page if needed.</span></span>

   ![마이그레이션 웹 페이지를 적용합니다.](identity/_static/apply-migrations.png)

   <span data-ttu-id="2529d-148">또는 영구적인 데이터베이스 없이 메모리 내 데이터베이스를 이용해서 응용 프로그램과 ASP.NET Core Identity를 테스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-148">Alternately, you can test using ASP.NET Core Identity with your app without a persistent database by using an in-memory database.</span></span> <span data-ttu-id="2529d-149">메모리 내 데이터베이스를 사용하려면 응용 프로그램에 `Microsoft.EntityFrameworkCore.InMemory` 패키지를 추가하고, 응용 프로그램이 `ConfigureServices`에서 `AddDbContext`를 호출하는 부분을 다음과 같이 수정합니다:</span><span class="sxs-lookup"><span data-stu-id="2529d-149">To use an in-memory database, add the `Microsoft.EntityFrameworkCore.InMemory` package to your app and modify your app's call to `AddDbContext` in `ConfigureServices` as follows:</span></span>

   ```csharp
   services.AddDbContext<ApplicationDbContext>(options =>
       options.UseInMemoryDatabase(Guid.NewGuid().ToString()));
   ```

   <span data-ttu-id="2529d-150">사용자가 **Register** 링크를 클릭하면 `AccountController` 에서 `Register` 액션이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-150">When the user clicks the **Register** link, the `Register` action is invoked on `AccountController`.</span></span> <span data-ttu-id="2529d-151">`Register` 액션은 `_userManager` 개체의 (종속성 주입으로 `AccountController`에 제공된) `CreateAsync`를 호출해서 사용자를 생성합니다:</span><span class="sxs-lookup"><span data-stu-id="2529d-151">The `Register` action creates the user by calling `CreateAsync` on the `_userManager` object (provided to `AccountController` by dependency injection):</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

   <span data-ttu-id="2529d-152">사용자가 정상적으로 생성되면 `_signInManager.SignInAsync` 가 호출되어 사용자가 즉시 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-152">If the user was created successfully, the user is logged in by the call to `_signInManager.SignInAsync`.</span></span>

   <span data-ttu-id="2529d-153">**참고:** 사용자 등록 즉시 로그인을 방지하는 방법은 [계정 확인](xref:security/authentication/accconfirm#prevent-login-at-registration) 을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-153">**Note:** See [account confirmation](xref:security/authentication/accconfirm#prevent-login-at-registration) for steps to prevent immediate login at registration.</span></span>

4. <span data-ttu-id="2529d-154">로그인</span><span class="sxs-lookup"><span data-stu-id="2529d-154">Log in.</span></span>

   <span data-ttu-id="2529d-155">사용자는 사이트 상단의 **Log in** 링크를 클릭해서 로그인할 수 있으며, 사이트에서 권한 부여가 필요한 페이지에 접근하려고 시도할 경우 Login 페이지로 이동하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-155">Users can sign in by clicking the **Log in** link at the top of the site, or they may be navigated to the Login page if they attempt to access a part of the site that requires authorization.</span></span> <span data-ttu-id="2529d-156">사용자가 Login 페이지의 양식을 제출하면 `AccountController`의 `Login` 액션이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-156">When the user submits the form on the Login page, the `AccountController` `Login` action is called.</span></span>

   <span data-ttu-id="2529d-157">`Login` 액션은 `_signInManager` 개체의 (종속성 주입으로 `AccountController` 에 제공된) `PasswordSignInAsync`를 호출합니다. </span><span class="sxs-lookup"><span data-stu-id="2529d-157">The `Login` action calls `PasswordSignInAsync` on the `_signInManager` object (provided to `AccountController` by dependency injection).</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]

   <span data-ttu-id="2529d-158">기본 `Controller` 클래스는 컨트롤러의 메서드에서 접근할 수 있는 `User` 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-158">The base `Controller` class exposes a `User` property that you can access from controller methods.</span></span> <span data-ttu-id="2529d-159">예를 들어, 열거할 수 있습니다 `User.Claims` 을 권한 부여 결정을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-159">For instance, you can enumerate `User.Claims` and make authorization decisions.</span></span> <span data-ttu-id="2529d-160">자세한 내용은 참조 [권한 부여](xref:security/authorization/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-160">For more information, see [Authorization](xref:security/authorization/index).</span></span>

5. <span data-ttu-id="2529d-161">로그아웃</span><span class="sxs-lookup"><span data-stu-id="2529d-161">Log out.</span></span>

   <span data-ttu-id="2529d-162">**LogOut** 링크를 클릭하면 `LogOut` 액션이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-162">Clicking the **Log out** link calls the `LogOut` action.</span></span>

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]

   <span data-ttu-id="2529d-163">위의 코드는 `_signInManager.SignOutAsync` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-163">The preceding code above calls the `_signInManager.SignOutAsync` method.</span></span> <span data-ttu-id="2529d-164">`SignOutAsync`메서드는 쿠키에 저장된 사용자의 클레임을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-164">The `SignOutAsync` method clears the user's claims stored in a cookie.</span></span>

<a name="pw"></a>
6. <span data-ttu-id="2529d-165">구성</span><span class="sxs-lookup"><span data-stu-id="2529d-165">Configuration.</span></span>

   <span data-ttu-id="2529d-166">Identity는 응용 프로그램의 시작 클래스에서 재지정할 수 있는 몇 가지 기본적인 동작을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-166">Identity has some default behaviors that can be overridden in the app's startup class.</span></span> <span data-ttu-id="2529d-167">기본 동작을 사용하고자 하는 경우에는 `IdentityOptions` 를 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-167">`IdentityOptions` don't need to be configured when using the default behaviors.</span></span> <span data-ttu-id="2529d-168">다음 코드는 여러 가지 암호 강도 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-168">The following code sets several password strength options:</span></span>

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="2529d-169">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="2529d-169">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

   [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="2529d-170">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="2529d-170">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

   [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=13-33)]

   ---

   <span data-ttu-id="2529d-171">Identity를 구성하는 보다 자세한 방법은 [Identity 구성하기](xref:security/authentication/identity-configuration)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-171">For more information about how to configure Identity, see [Configure Identity](xref:security/authentication/identity-configuration).</span></span>

   <span data-ttu-id="2529d-172">기본 키의 데이터 형식도 구성 가능합니다. [Identity 기본 키 데이터 형식 구성하기](xref:security/authentication/identity-primary-key-configuration)를 참고하시기 바랍니다. </span><span class="sxs-lookup"><span data-stu-id="2529d-172">You also can configure the data type of the primary key, see [Configure Identity primary keys data type](xref:security/authentication/identity-primary-key-configuration).</span></span>

7. <span data-ttu-id="2529d-173">데이터베이스 살펴보기</span><span class="sxs-lookup"><span data-stu-id="2529d-173">View the database.</span></span>

   <span data-ttu-id="2529d-174">응용 프로그램에서 SQL Server 데이터베이스를 사용할 경우 (Windows 및 Visual Studio 사용자에 대한 기본값), 응용 프로그램이 생성한 데이터베이스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-174">If your app is using a SQL Server database (the default on Windows and for Visual Studio users), you can view the database the app created.</span></span> <span data-ttu-id="2529d-175">이때 **SQL Server Management Studio** 를 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="2529d-175">You can use **SQL Server Management Studio**.</span></span> <span data-ttu-id="2529d-176">또는 Visual Studio에서 **보기**  >  **SQL Server 개체 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-176">Alternatively, from Visual Studio, select **View** > **SQL Server Object Explorer**.</span></span> <span data-ttu-id="2529d-177">그리고 **(localdb) \MSSQLLocalDB**에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-177">Connect to **(localdb)\MSSQLLocalDB**.</span></span> <span data-ttu-id="2529d-178">그러면 **aspnet-<*프로젝트명*>-<*날짜 문자열*>** 형태의 이름을 가진 데이터베이스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-178">The database with a name matching **aspnet-<*name of your project*>-<*date string*>** is displayed.</span></span>

   ![AspNetUsers 데이터베이스 테이블에 대한 컨텍스트 메뉴](identity/_static/04-db.png)

   <span data-ttu-id="2529d-180">데이터베이스와 그 **테이블** 들을 확장하고, **dbo.AspNetUsers** 테이블을 마우스 오른쪽 버튼으로 클릭한 다음, **데이터 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-180">Expand the database and its **Tables**, then right-click the **dbo.AspNetUsers** table and select **View Data**.</span></span>

8. <span data-ttu-id="2529d-181">Identity 동작 확인하기</span><span class="sxs-lookup"><span data-stu-id="2529d-181">Verify Identity works</span></span>

    <span data-ttu-id="2529d-182">기본 *ASP.NET Core 웹 응용 프로그램* 프로젝트 템플릿은 사용자가 로그인하지 않더라도 응용 프로그램의 모든 액션에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-182">The default *ASP.NET Core Web Application* project template allows users to access any action in the application without having to login.</span></span> <span data-ttu-id="2529d-183">정상적으로 ASP.NET Identity가 동작하는지 확인해보려면 `Home` 컨트롤러의 `About` 액션에 `[Authorize]` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-183">To verify that ASP.NET Identity works, add an`[Authorize]` attribute to the `About` action of the `Home` Controller.</span></span>

    ```csharp
    [Authorize]
    public IActionResult About()
    {
        ViewData["Message"] = "Your application description page.";
        return View();
    }
    ```

    # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2529d-184">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2529d-184">Visual Studio</span></span>](#tab/visual-studio)

    <span data-ttu-id="2529d-185">**Ctrl**  +  **F5** 키를 눌러서 프로젝트를 실행하고 **About** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-185">Run the project using **Ctrl** + **F5** and navigate to the **About** page.</span></span> <span data-ttu-id="2529d-186">이제 인증된 사용자만 **About** 페이지에 액세스할 수 있으므로 사용자가 로그인하거나 등록할 수 있도록 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-186">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="2529d-187">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="2529d-187">.NET Core CLI</span></span>](#tab/netcore-cli)

    <span data-ttu-id="2529d-188">명령 창을 열고 `.csproj` 파일이 위치한 프로젝트의 루트 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-188">Open a command window and navigate to the project's root directory containing the `.csproj` file.</span></span> <span data-ttu-id="2529d-189">실행의 [실행 dotnet](/dotnet/core/tools/dotnet-run) 명령을 앱을 실행 하려면:</span><span class="sxs-lookup"><span data-stu-id="2529d-189">Run the [dotnet run](/dotnet/core/tools/dotnet-run) command to run the app:</span></span>

    ```csharp
    dotnet run 
    ```

    <span data-ttu-id="2529d-190">검색의 출력에 지정 된 URL의 [dotnet 실행](/dotnet/core/tools/dotnet-run) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-190">Browse the URL specified in the output from the [dotnet run](/dotnet/core/tools/dotnet-run) command.</span></span> <span data-ttu-id="2529d-191">이 URL은 생성된 포트 번호가 지정된 `localhost`를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-191">The URL should point to `localhost` with a generated port number.</span></span> <span data-ttu-id="2529d-192">브라우저에서 **About** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-192">Navigate to the **About** page.</span></span> <span data-ttu-id="2529d-193">이제 인증된 사용자만 **About** 페이지에 액세스할 수 있으므로 사용자가 로그인하거나 등록할 수 있도록 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-193">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    ---

## <a name="identity-components"></a><span data-ttu-id="2529d-194">Identity 구성 요소</span><span class="sxs-lookup"><span data-stu-id="2529d-194">Identity Components</span></span>

<span data-ttu-id="2529d-195">Identity 시스템의 기본 참조 어셈블리는 `Microsoft.AspNetCore.Identity` 입니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-195">The primary reference assembly for the Identity system is `Microsoft.AspNetCore.Identity`.</span></span> <span data-ttu-id="2529d-196">ASP.NET Core Identity에 대한 주요 인터페이스 모음을 포함하고 있는 이 패키지는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore`에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-196">This package contains the core set of interfaces for ASP.NET Core Identity, and is included by `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span></span>

<span data-ttu-id="2529d-197">ASP.NET Core 응용 프로그램에서 Identity 시스템을 사용하려면 다음과 같은 종속성들이 필요합니다:</span><span class="sxs-lookup"><span data-stu-id="2529d-197">These dependencies are needed to use the Identity system in ASP.NET Core applications:</span></span>

* <span data-ttu-id="2529d-198">`Microsoft.AspNetCore.Identity.EntityFrameworkCore` -Entity Framework Core로 Identity를 사용하는데 필요한 형식들을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-198">`Microsoft.AspNetCore.Identity.EntityFrameworkCore` - Contains the required types to use Identity with Entity Framework Core.</span></span>

* <span data-ttu-id="2529d-199">`Microsoft.EntityFrameworkCore.SqlServer` - Entity Framework Core는 SQL Server와 같은 관계형 데이터베이스에 대한 Microsoft의 권장 데이터 액세스 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-199">`Microsoft.EntityFrameworkCore.SqlServer` - Entity Framework Core is Microsoft's recommended data access technology for relational databases like SQL Server.</span></span> <span data-ttu-id="2529d-200">테스트 목적으로 대신 `Microsoft.EntityFrameworkCore.InMemory` 를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-200">For testing, you can use `Microsoft.EntityFrameworkCore.InMemory`.</span></span>

* <span data-ttu-id="2529d-201">`Microsoft.AspNetCore.Authentication.Cookies` -응용 프로그램이 쿠키 기반의 인증을 사용할 수 있게 해주는 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-201">`Microsoft.AspNetCore.Authentication.Cookies` - Middleware that enables an app to use cookie-based authentication.</span></span>

## <a name="migrating-to-aspnet-core-identity"></a><span data-ttu-id="2529d-202">ASP.NET Identity로 마이그레이션하기</span><span class="sxs-lookup"><span data-stu-id="2529d-202">Migrating to ASP.NET Core Identity</span></span>

<span data-ttu-id="2529d-203">추가 정보 및 기존 본인 마이그레이션하는 방법에 대 한 지침을 참조 저장 [마이그레이션할 인증 및 Id](xref:migration/identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-203">For additional information and guidance on migrating your existing Identity store see [Migrate Authentication and Identity](xref:migration/identity).</span></span>

## <a name="setting-password-strength"></a><span data-ttu-id="2529d-204">암호 강도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-204">Setting password strength</span></span>

<span data-ttu-id="2529d-205">참조 [구성](#pw) 최소 암호 요구 사항을 설정 하는 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="2529d-205">See [Configuration](#pw) for a sample that sets the minimum password requirements.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2529d-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2529d-206">Next Steps</span></span>

* [<span data-ttu-id="2529d-207">인증 및 Id 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="2529d-207">Migrate Authentication and Identity</span></span>](xref:migration/identity)
* [<span data-ttu-id="2529d-208">계정 확인 및 비밀번호 복구</span><span class="sxs-lookup"><span data-stu-id="2529d-208">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="2529d-209">SMS를 이용한 2단계 인증</span><span class="sxs-lookup"><span data-stu-id="2529d-209">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="2529d-210">Facebook, Google 및 기타 외부 공급자를 이용한 인증 활성화</span><span class="sxs-lookup"><span data-stu-id="2529d-210">Facebook, Google, and external provider authentication</span></span>](xref:security/authentication/social/index)
