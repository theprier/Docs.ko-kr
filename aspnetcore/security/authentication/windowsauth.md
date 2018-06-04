---
title: ASP.NET Core에 Windows 인증을 구성 합니다.
author: ardalis
description: 이 문서에서는 IIS Express, IIS, HTTP.sys 및 WebListener를 사용 하 여 ASP.NET Core에 Windows 인증을 구성 하는 방법을 설명 합니다.
manager: wpickett
ms.author: riande
ms.date: 10/24/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/windowsauth
ms.openlocfilehash: dbcef095561fe656bdd28c4fa6560c6b269a2db0
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34689011"
---
# <a name="configure-windows-authentication-in-aspnet-core"></a><span data-ttu-id="73768-103">ASP.NET Core에 Windows 인증을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-103">Configure Windows authentication in ASP.NET Core</span></span>

<span data-ttu-id="73768-104">작성자: [Steve Smith](https://ardalis.com) 및 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="73768-104">By [Steve Smith](https://ardalis.com) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="73768-105">Iis에서 호스팅되는 ASP.NET Core 응용 프로그램에 대 한 Windows 인증을 구성할 수 있습니다 [HTTP.sys](xref:fundamentals/servers/httpsys), 또는 [WebListener](xref:fundamentals/servers/weblistener)합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-105">Windows authentication can be configured for ASP.NET Core apps hosted with IIS, [HTTP.sys](xref:fundamentals/servers/httpsys), or [WebListener](xref:fundamentals/servers/weblistener).</span></span>

## <a name="what-is-windows-authentication"></a><span data-ttu-id="73768-106">Windows 인증 이란?</span><span class="sxs-lookup"><span data-stu-id="73768-106">What is Windows authentication?</span></span>

<span data-ttu-id="73768-107">ASP.NET Core 응용 프로그램의 사용자를 인증 하는 운영 체제는 Windows 인증 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-107">Windows authentication relies on the operating system to authenticate users of ASP.NET Core apps.</span></span> <span data-ttu-id="73768-108">서버에 다른 Windows 계정 또는 Active Directory 도메인 id를 사용 하 여 사용자를 식별 하는 회사 네트워크에서 실행 될 때 Windows 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-108">You can use Windows authentication when your server runs on a corporate network using Active Directory domain identities or other Windows accounts to identify users.</span></span> <span data-ttu-id="73768-109">Windows 인증은 사용자, 클라이언트 응용 프로그램 및 웹 서버는 동일한 Windows 도메인에 속해 인트라넷 환경에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-109">Windows authentication is best suited to intranet environments in which users, client applications, and web servers belong to the same Windows domain.</span></span>

<span data-ttu-id="73768-110">[Windows 인증 및 iis 설치에 대 한 자세한](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/)합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-110">[Learn more about Windows authentication and installing it for IIS](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/).</span></span>

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="73768-111">ASP.NET Core 응용 프로그램에서 Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="73768-111">Enable Windows authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="73768-112">Visual Studio 웹 응용 프로그램 템플릿은 Windows 인증을 지원 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-112">The Visual Studio Web Application template can be configured to support Windows authentication.</span></span>

### <a name="use-the-windows-authentication-app-template"></a><span data-ttu-id="73768-113">Windows 인증 앱 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="73768-113">Use the Windows authentication app template</span></span>

<span data-ttu-id="73768-114">Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-114">In Visual Studio:</span></span>
1. <span data-ttu-id="73768-115">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73768-115">Create a new ASP.NET Core Web Application.</span></span> 
1. <span data-ttu-id="73768-116">템플릿 목록에서 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-116">Select Web Application from the list of templates.</span></span>
1. <span data-ttu-id="73768-117">선택 된 **인증 변경** 선택한 단추 **Windows 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-117">Select the **Change Authentication** button and select **Windows Authentication**.</span></span> 

<span data-ttu-id="73768-118">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-118">Run the app.</span></span> <span data-ttu-id="73768-119">사용자 이름 상단에 표시 됩니다. 응용 프로그램의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="73768-119">The username appears in the top right of the app.</span></span>

![Windows 인증에 대 한 브라우저 스크린 샷](windowsauth/_static/browser-screenshot.png)

<span data-ttu-id="73768-121">IIS Express를 사용 하 여 개발 작업에서는 서식 파일에 Windows 인증을 사용 하는 데 필요한 모든 구성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-121">For development work using IIS Express, the template provides all the configuration necessary to use Windows authentication.</span></span> <span data-ttu-id="73768-122">다음 섹션에는 Windows 인증에 대 한 ASP.NET Core 응용 프로그램을 수동으로 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73768-122">The following section shows how to manually configure an ASP.NET Core app for Windows authentication.</span></span>

### <a name="visual-studio-settings-for-windows-and-anonymous-authentication"></a><span data-ttu-id="73768-123">Windows 및 익명 인증에 대 한 visual Studio 설정</span><span class="sxs-lookup"><span data-stu-id="73768-123">Visual Studio settings for Windows and anonymous authentication</span></span>

<span data-ttu-id="73768-124">Visual Studio 프로젝트 **속성** 페이지의 **디버그** 탭은 Windows 인증 및 익명 인증에 대 한 확인란을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-124">The Visual Studio project **Properties** page's **Debug** tab provides check boxes for Windows authentication and anonymous authentication.</span></span>

![Windows 인증에 대 한 브라우저 스크린 샷](windowsauth/_static/vs-auth-property-menu.png)

<span data-ttu-id="73768-126">이러한 두 속성을 구성할 수 있습니다 또는 *launchSettings.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="73768-126">Alternatively, these two properties can be configured in the *launchSettings.json* file:</span></span>

[!code-json[](windowsauth/sample/launchSettings.json?highlight=3-4)]

## <a name="enable-windows-authentication-with-iis"></a><span data-ttu-id="73768-127">Iis Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="73768-127">Enable Windows authentication with IIS</span></span>

<span data-ttu-id="73768-128">IIS에서 사용 하는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) ASP.NET Core 응용 프로그램 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-128">IIS uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to host ASP.NET Core apps.</span></span> <span data-ttu-id="73768-129">모듈을 사용 하면 Windows 인증을 기본적으로 IIS에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-129">The module allows Windows authentication to flow to IIS by default.</span></span> <span data-ttu-id="73768-130">Iis에서 응용 프로그램이 아닌 Windows 인증이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73768-130">Windows authentication is configured in IIS, not the app.</span></span> <span data-ttu-id="73768-131">다음 섹션에서는 Windows 인증을 사용 하도록 ASP.NET Core 응용 프로그램을 구성 하려면 IIS 관리자를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73768-131">The following sections show how to use IIS Manager to configure an ASP.NET Core app to use Windows authentication.</span></span>

