---
title: "ASP.NET Core Identity 소개"
author: rick-anderson
description: "ASP.NET Core 응용 프로그램과 함께 Id를 사용 합니다. 암호 요구 사항 설정 (RequireDigit, RequiredLength, RequiredUniqueChars 등) 포함 되어 있습니다."
manager: wpickett
ms.author: riande
ms.date: 01/24/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/identity
ms.openlocfilehash: a84c5f1d4cf802ee0c4116d2a02bdbfbab9aa72b
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="introduction-to-identity-on-aspnet-core"></a><span data-ttu-id="5007b-104">ASP.NET Core Identity 소개</span><span class="sxs-lookup"><span data-stu-id="5007b-104">Introduction to Identity on ASP.NET Core</span></span>

<span data-ttu-id="5007b-105">작성자:[Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway [Erik Reitan](https://github.com/Erikre), [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="5007b-105">By [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway, [Erik Reitan](https://github.com/Erikre), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="5007b-106">ASP.NET Core Identity는 응용 프로그램에 로그인 기능을 추가할 수 있는 멤버십 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-106">ASP.NET Core Identity is a membership system which allows you to add login functionality to your application.</span></span> <span data-ttu-id="5007b-107">사용자는 계정을 생성한 다음 사용자 이름과 비밀번호를 사용해서 로그인하거나 Facebook, Google, Microsoft Account, Twitter 같은 외부 로그인 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-107">Users can create an account and login with a user name and password or they can use an external login provider such as Facebook, Google, Microsoft Account, Twitter or others.</span></span>

<span data-ttu-id="5007b-108">ASP.NET Core Identity는 SQL Server 데이터베이스에 사용자 이름, 비밀번호 및 프로필 정보를 저장하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-108">You can configure ASP.NET Core Identity to use a SQL Server database to store user names, passwords, and profile data.</span></span> <span data-ttu-id="5007b-109">또는 Azure 테이블 저장소 같은 사용자 고유의 영구 저장소를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-109">Alternatively, you can use your own persistent store, for example, an Azure Table Storage.</span></span> <span data-ttu-id="5007b-110">이 문서는 Visual Studio 및 CLI를 사용하는 경우에 대한 지침을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-110">This document contains instructions for Visual Studio and for using the CLI.</span></span>

[<span data-ttu-id="5007b-111">예제 코드 살펴보기 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="5007b-111">View or download the sample code.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) [<span data-ttu-id="5007b-112">(다운로드 방법)</span><span class="sxs-lookup"><span data-stu-id="5007b-112">(How to download)</span></span>](https://docs.microsoft.com/aspnet/core/tutorials/index#how-to-download-a-sample)

## <a name="overview-of-identity"></a><span data-ttu-id="5007b-113">Identity 개요</span><span class="sxs-lookup"><span data-stu-id="5007b-113">Overview of Identity</span></span>

<span data-ttu-id="5007b-114">본문에서는 ASP.NET Core Identity를 이용해서 사용자를 등록하고, 로그인하고, 로그아웃하는 기능을 추가하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-114">In this topic, you'll learn how to use ASP.NET Core Identity to add functionality to register, log in, and log out a user.</span></span> <span data-ttu-id="5007b-115">ASP.NET Core Identity를 이용해서 응용 프로그램을 생성하는 보다 상세한 지침은 본문의 마지막 섹션인 다음 단계 섹션을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-115">For more detailed instructions about creating apps using ASP.NET Core Identity, see the Next Steps section at the end of this article.</span></span>

1.  <span data-ttu-id="5007b-116">개별 사용자 계정으로 새로운 ASP.NET Core 웹 응용 프로그램 생성하기.</span><span class="sxs-lookup"><span data-stu-id="5007b-116">Create an ASP.NET Core Web Application project with Individual User Accounts.</span></span>

    # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5007b-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5007b-117">Visual Studio</span></span>](#tab/visual-studio)

    <span data-ttu-id="5007b-118">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-118">In Visual Studio, select **File** > **New** > **Project**.</span></span> <span data-ttu-id="5007b-119">그리고 **ASP.NET Core 웹 응용 프로그램**을 선택한 다음,**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-119">Select **ASP.NET Core Web Application** and click **OK**.</span></span>

    ![새 프로젝트 대화 상자](identity/_static/01-new-project.png)

    <span data-ttu-id="5007b-121">ASP.NET Core 2.x 용 ASP.NET Core**웹 응용 프로그램 (모델-뷰-컨트롤러)**을 선택한 다음 **인증 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-121">Select an ASP.NET Core **Web Application (Model-View-Controller)** for ASP.NET Core 2.x, then select **Change Authentication**.</span></span>

    ![새 프로젝트 대화 상자](identity/_static/02-new-project.png)

    <span data-ttu-id="5007b-123">그러면 인증 방식을 선택할 수 있는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-123">A dialog appears offering authentication choices.</span></span> <span data-ttu-id="5007b-124">**개별 사용자 계정**을 선택하고 **확인**을 클릭해서 이전 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-124">Select **Individual User Accounts** and click **OK** to return to the previous dialog.</span></span>

    ![새 프로젝트 대화 상자](identity/_static/03-new-project-auth.png)

    <span data-ttu-id="5007b-126">이렇게 **개별 사용자 계정**을 선택하면 Visual Studio에게 프로젝트 템플릿의 일부로 인증에 필요한 모델, 뷰 모델, 뷰, 컨트롤러 및 기타 자산을 생성하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-126">Selecting **Individual User Accounts** directs Visual Studio to create Models, ViewModels, Views, Controllers, and other assets required for authentication as part of the project template.</span></span>

    # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="5007b-127">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="5007b-127">.NET Core CLI</span></span>](#tab/netcore-cli)

    <span data-ttu-id="5007b-128">.NET Core CLI를 사용하는 경우, ``dotnet new mvc --auth Individual`` 명령으로 새로운 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-128">If using the .NET Core CLI, create the new project using ``dotnet new mvc --auth Individual``.</span></span> <span data-ttu-id="5007b-129">이 명령은 Visual Studio가 생성하는 것과 동일한 Identity 템플릿 코드를 사용하는 새로운 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-129">This command creates a new project with the same Identity template code Visual Studio creates.</span></span>

    <span data-ttu-id="5007b-130">생성된 프로젝트에는 [Entity Framework Core](https://docs.microsoft.com/ef/)를 이용해서 SQL Server에 Identity 데이터와 스키마를 저장하는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 패키지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-130">The created project contains the `Microsoft.AspNetCore.Identity.EntityFrameworkCore` package, which persists the Identity data and schema to SQL Server using [Entity Framework Core](https://docs.microsoft.com/ef/).</span></span>

    ---

2.  <span data-ttu-id="5007b-131">Identity 서비스를 구성하고 `Startup`에서 미들웨어 추가하기.</span><span class="sxs-lookup"><span data-stu-id="5007b-131">Configure Identity services and add middleware in `Startup`.</span></span>

    <span data-ttu-id="5007b-132">Identity 서비스는 `Startup` 클래스의 `ConfigureServices` 메서드에서 응용 프로그램에 추가됩니다:</span><span class="sxs-lookup"><span data-stu-id="5007b-132">The Identity services are added to the application in the `ConfigureServices` method in the `Startup` class:</span></span>

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5007b-133">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5007b-133">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)
    
    [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]
    
    <span data-ttu-id="5007b-134">이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-134">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>
    
    <span data-ttu-id="5007b-135">`Configure` 메서드에서 `UseAuthentication` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-135">Identity is enabled for the application by calling `UseAuthentication` in the `Configure` method.</span></span> <span data-ttu-id="5007b-136">`UseAuthentication`은 요청 파이프라인에 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-136">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>
    
    [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5007b-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5007b-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)
    
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-33)]
    
    <span data-ttu-id="5007b-138">이 서비스들은 응용 프로그램에서 [종속성 주입](xref:fundamentals/dependency-injection)을 통해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-138">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>
    
    <span data-ttu-id="5007b-139">`Configure` 메서드에서 `UseIdentity` 메서드를 호출하면 응용 프로그램에서 Identity가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-139">Identity is enabled for the application by calling `UseIdentity` in the `Configure` method.</span></span> <span data-ttu-id="5007b-140">`UseIdentity`는 요청 파이프라인에 쿠키 기반의 인증 [미들웨어](xref:fundamentals/middleware/index)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-140">`UseIdentity` adds cookie-based authentication [middleware](xref:fundamentals/middleware/index) to the request pipeline.</span></span>
        
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]
    
    ---
     
    <span data-ttu-id="5007b-141">응용 프로그램 시작 과정에 대한 더 자세한 내용은 [응용 프로그램 시작](xref:fundamentals/startup)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-141">For more information about the application start up process, see [Application Startup](xref:fundamentals/startup).</span></span>

