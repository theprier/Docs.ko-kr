---
title: 계정 확인 및 ASP.NET Core에서 암호 복구
author: rick-anderson
description: 전자 메일 확인 및 암호 재설정을 사용 하 여 ASP.NET Core 앱을 빌드하는 방법에 알아봅니다.
ms.author: riande
ms.date: 7/11/2018
uid: security/authentication/accconfirm
ms.openlocfilehash: af3ba8b27148d94c4a905c688b8165f49b9f2927
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095748"
---
::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="79490-103">참조 [이 PDF 파일](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core 1.1 및 2.1 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-103">See [this PDF file](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core 1.1 and 2.1 version.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

# <a name="account-confirmation-and-password-recovery-in-aspnet-core"></a><span data-ttu-id="79490-104">계정 확인 및 ASP.NET Core에서 암호 복구</span><span class="sxs-lookup"><span data-stu-id="79490-104">Account confirmation and password recovery in ASP.NET Core</span></span>

<span data-ttu-id="79490-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="79490-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

<span data-ttu-id="79490-106">이 자습서에서는 전자 메일 확인 및 암호 재설정을 사용 하 여 ASP.NET Core 앱을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="79490-106">This tutorial shows how to build an ASP.NET Core app with email confirmation and password reset.</span></span> <span data-ttu-id="79490-107">이 자습서는 **되지** 시작 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-107">This tutorial is **not** a beginning topic.</span></span> <span data-ttu-id="79490-108">에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-108">You should be familiar with:</span></span>

* [<span data-ttu-id="79490-109">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="79490-109">ASP.NET Core</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="79490-110">인증</span><span class="sxs-lookup"><span data-stu-id="79490-110">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="79490-111">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="79490-111">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

<!-- see C:/Dropbox/wrk/Code/SendGridConsole/Program.cs -->

## <a name="prerequisites"></a><span data-ttu-id="79490-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="79490-112">Prerequisites</span></span>

<span data-ttu-id="79490-113">[!INCLUDE](~/includes/2.1-SDK.md) [](~/includes/2.1-SDK.md)]</span><span class="sxs-lookup"><span data-stu-id="79490-113">[!INCLUDE [](~/includes/2.1-SDK.md) [](~/includes/2.1-SDK.md)]</span></span>

## <a name="create-a-web--app-and-scaffold-identity"></a><span data-ttu-id="79490-114">웹 앱 만들기 및 Identity를 스 캐 폴드</span><span class="sxs-lookup"><span data-stu-id="79490-114">Create a web  app and scaffold Identity</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="79490-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79490-115">Visual Studio</span></span>](#tab/visual-studio) 

* <span data-ttu-id="79490-116">Visual Studio에서 만드는 새 **웹 응용 프로그램** 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-116">In Visual Studio, create a new **Web Application** project.</span></span>
* <span data-ttu-id="79490-117">선택 **ASP.NET Core 2.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-117">Select **ASP.NET Core 2.1**.</span></span>
* <span data-ttu-id="79490-118">기본값을 유지 **Authentication** 로 설정 **인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-118">Keep the default **Authentication** set to **No Authentication**.</span></span> <span data-ttu-id="79490-119">다음 단계에 인증 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-119">Authentication is added in the next step.</span></span>

<span data-ttu-id="79490-120">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="79490-120">In the next step:</span></span>

* <span data-ttu-id="79490-121">레이아웃 페이지로 *~/Pages/Shared/_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="79490-121">Set the layout page to *~/Pages/Shared/_Layout.cshtml*</span></span>
* <span data-ttu-id="79490-122">선택 *계정/등록*</span><span class="sxs-lookup"><span data-stu-id="79490-122">Select *Account/Register*</span></span>
* <span data-ttu-id="79490-123">새 **데이터 컨텍스트 클래스**</span><span class="sxs-lookup"><span data-stu-id="79490-123">Create a new **Data context class**</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="79490-124">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="79490-124">.NET Core CLI</span></span>](#tab/netcore-cli)

```console
dotnet new webapp -o WebPWrecover
cd WebPWrecover
dotnet tool install -g dotnet-aspnet-codegenerator
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet aspnet-codegenerator identity -fi Account.Register -dc WebPWrecover.Models.WebPWrecoverContext
dotnet ef migrations add CreateIdentitySchema
dotnet ef database drop -f
dotnet ef database update
dotnet build
```

<span data-ttu-id="79490-125">실행 `dotnet aspnet-codegenerator identity --help` 스 캐 폴딩 도구 도움말을 보려면.</span><span class="sxs-lookup"><span data-stu-id="79490-125">Run `dotnet aspnet-codegenerator identity --help` to get help on the scaffolding tool.</span></span>

------

<span data-ttu-id="79490-126">지침을 따릅니다 [인증을 사용](xref:security/authentication/scaffold-identity#useauthentication):</span><span class="sxs-lookup"><span data-stu-id="79490-126">Follow the instructions in [Enable authentication](xref:security/authentication/scaffold-identity#useauthentication):</span></span>

* <span data-ttu-id="79490-127">추가 `app.UseAuthentication();` 를 `Startup.Configure`</span><span class="sxs-lookup"><span data-stu-id="79490-127">Add `app.UseAuthentication();` to `Startup.Configure`</span></span>
* <span data-ttu-id="79490-128">추가 `<partial name="_LoginPartial" />` 레이아웃 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-128">Add `<partial name="_LoginPartial" />` to the layout file.</span></span>

## <a name="test-new-user-registration"></a><span data-ttu-id="79490-129">새 사용자 등록 테스트</span><span class="sxs-lookup"><span data-stu-id="79490-129">Test new user registration</span></span>

<span data-ttu-id="79490-130">앱 실행을 선택 합니다 **등록** 링크를 선택한 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-130">Run the app, select the **Register** link, and register a user.</span></span> <span data-ttu-id="79490-131">이 시점에서 전자 메일에만 유효성 검사 된 합니다 [[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-131">At this point, the only validation on the email is with the [[EmailAddress]](/dotnet/api/system.componentmodel.dataannotations.emailaddressattribute) attribute.</span></span> <span data-ttu-id="79490-132">등록을 제출 후 앱에 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-132">After submitting the registration, you are logged into the app.</span></span> <span data-ttu-id="79490-133">자습서의 뒷부분에 나오는 코드에는 전자 메일의 유효성을 검사할 때까지 새 사용자가 로그인 할 수 없습니다 있도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-133">Later in the tutorial, the code is updated so new users can't log in until their email is validated.</span></span>

## <a name="view-the-identity-database"></a><span data-ttu-id="79490-134">Id 데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="79490-134">View the Identity database</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="79490-135">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79490-135">Visual Studio</span></span>](#tab/visual-studio) 

* <span data-ttu-id="79490-136">**뷰** 메뉴에서 **SQL Server 개체 탐색기** (SSOX).</span><span class="sxs-lookup"><span data-stu-id="79490-136">From the **View** menu, select **SQL Server Object Explorer** (SSOX).</span></span>
* <span data-ttu-id="79490-137">이동할 **(localdb) (SQL Server 13) MSSQLLocalDB**합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-137">Navigate to **(localdb)MSSQLLocalDB(SQL Server 13)**.</span></span> <span data-ttu-id="79490-138">마우스 오른쪽 단추로 클릭 **dbo입니다. AspNetUsers** > **데이터를 볼**:</span><span class="sxs-lookup"><span data-stu-id="79490-138">Right-click on **dbo.AspNetUsers** > **View Data**:</span></span>

![SQL Server 개체 탐색기에서 AspNetUsers 테이블의 상황에 맞는 메뉴](accconfirm/_static/ssox.png)

<span data-ttu-id="79490-140">테이블의 유의 `EmailConfirmed` 필드는 `False`합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-140">Note the table's `EmailConfirmed` field is `False`.</span></span>

<span data-ttu-id="79490-141">앱에서 확인 전자 메일을 보낼 때 다음 단계에서는이 전자 메일에 다시 사용 하려는.</span><span class="sxs-lookup"><span data-stu-id="79490-141">You might want to use this email again in the next step when the app sends a confirmation email.</span></span> <span data-ttu-id="79490-142">선택한 행을 마우스 오른쪽 단추로 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-142">Right-click on the row and select **Delete**.</span></span> <span data-ttu-id="79490-143">전자 메일 별칭을 삭제 하면 쉽게 다음 단계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-143">Deleting the email alias makes it easier in the following steps.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="79490-144">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="79490-144">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="79490-145">참조 [ASP.NET Core MVC 프로젝트에서 SQLite 작업](xref:tutorials/first-mvc-app-xplat/working-with-sql) SQLite 데이터베이스를 보는 방법에 대 한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-145">See [Work with SQLite in an ASP.NET Core MVC project](xref:tutorials/first-mvc-app-xplat/working-with-sql) for instructions on how to view the SQLite database.</span></span>

------

<a name="prevent-login-at-registration"></a>
## <a name="require-email-confirmation"></a><span data-ttu-id="79490-146">전자 메일 확인이 필요</span><span class="sxs-lookup"><span data-stu-id="79490-146">Require email confirmation</span></span>

<span data-ttu-id="79490-147">새 사용자 등록 전자 메일을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-147">It's a best practice to confirm the email of a new user registration.</span></span> <span data-ttu-id="79490-148">다른 사람이 가장 하지는 확인 하려면 확인 하면 전자 메일 (즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않은).</span><span class="sxs-lookup"><span data-stu-id="79490-148">Email confirmation helps to verify they're not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="79490-149">토론 포럼을 했으며 방지 하려고 한다고 가정해 보겠습니다 "yli@example.com"등록"에서nolivetto@contoso.com"입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-149">Suppose you had a discussion forum, and you wanted to prevent "yli@example.com" from registering as "nolivetto@contoso.com".</span></span> <span data-ttu-id="79490-150">전자 메일 확인 하지 않고 "nolivetto@contoso.com" 앱에서 원치 않는 전자 메일을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-150">Without email confirmation, "nolivetto@contoso.com" could receive unwanted email from your app.</span></span> <span data-ttu-id="79490-151">사용자는 실수로로 등록 되어 있다고 가정 "ylo@example.com" 및 "yli"의 오타 눈치채 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-151">Suppose the user accidentally registered as "ylo@example.com" and hadn't noticed the misspelling of "yli".</span></span> <span data-ttu-id="79490-152">이러한 앱에 올바른 전자 메일 없기 때문에 암호 복구를 사용 하려면 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-152">They wouldn't be able to use password recovery because the app doesn't have their correct email.</span></span> <span data-ttu-id="79490-153">전자 메일 확인 봇을에서 제한 된 보호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-153">Email confirmation provides limited protection from bots.</span></span> <span data-ttu-id="79490-154">전자 메일 확인 전자 메일 계정의 수를 사용 하 여 악의적인 사용자 로부터 보호를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-154">Email confirmation doesn't provide protection from malicious users with many email accounts.</span></span>

<span data-ttu-id="79490-155">일반적으로 새 사용자가 전자 메일을 확인된 하기 전에 먼저 웹 사이트에 데이터를 게시 하지 못하도록 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-155">You generally want to prevent new users from posting any data to your web site before they have a confirmed email.</span></span>

<span data-ttu-id="79490-156">업데이트 *Areas/Identity/IdentityHostingStartup.cs* 전자 메일을 확인된 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-156">Update *Areas/Identity/IdentityHostingStartup.cs*  to require a confirmed email:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Areas/Identity/IdentityHostingStartup.cs?name=snippet1&highlight=10-13)]

<span data-ttu-id="79490-157">`config.SignIn.RequireConfirmedEmail = true;` 등록 된 사용자를가 해당 전자 메일이 확인 될 때까지 로그인 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-157">`config.SignIn.RequireConfirmedEmail = true;` prevents registered users from logging in until their email is confirmed.</span></span>

### <a name="configure-email-provider"></a><span data-ttu-id="79490-158">전자 메일 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="79490-158">Configure email provider</span></span>

<span data-ttu-id="79490-159">이 자습서에서는 [SendGrid](https://sendgrid.com) 전자 메일을 보내는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-159">In this tutorial, [SendGrid](https://sendgrid.com) is used to send email.</span></span> <span data-ttu-id="79490-160">SendGrid 계정 및 전자 메일을 보내는 키 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-160">You need a SendGrid account and key to send email.</span></span> <span data-ttu-id="79490-161">다른 이메일 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-161">You can use other email providers.</span></span> <span data-ttu-id="79490-162">ASP.NET Core 2.x 포함 `System.Net.Mail`, 앱에서 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-162">ASP.NET Core 2.x includes `System.Net.Mail`, which allows you to send email from your app.</span></span> <span data-ttu-id="79490-163">전자 메일을 보내려면 SendGrid 또는 다른 전자 메일 서비스를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-163">We recommend you use SendGrid or another email service to send email.</span></span> <span data-ttu-id="79490-164">SMTP를 보호 하 고 올바르게 설정 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-164">SMTP is difficult to secure and set up correctly.</span></span>

<span data-ttu-id="79490-165">합니다 [옵션 패턴](xref:fundamentals/configuration/options) 사용자 계정 및 키 설정에 액세스 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-165">The [Options pattern](xref:fundamentals/configuration/options) is used to access the user account and key settings.</span></span> <span data-ttu-id="79490-166">자세한 내용은 [구성](xref:fundamentals/configuration/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-166">For more information, see [configuration](xref:fundamentals/configuration/index).</span></span>

<span data-ttu-id="79490-167">전자 메일 보안 키를 인출 하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79490-167">Create a class to fetch the secure email key.</span></span> <span data-ttu-id="79490-168">이 샘플을 만들 *Services/AuthMessageSenderOptions.cs*:</span><span class="sxs-lookup"><span data-stu-id="79490-168">For this sample, create *Services/AuthMessageSenderOptions.cs*:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Services/AuthMessageSenderOptions.cs?name=snippet1)]

#### <a name="configure-sendgrid-user-secrets"></a><span data-ttu-id="79490-169">SendGrid 사용자 암호를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-169">Configure SendGrid user secrets</span></span>

<span data-ttu-id="79490-170">고유한 추가 `<UserSecretsId>` 값을 `<PropertyGroup>` 프로젝트 파일의 요소:</span><span class="sxs-lookup"><span data-stu-id="79490-170">Add a unique `<UserSecretsId>` value to the `<PropertyGroup>` element of the project file:</span></span>

[!code-xml[](accconfirm/sample/WebPWrecover21/WebPWrecover.csproj?highlight=5)]

<span data-ttu-id="79490-171">설정 합니다 `SendGridUser` 하 고 `SendGridKey` 사용 하 여는 [암호 관리자 도구](xref:security/app-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-171">Set the `SendGridUser` and `SendGridKey` with the [secret-manager tool](xref:security/app-secrets).</span></span> <span data-ttu-id="79490-172">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="79490-172">For example:</span></span>

```console
C:/WebAppl>dotnet user-secrets set SendGridUser RickAndMSFT
info: Successfully saved SendGridUser = RickAndMSFT to the secret store.
```

<span data-ttu-id="79490-173">Windows, 암호 관리자의 키/값 쌍 저장 하는 *secrets.json* 파일을 `%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-173">On Windows, Secret Manager stores keys/value pairs in a *secrets.json* file in the `%APPDATA%/Microsoft/UserSecrets/<WebAppName-userSecretsId>` directory.</span></span>

<span data-ttu-id="79490-174">콘텐츠를 *secrets.json* 파일 암호화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-174">The contents of the *secrets.json* file aren't encrypted.</span></span> <span data-ttu-id="79490-175">합니다 *secrets.json* 파일은 다음과 같습니다 (의 `SendGridKey` 값이 제거 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="79490-175">The *secrets.json* file is shown below (the `SendGridKey` value has been removed.)</span></span>

 ```json
  {
    "SendGridUser": "RickAndMSFT",
    "SendGridKey": "<key removed>"
  }
  ```

### <a name="install-sendgrid"></a><span data-ttu-id="79490-176">SendGrid를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-176">Install SendGrid</span></span>

<span data-ttu-id="79490-177">이 자습서를 통해 전자 메일 알림을 추가 하는 방법을 보여 줍니다 [SendGrid](https://sendgrid.com/), 하지만 SMTP 및 다른 메커니즘을 사용 하 여 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-177">This tutorial shows how to add email notifications through [SendGrid](https://sendgrid.com/), but you can send email using SMTP and other mechanisms.</span></span>

<span data-ttu-id="79490-178">설치는 `SendGrid` NuGet 패키지:</span><span class="sxs-lookup"><span data-stu-id="79490-178">Install the `SendGrid` NuGet package:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="79490-179">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79490-179">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="79490-180">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-180">From the Package Manager Console, enter the following command:</span></span>

``` PMC
Install-Package SendGrid
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="79490-181">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="79490-181">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="79490-182">콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-182">From the console, enter the following command:</span></span>

```cli
dotnet add package SendGrid
```

------

<span data-ttu-id="79490-183">참조 [SendGrid를 사용 하 여 시작 해 보세요](https://sendgrid.com/free/) 무료 SendGrid 계정을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-183">See [Get Started with SendGrid for Free](https://sendgrid.com/free/) to register for a free SendGrid account.</span></span>
### <a name="implement-iemailsender"></a><span data-ttu-id="79490-184">IEmailSender 구현</span><span class="sxs-lookup"><span data-stu-id="79490-184">Implement IEmailSender</span></span>

<span data-ttu-id="79490-185">구현 `IEmailSender`를 만듭니다 *Services/EmailSender.cs* 다음과 비슷한 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="79490-185">To Implement `IEmailSender`, create *Services/EmailSender.cs* with code similar to the following:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Services/EmailSender.cs)]

### <a name="configure-startup-to-support-email"></a><span data-ttu-id="79490-186">시작 전자 메일을 지원 하도록 구성</span><span class="sxs-lookup"><span data-stu-id="79490-186">Configure startup to support email</span></span>

<span data-ttu-id="79490-187">다음 코드를 추가 합니다 `ConfigureServices` 의 메서드를 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="79490-187">Add the following code to the `ConfigureServices` method in the *Startup.cs* file:</span></span>

* <span data-ttu-id="79490-188">추가 `EmailSender` singleton 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-188">Add `EmailSender` as a singleton service.</span></span>
* <span data-ttu-id="79490-189">등록 된 `AuthMessageSenderOptions` 구성 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="79490-189">Register the `AuthMessageSenderOptions` configuration instance.</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Startup.cs?name=snippet2&highlight=12-99)]

## <a name="enable-account-confirmation-and-password-recovery"></a><span data-ttu-id="79490-190">계정 확인 및 암호 복구를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="79490-190">Enable account confirmation and password recovery</span></span>

<span data-ttu-id="79490-191">서식 파일에 계정 확인 및 암호 복구를 위한 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-191">The template has the code for account confirmation and password recovery.</span></span> <span data-ttu-id="79490-192">찾을 합니다 `OnPostAsync` 의 메서드 *Areas/Identity/Pages/Account/Register.cshtml.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-192">Find the `OnPostAsync` method in *Areas/Identity/Pages/Account/Register.cshtml.cs*.</span></span>

<span data-ttu-id="79490-193">다음 줄을 주석으로 자동으로 로그온 하에서 새로 등록 된 사용자를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-193">Prevent newly registered users from being automatically logged on by commenting out the following line:</span></span>

```csharp
await _signInManager.SignInAsync(user, isPersistent: false);
```

<span data-ttu-id="79490-194">전체 메서드는 강조 표시 된 변경 된 줄으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-194">The complete method is shown with the changed line highlighted:</span></span>

[!code-csharp[](accconfirm/sample/WebPWrecover21/Areas/Identity/Pages/Account/Register.cshtml.cs?highlight=22&name=snippet_Register)]

## <a name="register-confirm-email-and-reset-password"></a><span data-ttu-id="79490-195">등록 하 고, 전자 메일을 확인 하 고, 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="79490-195">Register, confirm email, and reset password</span></span>

<span data-ttu-id="79490-196">웹 앱을 실행 하 고 계정 확인 및 암호 복구 흐름을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-196">Run the web app, and test the account confirmation and password recovery flow.</span></span>

* <span data-ttu-id="79490-197">앱을 실행 하 고 새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="79490-197">Run the app and register a new user</span></span>

  ![웹 응용 프로그램 계정 등록 보기](accconfirm/_static/loginaccconfirm1.png)

* <span data-ttu-id="79490-199">계정 확인 링크에 대 한 전자 메일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-199">Check your email for the account confirmation link.</span></span> <span data-ttu-id="79490-200">참조 [전자 메일을 디버그](#debug) 전자 메일을 얻지 못한 경우.</span><span class="sxs-lookup"><span data-stu-id="79490-200">See [Debug email](#debug) if you don't get the email.</span></span>
* <span data-ttu-id="79490-201">전자 메일 확인 하기 위한 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-201">Click the link to confirm your email.</span></span>
* <span data-ttu-id="79490-202">전자 메일 및 암호를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-202">Log in with your email and password.</span></span>
* <span data-ttu-id="79490-203">로그 오프 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-203">Log off.</span></span>

### <a name="view-the-manage-page"></a><span data-ttu-id="79490-204">관리 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="79490-204">View the manage page</span></span>

<span data-ttu-id="79490-205">브라우저에서 사용자 이름을 선택 합니다. ![사용자 이름이 있는 브라우저 창](accconfirm/_static/un.png)</span><span class="sxs-lookup"><span data-stu-id="79490-205">Select your user name in the browser: ![browser window with user name](accconfirm/_static/un.png)</span></span>

<span data-ttu-id="79490-206">사용자 이름을 보려면 탐색 모음을 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-206">You might need to expand the navbar to see user name.</span></span>

![탐색 모음](accconfirm/_static/x.png)

<span data-ttu-id="79490-208">사용 하 여 관리 페이지가 표시 되는 **프로필** 탭이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-208">The manage page is displayed with the **Profile** tab selected.</span></span> <span data-ttu-id="79490-209">합니다 **전자 메일** 확인 된 전자 메일을 나타내는 확인란을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="79490-209">The **Email** shows a check box indicating the email has been confirmed.</span></span>

### <a name="test-password-reset"></a><span data-ttu-id="79490-210">테스트 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="79490-210">Test password reset</span></span>

* <span data-ttu-id="79490-211">에 로그인 하는 경우 선택 **로그 아웃**합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-211">If you're logged in, select **Logout**.</span></span>
* <span data-ttu-id="79490-212">선택 합니다 **에 로그인** 연결 하 고 선택 합니다 **암호를 잊으셨나요?** 링크.</span><span class="sxs-lookup"><span data-stu-id="79490-212">Select the **Log in** link and select the **Forgot your password?** link.</span></span>
* <span data-ttu-id="79490-213">계정을 등록 하는 데 전자 메일을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-213">Enter the email you used to register the account.</span></span>
* <span data-ttu-id="79490-214">암호 재설정에 대 한 링크가 포함 된 전자 메일이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-214">An email with a link to reset your password is sent.</span></span> <span data-ttu-id="79490-215">전자 메일을 확인 하 고 암호 재설정에 대 한 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-215">Check your email and click the link to reset your password.</span></span> <span data-ttu-id="79490-216">암호가 성공적으로 다시 설정, 메일 및 새 암호를 사용 하 여 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-216">After your password has been successfully reset, you can log in with your email and new password.</span></span>

<a name="debug"></a>

### <a name="debug-email"></a><span data-ttu-id="79490-217">전자 메일을 디버그</span><span class="sxs-lookup"><span data-stu-id="79490-217">Debug email</span></span>

<span data-ttu-id="79490-218">경우 전자 메일 작업을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-218">If you can't get email working:</span></span>

* <span data-ttu-id="79490-219">중단점을 설정 `EmailSender.Execute` 확인 하려면 `SendGridClient.SendEmailAsync` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-219">Set a breakpoint in `EmailSender.Execute` to verify `SendGridClient.SendEmailAsync` is called.</span></span>
* <span data-ttu-id="79490-220">만들기는 [전자 메일을 보내는 콘솔 앱](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html) 비슷한 코드를 사용 하 여 `EmailSender.Execute`입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-220">Create a [console app to send email](https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html) using similar code to `EmailSender.Execute`.</span></span>
* <span data-ttu-id="79490-221">검토 합니다 [전자 메일 작업](https://sendgrid.com/docs/User_Guide/email_activity.html) 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-221">Review the [Email Activity](https://sendgrid.com/docs/User_Guide/email_activity.html) page.</span></span>
* <span data-ttu-id="79490-222">스팸 폴더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-222">Check your spam folder.</span></span>
* <span data-ttu-id="79490-223">다른 전자 메일 별칭에는 다른 전자 메일 공급자 (Microsoft, Yahoo, Gmail 등)를 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="79490-223">Try another email alias on a different email provider (Microsoft, Yahoo, Gmail, etc.)</span></span>
* <span data-ttu-id="79490-224">다른 메일 계정으로 보내기를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-224">Try sending to different email accounts.</span></span>

<span data-ttu-id="79490-225">**보안 모범 사례** 하는 것 **하지** 테스트 및 개발에서 프로덕션 비밀을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-225">**A security best practice** is to **not** use production secrets in test and development.</span></span> <span data-ttu-id="79490-226">Azure에 앱을 게시 하는 경우 Azure 웹 앱 포털에서 응용 프로그램 설정으로 SendGrid 비밀을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-226">If you publish the app to Azure, you can set the SendGrid secrets as application settings in the Azure Web App portal.</span></span> <span data-ttu-id="79490-227">구성 시스템 환경 변수에서 키를 읽을 수 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79490-227">The configuration system is set up to read keys from environment variables.</span></span>

## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="79490-228">로컬 및 소셜 로그인 계정을 병합합니다</span><span class="sxs-lookup"><span data-stu-id="79490-228">Combine social and local login accounts</span></span>

<span data-ttu-id="79490-229">이 섹션을 완료 하려면 먼저 외부 인증 공급자를 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-229">To complete this section, you must first enable an external authentication provider.</span></span> <span data-ttu-id="79490-230">참조 [Facebook, Google 및 외부 공급자 인증](xref:security/authentication/social/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-230">See [Facebook, Google, and external provider authentication](xref:security/authentication/social/index).</span></span>

<span data-ttu-id="79490-231">로컬 및 소셜 계정 전자 메일 링크를 클릭 하 여 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-231">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="79490-232">그러나 다음 순서로 "RickAndMSFT@gmail.com" 로컬 로그인;으로 처음 만들어질 수 계정으로 소셜 로그인을 먼저 만든 다음 로컬 로그인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-232">In the following sequence, "RickAndMSFT@gmail.com" is first created as a local login; however, you can create the account as a social login first, then add a local login.</span></span>

![웹 응용 프로그램: RickAndMSFT@gmail.com 인증 된 사용자](accconfirm/_static/rick.png)

<span data-ttu-id="79490-234">클릭 합니다 **관리** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-234">Click on the **Manage** link.</span></span> <span data-ttu-id="79490-235">이 계정과 연결 된 참고 0 외부 (소셜 로그인)</span><span class="sxs-lookup"><span data-stu-id="79490-235">Note the 0 external (social logins) associated with this account.</span></span>

![보기 관리](accconfirm/_static/manage.png)

<span data-ttu-id="79490-237">다른 로그인 서비스에 대 한 링크를 클릭 하 고 앱 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-237">Click the link to another login service and accept the app requests.</span></span> <span data-ttu-id="79490-238">다음 이미지에서는 Facebook는 외부 인증 공급자:</span><span class="sxs-lookup"><span data-stu-id="79490-238">In the following image, Facebook is the external authentication provider:</span></span>

![Facebook을 목록 외부 로그인 보기를 관리 합니다.](accconfirm/_static/fb.png)

<span data-ttu-id="79490-240">두 개의 계정은 결합 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-240">The two accounts have been combined.</span></span> <span data-ttu-id="79490-241">두 계정으로 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-241">You are able to log on with either account.</span></span> <span data-ttu-id="79490-242">사용자가 자신의 소셜 로그인 인증 서비스가 다운 된 또는 가능성이 소셜 계정에 대 한 액세스를 손실 했습니다 되는 경우 로컬 계정을 추가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-242">You might want your users to add local accounts in case their social login authentication service is down, or more likely they've lost access to their social account.</span></span>

## <a name="enable-account-confirmation-after-a-site-has-users"></a><span data-ttu-id="79490-243">사이트 사용자 후 계정 확인을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="79490-243">Enable account confirmation after a site has users</span></span>

<span data-ttu-id="79490-244">사용자를 사용 하 여 사이트에서 계정 확인을 사용 하도록 설정 하면 모든 기존 사용자를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="79490-244">Enabling account confirmation on a site with users locks out all the existing users.</span></span> <span data-ttu-id="79490-245">해당 계정 확인 되지 때문에 기존 사용자가 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79490-245">Existing users are locked out because their accounts aren't confirmed.</span></span> <span data-ttu-id="79490-246">기존 사용자 잠금 문제를 해결 하려면 다음 방법 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-246">To work around existing user lockout, use one of the following approaches:</span></span>

* <span data-ttu-id="79490-247">로 확인 되 고 모든 기존 사용자를 표시 하도록 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-247">Update the database to mark all existing users as being confirmed.</span></span>
* <span data-ttu-id="79490-248">기존 사용자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79490-248">Confirm exiting users.</span></span> <span data-ttu-id="79490-249">예를 들어 일괄 처리-송신 확인 링크를 사용 하 여 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="79490-249">For example, batch-send emails with confirmation links.</span></span>

::: moniker-end