### <a name="create-a-new-iis-site"></a><span data-ttu-id="73768-132">새 IIS 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="73768-132">Create a new IIS site</span></span>

<span data-ttu-id="73768-133">이름 및 폴더를 지정 하 고 새 응용 프로그램 풀을 만들 수 있도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-133">Specify a name and folder and allow it to create a new application pool.</span></span>

### <a name="customize-authentication"></a><span data-ttu-id="73768-134">인증을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="73768-134">Customize authentication</span></span>

<span data-ttu-id="73768-135">사이트에 대 한 인증 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73768-135">Open the Authentication menu for the site.</span></span>

![IIS 인증 메뉴](windowsauth/_static/iis-authentication-menu.png)

<span data-ttu-id="73768-137">익명 인증을 사용 하지 않도록 설정 하 고 Windows 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-137">Disable Anonymous Authentication and enable Windows Authentication.</span></span>

![IIS 인증 설정](windowsauth/_static/iis-auth-settings.png)

### <a name="publish-your-project-to-the-iis-site-folder"></a><span data-ttu-id="73768-139">IIS 사이트 폴더에 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-139">Publish your project to the IIS site folder</span></span>

<span data-ttu-id="73768-140">Visual Studio 또는.NET Core CLI를 사용 하 여 대상 폴더에 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-140">Using Visual Studio or the .NET Core CLI, publish the app to the destination folder.</span></span>

![Visual Studio 게시 대화 상자](windowsauth/_static/vs-publish-app.png)