3.  <span data-ttu-id="5007b-142">사용자 생성.</span><span class="sxs-lookup"><span data-stu-id="5007b-142">Create a user.</span></span>

    <span data-ttu-id="5007b-143">응용 프로그램을 시작 하 고을 클릭는 **등록** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-143">Launch the application and then click on the **Register** link.</span></span>

    <span data-ttu-id="5007b-144">처음이이 작업을 수행 하는 경우 마이그레이션을 실행 하는 데 필요한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-144">If this is the first time you're performing this action, you may be required to run migrations.</span></span> <span data-ttu-id="5007b-145">응용 프로그램 하 라는 메시지가 표시 **적용 마이그레이션**합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-145">The application prompts you to **Apply Migrations**.</span></span> <span data-ttu-id="5007b-146">필요한 경우 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-146">Refresh the page if needed.</span></span>
    
    ![마이그레이션 웹 페이지를 적용 합니다.](identity/_static/apply-migrations.png)
    
    <span data-ttu-id="5007b-148">또는 영구 데이터베이스 없이 응용 프로그램과 함께 ASP.NET Core Id를 사용 하 여 메모리 내 데이터베이스를 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-148">Alternately, you can test using ASP.NET Core Identity with your app without a persistent database by using an in-memory database.</span></span> <span data-ttu-id="5007b-149">메모리 내 데이터베이스를 사용 하려면 추가 ``Microsoft.EntityFrameworkCore.InMemory`` 앱 패키지 및 응용 프로그램의 호출을 수정 ``AddDbContext`` 에 ``ConfigureServices`` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-149">To use an in-memory database, add the ``Microsoft.EntityFrameworkCore.InMemory`` package to your app and modify your app's call to ``AddDbContext`` in ``ConfigureServices`` as follows:</span></span>

    ```csharp
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseInMemoryDatabase(Guid.NewGuid().ToString()));
    ```
    
    <span data-ttu-id="5007b-150">사용자가 클릭할 때는 **등록** 링크는 ``Register`` 에서 동작이 호출 될 ``AccountController``합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-150">When the user clicks the **Register** link, the ``Register`` action is invoked on ``AccountController``.</span></span> <span data-ttu-id="5007b-151">``Register`` 동작 호출 하 여 사용자를 만듭니다 `CreateAsync` 에 `_userManager` 개체 (제공 된 ``AccountController`` 종속성 주입 하 여):</span><span class="sxs-lookup"><span data-stu-id="5007b-151">The ``Register`` action creates the user by calling `CreateAsync` on the `_userManager` object (provided to ``AccountController`` by dependency injection):</span></span>
 
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

    <span data-ttu-id="5007b-152">에 대 한 호출 사용자가 로그인 된 사용자가 성공적으로 만들어진 경우 ``_signInManager.SignInAsync``합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-152">If the user was created successfully, the user is logged in by the call to ``_signInManager.SignInAsync``.</span></span>

    <span data-ttu-id="5007b-153">**참고:** 참조 [계정 확인](xref:security/authentication/accconfirm#prevent-login-at-registration) 등록 시 즉시 로그인을 방지 하는 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-153">**Note:** See [account confirmation](xref:security/authentication/accconfirm#prevent-login-at-registration) for steps to prevent immediate login at registration.</span></span>
 
4.  <span data-ttu-id="5007b-154">로그인.</span><span class="sxs-lookup"><span data-stu-id="5007b-154">Log in.</span></span>
 
    <span data-ttu-id="5007b-155">사용자가 클릭 하 여 로그인 할 수는 **로그인** 사이트의 맨 위에 링크 될 수 있습니다 이동 하 게 될 로그인 페이지에 권한 부여를 요구 하는 사이트의 일부에 액세스 하려는 경우 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-155">Users can sign in by clicking the **Log in** link at the top of the site, or they may be navigated to the Login page if they attempt to access a part of the site that requires authorization.</span></span> <span data-ttu-id="5007b-156">사용자가 로그인 페이지에 폼을 제출는 ``AccountController`` ``Login`` 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-156">When the user submits the form on the Login page, the ``AccountController`` ``Login`` action is called.</span></span>

    <span data-ttu-id="5007b-157">``Login`` 동작 호출 ``PasswordSignInAsync`` 에 ``_signInManager`` 개체 (제공 된 ``AccountController`` 종속성 주입 하 여).</span><span class="sxs-lookup"><span data-stu-id="5007b-157">The ``Login`` action calls ``PasswordSignInAsync`` on the ``_signInManager`` object (provided to ``AccountController`` by dependency injection).</span></span>

    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]
 
    <span data-ttu-id="5007b-158">기본 ``Controller`` 클래스가 노출 한 ``User`` 컨트롤러 메서드에서 액세스할 수 있는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-158">The base ``Controller`` class exposes a ``User`` property that you can access from controller methods.</span></span> <span data-ttu-id="5007b-159">예를 들어, 열거할 수 있습니다 `User.Claims` 을 권한 부여 결정을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-159">For instance, you can enumerate `User.Claims` and make authorization decisions.</span></span> <span data-ttu-id="5007b-160">자세한 내용은 참조 [권한 부여](xref:security/authorization/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-160">For more information, see [Authorization](xref:security/authorization/index).</span></span>
 
5.  <span data-ttu-id="5007b-161">로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-161">Log out.</span></span>
 
    <span data-ttu-id="5007b-162">클릭 하 고 **로그 아웃** 호출 연결는 `LogOut` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-162">Clicking the **Log out** link calls the `LogOut` action.</span></span>
 
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]
 
    <span data-ttu-id="5007b-163">앞의 코드 호출 위에 `_signInManager.SignOutAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="5007b-163">The preceding code above calls the `_signInManager.SignOutAsync` method.</span></span> <span data-ttu-id="5007b-164">`SignOutAsync` 메서드 쿠키에 저장 하는 사용자의 클레임을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-164">The `SignOutAsync` method clears the user's claims stored in a cookie.</span></span>
 
<a name="pw"></a>
6.  <span data-ttu-id="5007b-165">구성입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-165">Configuration.</span></span>

    <span data-ttu-id="5007b-166">Id는 응용 프로그램의 시작 클래스에서 재정의 될 수 있는 몇 가지 기본 동작에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-166">Identity has some default behaviors that can be overridden in the app's startup class.</span></span> <span data-ttu-id="5007b-167">`IdentityOptions` 기본 동작을 사용 하는 경우 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-167">`IdentityOptions` don't need to be configured when using the default behaviors.</span></span> <span data-ttu-id="5007b-168">다음 코드는 여러 가지 암호 강도 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-168">The following code sets several password strength options:</span></span>

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5007b-169">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5007b-169">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)
    
    [!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-42)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5007b-170">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5007b-170">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)
    
    [!code-csharp[](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=13-33)]

    ---
    
    <span data-ttu-id="5007b-171">Id를 구성 하는 방법에 대 한 자세한 내용은 참조 [구성 Identity](xref:security/authentication/identity-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-171">For more information about how to configure Identity, see [Configure Identity](xref:security/authentication/identity-configuration).</span></span>
    
    <span data-ttu-id="5007b-172">기본 키의 데이터 형식을 구성할 수 참조 [Id 구성 기본 키 데이터 형식이](xref:security/authentication/identity-primary-key-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-172">You also can configure the data type of the primary key, see [Configure Identity primary keys data type](xref:security/authentication/identity-primary-key-configuration).</span></span>
 
7.  <span data-ttu-id="5007b-173">데이터베이스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-173">View the database.</span></span>

    <span data-ttu-id="5007b-174">앱 (Windows와 Visual Studio 사용자에 대 한 기본값)는 SQL Server 데이터베이스를 사용 하는 경우에 만든 응용 프로그램 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-174">If your app is using a SQL Server database (the default on Windows and for Visual Studio users), you can view the database the app created.</span></span> <span data-ttu-id="5007b-175">사용할 수 있습니다 **SQL Server Management Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-175">You can use **SQL Server Management Studio**.</span></span> <span data-ttu-id="5007b-176">또는 Visual Studio에서 선택 **보기** > **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-176">Alternatively, from Visual Studio, select **View** > **SQL Server Object Explorer**.</span></span> <span data-ttu-id="5007b-177">연결할 **(localdb) \MSSQLLocalDB**합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-177">Connect to **(localdb)\MSSQLLocalDB**.</span></span> <span data-ttu-id="5007b-178">일치 하는 이름을 사용 하 여 데이터베이스 **aspnet-<*프로젝트의 이름*>-<*날짜 문자열* >**  표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-178">The database with a name matching **aspnet-<*name of your project*>-<*date string*>** is displayed.</span></span>

    ![AspNetUsers 데이터베이스 테이블에 대 한 상황에 맞는 메뉴](identity/_static/04-db.png)
    
    <span data-ttu-id="5007b-180">데이터베이스 확장 및 해당 **테이블**를 마우스 오른쪽 단추로 클릭 한 다음는 **dbo입니다. AspNetUsers** 테이블을 선택한 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-180">Expand the database and its **Tables**, then right-click the **dbo.AspNetUsers** table and select **View Data**.</span></span>

8. <span data-ttu-id="5007b-181">Identity 작동 확인</span><span class="sxs-lookup"><span data-stu-id="5007b-181">Verify Identity works</span></span>

    <span data-ttu-id="5007b-182">기본 *ASP.NET Core 웹 응용 프로그램* 프로젝트 템플릿이 필요 없이 응용 프로그램에서 모든 작업에 액세스할 수 있도록 로그인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-182">The default *ASP.NET Core Web Application* project template allows users to access any action in the application without having to login.</span></span> <span data-ttu-id="5007b-183">ASP.NET Identity 작동 하는지 확인 하려면 추가`[Authorize]` 특성을 `About` 의 작업은 `Home` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-183">To verify that ASP.NET Identity works, add an`[Authorize]` attribute to the `About` action of the `Home` Controller.</span></span>
 
    ```cs
    [Authorize]
    public IActionResult About()
    {
        ViewData["Message"] = "Your application description page.";
        return View();
    }
    ```
    
    # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5007b-184">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5007b-184">Visual Studio</span></span>](#tab/visual-studio)

    <span data-ttu-id="5007b-185">사용 하 여 프로젝트 실행 **Ctrl** + **F5** 로 이동 하 고는 **에 대 한** 페이지.</span><span class="sxs-lookup"><span data-stu-id="5007b-185">Run the project using **Ctrl** + **F5** and navigate to the **About** page.</span></span> <span data-ttu-id="5007b-186">인증 된 사용자만 액세스할 수 있습니다는 **에 대 한** 페이지 이제 하므로 ASP.NET에 로그인 하거나 등록 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-186">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="5007b-187">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="5007b-187">.NET Core CLI</span></span>](#tab/netcore-cli)

    <span data-ttu-id="5007b-188">명령 창을 열고 프로젝트의 루트 디렉터리로 이동 포함 된 디렉터리는 `.csproj` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-188">Open a command window and navigate to the project's root directory containing the `.csproj` file.</span></span> <span data-ttu-id="5007b-189">실행의 [실행 dotnet](/dotnet/core/tools/dotnet-run) 명령을 앱을 실행 하려면:</span><span class="sxs-lookup"><span data-stu-id="5007b-189">Run the [dotnet run](/dotnet/core/tools/dotnet-run) command to run the app:</span></span>

    ```cs
    dotnet run 
    ```

    <span data-ttu-id="5007b-190">검색의 출력에 지정 된 URL의 [dotnet 실행](/dotnet/core/tools/dotnet-run) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-190">Browse the URL specified in the output from the [dotnet run](/dotnet/core/tools/dotnet-run) command.</span></span> <span data-ttu-id="5007b-191">URL 가리키는 `localhost` 생성 된 포트 번호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-191">The URL should point to `localhost` with a generated port number.</span></span> <span data-ttu-id="5007b-192">탐색 하 고 **에 대 한** 페이지.</span><span class="sxs-lookup"><span data-stu-id="5007b-192">Navigate to the **About** page.</span></span> <span data-ttu-id="5007b-193">인증 된 사용자만 액세스할 수 있습니다는 **에 대 한** 페이지 이제 하므로 ASP.NET에 로그인 하거나 등록 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-193">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    ---

## <a name="identity-components"></a><span data-ttu-id="5007b-194">Identity 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5007b-194">Identity Components</span></span>

<span data-ttu-id="5007b-195">Id 시스템에 대 한 기본 참조 어셈블리는 `Microsoft.AspNetCore.Identity`합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-195">The primary reference assembly for the Identity system is `Microsoft.AspNetCore.Identity`.</span></span> <span data-ttu-id="5007b-196">이 패키지 ASP.NET Core Id에 대 한 인터페이스의 핵심 집합으로 포함 되어 있으며 `Microsoft.AspNetCore.Identity.EntityFrameworkCore`합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-196">This package contains the core set of interfaces for ASP.NET Core Identity, and is included by `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span></span>

<span data-ttu-id="5007b-197">이러한 종속성 ASP.NET Core 응용 프로그램의 Id 시스템을 사용 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-197">These dependencies are needed to use the Identity system in ASP.NET Core applications:</span></span>

* <span data-ttu-id="5007b-198">`Microsoft.AspNetCore.Identity.EntityFrameworkCore` -Identity Entity Framework Core 사용 시 필요한 형식을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-198">`Microsoft.AspNetCore.Identity.EntityFrameworkCore` - Contains the required types to use Identity with Entity Framework Core.</span></span>

* <span data-ttu-id="5007b-199">`Microsoft.EntityFrameworkCore.SqlServer` -Entity Framework Core는 SQL Server와 같은 관계형 데이터베이스에 대 한 Microsoft의 권장 되는 데이터 액세스 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-199">`Microsoft.EntityFrameworkCore.SqlServer` - Entity Framework Core is Microsoft's recommended data access technology for relational databases like SQL Server.</span></span> <span data-ttu-id="5007b-200">테스트를 위해 사용할 수 있습니다 `Microsoft.EntityFrameworkCore.InMemory`합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-200">For testing, you can use `Microsoft.EntityFrameworkCore.InMemory`.</span></span>

* <span data-ttu-id="5007b-201">`Microsoft.AspNetCore.Authentication.Cookies` -앱이 쿠키 기반 인증을 사용할 수 있도록 하는 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-201">`Microsoft.AspNetCore.Authentication.Cookies` - Middleware that enables an app to use cookie-based authentication.</span></span>