<span data-ttu-id="73768-142">에 대 한 자세한 내용은 [를 IIS에 게시](xref:host-and-deploy/iis/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-142">Learn more about [publishing to IIS](xref:host-and-deploy/iis/index).</span></span>

<span data-ttu-id="73768-143">Windows 인증 작동 확인 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-143">Launch the app to verify Windows authentication is working.</span></span>

## <a name="enable-windows-authentication-with-httpsys-or-weblistener"></a><span data-ttu-id="73768-144">HTTP.sys 또는 WebListener와 함께 Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="73768-144">Enable Windows authentication with HTTP.sys or WebListener</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="73768-145">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="73768-145">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="73768-146">Kestrel Windows 인증을 지원 하지 않지만 사용할 수 있습니다 [HTTP.sys](xref:fundamentals/servers/httpsys) Windows에서 자체 호스팅된 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-146">Although Kestrel doesn't support Windows authentication, you can use [HTTP.sys](xref:fundamentals/servers/httpsys) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="73768-147">다음 예제에서는 Windows 인증과 함께 HTTP.sys를 사용 하도록 응용 프로그램의 웹 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-147">The following example configures the app's web host to use HTTP.sys with Windows authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program2x.cs?highlight=9-14)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="73768-148">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="73768-148">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="73768-149">Kestrel Windows 인증을 지원 하지 않지만 사용할 수 있습니다 [WebListener](xref:fundamentals/servers/weblistener) Windows에서 자체 호스팅된 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-149">Although Kestrel doesn't support Windows authentication, you can use [WebListener](xref:fundamentals/servers/weblistener) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="73768-150">다음 예제에서는 Windows 인증과 함께 WebListener를 사용 하도록 응용 프로그램의 웹 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-150">The following example configures the app's web host to use WebListener with Windows authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program1x.cs?highlight=6-11)]

---

## <a name="work-with-windows-authentication"></a><span data-ttu-id="73768-151">Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="73768-151">Work with Windows authentication</span></span>

<span data-ttu-id="73768-152">구성 상태에 대 한 익명 액세스 결정 되는 방식으로 `[Authorize]` 및 `[AllowAnonymous]` 특성이 앱에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73768-152">The configuration state of anonymous access determines the way in which the `[Authorize]` and `[AllowAnonymous]` attributes are used in the app.</span></span> <span data-ttu-id="73768-153">다음 두 섹션에서는 익명 액세스의 허용 되 고 허용 되지 않는 구성 상태를 처리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-153">The following two sections explain how to handle the disallowed and allowed configuration states of anonymous access.</span></span>

### <a name="disallow-anonymous-access"></a><span data-ttu-id="73768-154">익명 액세스 허용 안 함</span><span class="sxs-lookup"><span data-stu-id="73768-154">Disallow anonymous access</span></span>

<span data-ttu-id="73768-155">Windows 인증을 사용 하 고 익명 액세스를 비활성화 하는 경우는 `[Authorize]` 및 `[AllowAnonymous]` 특성은 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-155">When Windows authentication is enabled and anonymous access is disabled, the `[Authorize]` and `[AllowAnonymous]` attributes have no effect.</span></span> <span data-ttu-id="73768-156">IIS 사이트 (또는 HTTP.sys 또는 WebListener 서버)에 익명 액세스를 허용 하도록 구성 된, 경우 요청에 결코 응용 프로그램에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-156">If the IIS site (or HTTP.sys or WebListener server) is configured to disallow anonymous access, the request never reaches your app.</span></span> <span data-ttu-id="73768-157">이러한 이유로 `[AllowAnonymous]` 특성은 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-157">For this reason, the `[AllowAnonymous]` attribute isn't applicable.</span></span>

### <a name="allow-anonymous-access"></a><span data-ttu-id="73768-158">익명 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="73768-158">Allow anonymous access</span></span>

<span data-ttu-id="73768-159">사용 하 여 Windows 인증 및 익명 액세스를 모두 설정 된 경우는 `[Authorize]` 및 `[AllowAnonymous]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="73768-159">When both Windows authentication and anonymous access are enabled, use the `[Authorize]` and `[AllowAnonymous]` attributes.</span></span> <span data-ttu-id="73768-160">`[Authorize]` 특성을 사용 하면 Windows 인증 필요 진정으로 응용 프로그램의 부분을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-160">The `[Authorize]` attribute allows you to secure pieces of the app which truly do require Windows authentication.</span></span> <span data-ttu-id="73768-161">`[AllowAnonymous]` 특성 재정의 `[Authorize]` 특성 익명 액세스를 허용 하는 앱 내에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-161">The `[AllowAnonymous]` attribute overrides `[Authorize]` attribute usage within apps which allow anonymous access.</span></span> <span data-ttu-id="73768-162">참조 [간단한 인증](xref:security/authorization/simple) 특성 사용 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-162">See [Simple Authorization](xref:security/authorization/simple) for attribute usage details.</span></span>

<span data-ttu-id="73768-163">ASP.NET Core에서 2.x는 `[Authorize]` 특성 추가 구성이 필요 *Startup.cs* Windows 인증에 대 한 익명 요청을 보도록 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="73768-163">In ASP.NET Core 2.x, the `[Authorize]` attribute requires additional configuration in *Startup.cs* to challenge anonymous requests for Windows authentication.</span></span> <span data-ttu-id="73768-164">권장된 구성을 사용 하 고 웹 서버에 따라 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="73768-164">The recommended configuration varies slightly based on the web server being used.</span></span>

> [!NOTE]
> <span data-ttu-id="73768-165">기본적으로 빈 403 HTTP 응답을 페이지에 액세스할 수 있는 권한 부족 한 사용자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73768-165">By default, users who lack authorization to access a page are presented with an empty HTTP 403 response.</span></span> <span data-ttu-id="73768-166">[StatusCodePages 미들웨어](xref:fundamentals/error-handling#configuring-status-code-pages) "액세스 거부" 더 나은 환경을 제공 하기 위해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-166">The [StatusCodePages middleware](xref:fundamentals/error-handling#configuring-status-code-pages) can be configured to provide users with a better "Access Denied" experience.</span></span>

#### <a name="iis"></a><span data-ttu-id="73768-167">IIS</span><span class="sxs-lookup"><span data-stu-id="73768-167">IIS</span></span>

<span data-ttu-id="73768-168">IIS를 사용 하는 경우 다음을 추가 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="73768-168">If using IIS, add the following to the `ConfigureServices` method:</span></span> 

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a><span data-ttu-id="73768-169">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="73768-169">HTTP.sys</span></span>

<span data-ttu-id="73768-170">HTTP.sys를 사용 하는 경우 다음을 추가 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="73768-170">If using HTTP.sys, add the following to the `ConfigureServices` method:</span></span>

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a><span data-ttu-id="73768-171">가장</span><span class="sxs-lookup"><span data-stu-id="73768-171">Impersonation</span></span>

<span data-ttu-id="73768-172">ASP.NET Core 가장을 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-172">ASP.NET Core doesn't implement impersonation.</span></span> <span data-ttu-id="73768-173">앱에 대 한 모든 요청을 응용 프로그램 풀 또는 프로세스 id를 사용 하 여 응용 프로그램 id로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73768-173">Apps run with the application identity for all requests, using app pool or process identity.</span></span> <span data-ttu-id="73768-174">사용 하 여 명시적으로 사용자를 대신 하 여 작업을 수행 해야 할 경우 `WindowsIdentity.RunImpersonated`합니다.</span><span class="sxs-lookup"><span data-stu-id="73768-174">If you need to explicitly perform an action on behalf of a user, use `WindowsIdentity.RunImpersonated`.</span></span> <span data-ttu-id="73768-175">이 컨텍스트에서 단일 작업을 실행 하 고 컨텍스트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-175">Run a single action in this context and then close the context.</span></span>

[!code-csharp[](windowsauth/sample/Startup.cs?name=snippet_Impersonate&highlight=10-18)]

<span data-ttu-id="73768-176">`RunImpersonated` 비동기 작업을 지원 하지 않으므로 하 고 복잡 한 시나리오에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-176">Note that `RunImpersonated` doesn't support asynchronous operations and shouldn't be used for complex scenarios.</span></span> <span data-ttu-id="73768-177">예를 들어 전체 요청 또는 미들웨어 체인 래핑 지원 아니거나 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="73768-177">For example, wrapping entire requests or middleware chains isn't supported or recommended.</span></span>

---