## <a name="migrating-to-aspnet-core-identity"></a><span data-ttu-id="5007b-202">ASP.NET Core Id로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5007b-202">Migrating to ASP.NET Core Identity</span></span>

<span data-ttu-id="5007b-203">추가 정보 및 기존 본인 마이그레이션하는 방법에 대 한 지침을 참조 저장 [마이그레이션 인증 및 Id](xref:migration/identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-203">For additional information and guidance on migrating your existing Identity store see [Migrating Authentication and Identity](xref:migration/identity).</span></span>

## <a name="setting-password-strength"></a><span data-ttu-id="5007b-204">암호 강도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-204">Setting password strength</span></span>

<span data-ttu-id="5007b-205">참조 [구성](#pw) 최소 암호 요구 사항을 설정 하는 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="5007b-205">See [Configuration](#pw) for a sample that sets the minimum password requirements.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5007b-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5007b-206">Next Steps</span></span>

* [<span data-ttu-id="5007b-207">인증 및 ID 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5007b-207">Migrating Authentication and Identity</span></span>](xref:migration/identity)
* [<span data-ttu-id="5007b-208">계정 확인 및 암호 복구</span><span class="sxs-lookup"><span data-stu-id="5007b-208">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="5007b-209">SMS를 사용한 2단계 인증</span><span class="sxs-lookup"><span data-stu-id="5007b-209">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="5007b-210">Facebook, Google, 및 외부 공급자 인증</span><span class="sxs-lookup"><span data-stu-id="5007b-210">Facebook, Google, and external provider authentication</span></span>](xref:security/authentication/social/index)
