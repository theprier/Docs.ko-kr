---
title: ASP.NET Core에서 Windows 인증을 구성 합니다.
author: ardalis
description: 이 문서에서는 ASP.NET core에서 IIS Express, IIS, HTTP.sys 및 WebListener를 사용 하 여 Windows 인증을 구성 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 08/18/2018
uid: security/authentication/windowsauth
ms.openlocfilehash: 93b1a1de74ef6554d48709b04870f7e23738846b
ms.sourcegitcommit: 15d7bd0b2c4e6fe9ac335d658bab71a45ca5bc72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2018
ms.locfileid: "41829804"
---
# <a name="configure-windows-authentication-in-aspnet-core"></a><span data-ttu-id="969fe-103">ASP.NET Core에서 Windows 인증을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-103">Configure Windows Authentication in ASP.NET Core</span></span>

<span data-ttu-id="969fe-104">작성자: [Steve Smith](https://ardalis.com) 및 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="969fe-104">By [Steve Smith](https://ardalis.com) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="969fe-105">Iis에서 호스팅되는 ASP.NET Core 앱에 대 한 Windows 인증을 구성할 수 있습니다 [HTTP.sys](xref:fundamentals/servers/httpsys), 또는 [WebListener](xref:fundamentals/servers/weblistener)합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-105">Windows Authentication can be configured for ASP.NET Core apps hosted with IIS, [HTTP.sys](xref:fundamentals/servers/httpsys), or [WebListener](xref:fundamentals/servers/weblistener).</span></span>

## <a name="windows-authentication"></a><span data-ttu-id="969fe-106">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="969fe-106">Windows Authentication</span></span>

<span data-ttu-id="969fe-107">Windows 인증은 ASP.NET Core 앱의 사용자를 인증 하는 운영 체제에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-107">Windows Authentication relies on the operating system to authenticate users of ASP.NET Core apps.</span></span> <span data-ttu-id="969fe-108">서버에 다른 Windows 계정 또는 Active Directory 도메인 id를 사용 하 여 사용자를 식별 하는 회사 네트워크에서 실행 될 때 Windows 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-108">You can use Windows Authentication when your server runs on a corporate network using Active Directory domain identities or other Windows accounts to identify users.</span></span> <span data-ttu-id="969fe-109">Windows 인증 사용자, 클라이언트 응용 프로그램 및 웹 서버는 동일한 Windows 도메인에 속해 인트라넷 환경에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-109">Windows Authentication is best suited to intranet environments in which users, client applications, and web servers belong to the same Windows domain.</span></span>

<span data-ttu-id="969fe-110">[Windows 인증에 자세히 알아보기 및 IIS에 대 한 설치](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/)합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-110">[Learn more about Windows Authentication and installing it for IIS](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/).</span></span>

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="969fe-111">ASP.NET Core 앱에서 Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="969fe-111">Enable Windows Authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="969fe-112">Visual Studio 웹 응용 프로그램 템플릿은 Windows 인증을 지원 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-112">The Visual Studio Web Application template can be configured to support Windows Authentication.</span></span>

### <a name="use-the-windows-authentication-app-template"></a><span data-ttu-id="969fe-113">Windows 인증 앱 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="969fe-113">Use the Windows Authentication app template</span></span>

<span data-ttu-id="969fe-114">Visual studio:</span><span class="sxs-lookup"><span data-stu-id="969fe-114">In Visual Studio:</span></span>

1. <span data-ttu-id="969fe-115">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-115">Create a new ASP.NET Core Web Application.</span></span>
1. <span data-ttu-id="969fe-116">템플릿 목록에서 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-116">Select Web Application from the list of templates.</span></span>
1. <span data-ttu-id="969fe-117">선택 된 **인증 변경** 단추를 선택 **Windows 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-117">Select the **Change Authentication** button and select **Windows Authentication**.</span></span>

<span data-ttu-id="969fe-118">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-118">Run the app.</span></span> <span data-ttu-id="969fe-119">위쪽에 표시 되는 사용자 앱의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-119">The username appears in the top right of the app.</span></span>

![Windows 인증에 대 한 브라우저 스크린 샷](windowsauth/_static/browser-screenshot.png)

<span data-ttu-id="969fe-121">IIS Express를 사용 하 여 개발 작업에 대 한 템플릿을 Windows 인증을 사용 하는 데 필요한 모든 구성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-121">For development work using IIS Express, the template provides all the configuration necessary to use Windows Authentication.</span></span> <span data-ttu-id="969fe-122">다음 섹션에는 Windows 인증에 대 한 ASP.NET Core 앱을 수동으로 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-122">The following section shows how to manually configure an ASP.NET Core app for Windows Authentication.</span></span>

### <a name="visual-studio-settings-for-windows-and-anonymous-authentication"></a><span data-ttu-id="969fe-123">Windows 및 익명 인증을 위해 visual Studio 설정</span><span class="sxs-lookup"><span data-stu-id="969fe-123">Visual Studio settings for Windows and anonymous authentication</span></span>

<span data-ttu-id="969fe-124">Visual Studio 프로젝트 **속성** 페이지의 **디버그** 탭은 Windows 인증 및 익명 인증에 대 한 확인란을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-124">The Visual Studio project **Properties** page's **Debug** tab provides check boxes for Windows Authentication and anonymous authentication.</span></span>

![Windows 인증에 대 한 브라우저 스크린 샷](windowsauth/_static/vs-auth-property-menu.png)

<span data-ttu-id="969fe-126">이러한 두 속성을 구성할 수 있습니다 또는 합니다 *launchSettings.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="969fe-126">Alternatively, these two properties can be configured in the *launchSettings.json* file:</span></span>

[!code-json[](windowsauth/sample/launchSettings.json?highlight=3-4)]

## <a name="enable-windows-authentication-with-iis"></a><span data-ttu-id="969fe-127">IIS 사용 하 여 Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="969fe-127">Enable Windows Authentication with IIS</span></span>

<span data-ttu-id="969fe-128">IIS에서 사용 하 여 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) ASP.NET Core 앱을 호스트 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-128">IIS uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to host ASP.NET Core apps.</span></span> <span data-ttu-id="969fe-129">Windows 인증은 응용 프로그램이 아닌 IIS에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-129">Windows Authentication is configured in IIS, not the app.</span></span> <span data-ttu-id="969fe-130">다음 섹션에서는 IIS 관리자를 사용 하 여 Windows 인증을 사용 하도록 ASP.NET Core 앱을 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-130">The following sections show how to use IIS Manager to configure an ASP.NET Core app to use Windows Authentication.</span></span>

### <a name="iis-configuration"></a><span data-ttu-id="969fe-131">IIS 구성</span><span class="sxs-lookup"><span data-stu-id="969fe-131">IIS configuration</span></span>

<span data-ttu-id="969fe-132">Windows 인증을 위해 IIS 역할 서비스를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-132">Enable the IIS Role Service for Windows Authentication.</span></span> <span data-ttu-id="969fe-133">자세한 내용은 [IIS 역할 서비스 (2 단계 참조)에서 Windows 인증 사용](xref:host-and-deploy/iis/index#iis-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-133">For more information, see [Enable Windows Authentication in IIS Role Services (see Step 2)](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

<span data-ttu-id="969fe-134">IIS 통합 미들웨어는 기본적으로 자동으로 요청을 인증 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-134">IIS Integration Middleware is configured to automatically authenticate requests by default.</span></span> <span data-ttu-id="969fe-135">자세한 내용은 [IIS 사용 하 여 Windows에서 ASP.NET Core 호스팅: IIS 옵션 (AutomaticAuthentication)](xref:host-and-deploy/iis/index#iis-options)합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-135">For more information, see [Host ASP.NET Core on Windows with IIS: IIS options (AutomaticAuthentication)](xref:host-and-deploy/iis/index#iis-options).</span></span>

<span data-ttu-id="969fe-136">ASP.NET Core 모듈은 기본적으로 앱에 Windows 인증 토큰을 전달 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-136">The ASP.NET Core Module is configured to forward the Windows Authentication token to the app by default.</span></span> <span data-ttu-id="969fe-137">자세한 내용은 [ASP.NET Core 모듈 구성 참조: aspNetCore 요소의 특성](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-137">For more information, see [ASP.NET Core Module configuration reference: Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

### <a name="create-a-new-iis-site"></a><span data-ttu-id="969fe-138">새 IIS 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="969fe-138">Create a new IIS site</span></span>

<span data-ttu-id="969fe-139">이름 및 폴더를 지정 하 고 새 응용 프로그램 풀을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-139">Specify a name and folder and allow it to create a new application pool.</span></span>

### <a name="customize-authentication"></a><span data-ttu-id="969fe-140">인증을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="969fe-140">Customize authentication</span></span>

<span data-ttu-id="969fe-141">사이트에 대 한 인증 기능을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-141">Open the Authentication features for the site.</span></span>

![IIS 인증 메뉴](windowsauth/_static/iis-authentication-menu.png)

<span data-ttu-id="969fe-143">익명 인증을 사용 하지 않도록 설정 하 고 Windows 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-143">Disable Anonymous Authentication and enable Windows Authentication.</span></span>

![IIS 인증 설정](windowsauth/_static/iis-auth-settings.png)

### <a name="publish-your-project-to-the-iis-site-folder"></a><span data-ttu-id="969fe-145">IIS 사이트 폴더에 프로젝트 게시</span><span class="sxs-lookup"><span data-stu-id="969fe-145">Publish your project to the IIS site folder</span></span>

<span data-ttu-id="969fe-146">대상 폴더에 앱을 게시 Visual Studio 또는.NET Core CLI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-146">Using Visual Studio or the .NET Core CLI, publish the app to the destination folder.</span></span>

![Visual Studio 게시 대화 상자](windowsauth/_static/vs-publish-app.png)

<span data-ttu-id="969fe-148">에 대해 자세히 알아보세요 [IIS에 게시](xref:host-and-deploy/iis/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-148">Learn more about [publishing to IIS](xref:host-and-deploy/iis/index).</span></span>

<span data-ttu-id="969fe-149">Windows 인증이 작동을 확인 하려면 앱을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-149">Launch the app to verify Windows Authentication is working.</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="enable-windows-authentication-with-httpsys"></a><span data-ttu-id="969fe-150">HTTP.sys 사용 하 여 Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="969fe-150">Enable Windows Authentication with HTTP.sys</span></span>

<span data-ttu-id="969fe-151">Kestrel은 Windows 인증을 지원 하지 않지만 사용할 수 있습니다 [HTTP.sys](xref:fundamentals/servers/httpsys) Windows에서 자체 호스팅된 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-151">Although Kestrel doesn't support Windows Authentication, you can use [HTTP.sys](xref:fundamentals/servers/httpsys) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="969fe-152">다음 예제에서는 Windows 인증을 사용 하 여 HTTP.sys를 사용 하도록 앱의 웹 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-152">The following example configures the app's web host to use HTTP.sys with Windows Authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program2x.cs?highlight=9-14)]

> [!NOTE]
> <span data-ttu-id="969fe-153">Kerberos 인증 프로토콜을 사용 하 여 커널 모드 인증을 HTTP.sys 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-153">HTTP.sys delegates to kernel mode authentication with the Kerberos authentication protocol.</span></span> <span data-ttu-id="969fe-154">Kerberos 및 HTTP.sys를 사용 하 여 사용자 모드 인증이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-154">User mode authentication isn't supported with Kerberos and HTTP.sys.</span></span> <span data-ttu-id="969fe-155">컴퓨터 계정이 Active Directory에서 가져온 Kerberos 토큰/티켓의 암호를 해독 하는 데 사용 하 고 사용자를 인증 하는 서버에 클라이언트에서 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-155">The machine account must be used to decrypt the Kerberos token/ticket that's obtained from Active Directory and forwarded by the client to the server to authenticate the user.</span></span> <span data-ttu-id="969fe-156">앱의 사용자가 아닌 호스트에 대 한 서비스 주체 이름 (SPN)을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-156">Register the Service Principal Name (SPN) for the host, not the user of the app.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

## <a name="enable-windows-authentication-with-weblistener"></a><span data-ttu-id="969fe-157">WebListener 사용 하 여 Windows 인증을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="969fe-157">Enable Windows Authentication with WebListener</span></span>

<span data-ttu-id="969fe-158">Kestrel은 Windows 인증을 지원 하지 않지만 사용할 수 있습니다 [WebListener](xref:fundamentals/servers/weblistener) Windows에서 자체 호스팅된 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-158">Although Kestrel doesn't support Windows Authentication, you can use [WebListener](xref:fundamentals/servers/weblistener) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="969fe-159">다음 예제에서는 Windows 인증을 사용 하 여 WebListener를 사용 하는 앱의 웹 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-159">The following example configures the app's web host to use WebListener with Windows Authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program1x.cs?highlight=6-11)]

> [!NOTE]
> <span data-ttu-id="969fe-160">Kerberos 인증 프로토콜을 사용 하 여 커널 모드 인증에 WebListener 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-160">WebListener delegates to kernel mode authentication with the Kerberos authentication protocol.</span></span> <span data-ttu-id="969fe-161">Kerberos 및 WebListener를 사용 하 여 사용자 모드 인증이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-161">User mode authentication isn't supported with Kerberos and WebListener.</span></span> <span data-ttu-id="969fe-162">컴퓨터 계정이 Active Directory에서 가져온 Kerberos 토큰/티켓의 암호를 해독 하는 데 사용 하 고 사용자를 인증 하는 서버에 클라이언트에서 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-162">The machine account must be used to decrypt the Kerberos token/ticket that's obtained from Active Directory and forwarded by the client to the server to authenticate the user.</span></span> <span data-ttu-id="969fe-163">앱의 사용자가 아닌 호스트에 대 한 서비스 주체 이름 (SPN)을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-163">Register the Service Principal Name (SPN) for the host, not the user of the app.</span></span>

::: moniker-end

## <a name="work-with-windows-authentication"></a><span data-ttu-id="969fe-164">Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="969fe-164">Work with Windows Authentication</span></span>

<span data-ttu-id="969fe-165">익명 액세스 구성 상태는 방식을 결정 합니다 `[Authorize]` 및 `[AllowAnonymous]` 특성은 앱에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-165">The configuration state of anonymous access determines the way in which the `[Authorize]` and `[AllowAnonymous]` attributes are used in the app.</span></span> <span data-ttu-id="969fe-166">다음 두 섹션에는 익명 액세스는 허용 되지 않는 및 허용 된 구성 상태를 처리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-166">The following two sections explain how to handle the disallowed and allowed configuration states of anonymous access.</span></span>

### <a name="disallow-anonymous-access"></a><span data-ttu-id="969fe-167">익명 액세스 허용 안 함</span><span class="sxs-lookup"><span data-stu-id="969fe-167">Disallow anonymous access</span></span>

<span data-ttu-id="969fe-168">Windows 인증을 사용 하 고 익명 액세스가 비활성화 되어는 `[Authorize]` 고 `[AllowAnonymous]` 특성은 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-168">When Windows Authentication is enabled and anonymous access is disabled, the `[Authorize]` and `[AllowAnonymous]` attributes have no effect.</span></span> <span data-ttu-id="969fe-169">IIS 사이트 (또는 HTTP.sys 또는 WebListener 서버)을 익명 액세스를 허용 하지 않도록 구성 된 경우 요청에 하지 앱에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-169">If the IIS site (or HTTP.sys or WebListener server) is configured to disallow anonymous access, the request never reaches your app.</span></span> <span data-ttu-id="969fe-170">이러한 이유로 `[AllowAnonymous]` 특성 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-170">For this reason, the `[AllowAnonymous]` attribute isn't applicable.</span></span>

### <a name="allow-anonymous-access"></a><span data-ttu-id="969fe-171">익명 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="969fe-171">Allow anonymous access</span></span>

<span data-ttu-id="969fe-172">Windows 인증 및 익명 액세스를 모두 설정 된 경우 사용 합니다 `[Authorize]` 및 `[AllowAnonymous]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-172">When both Windows Authentication and anonymous access are enabled, use the `[Authorize]` and `[AllowAnonymous]` attributes.</span></span> <span data-ttu-id="969fe-173">`[Authorize]` 특성을 사용 하면 Windows 인증 필요 실제로 앱의 부분을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-173">The `[Authorize]` attribute allows you to secure pieces of the app which truly do require Windows Authentication.</span></span> <span data-ttu-id="969fe-174">합니다 `[AllowAnonymous]` 재정의 특성 `[Authorize]` 특성 익명 액세스를 허용 하는 앱 내에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-174">The `[AllowAnonymous]` attribute overrides `[Authorize]` attribute usage within apps which allow anonymous access.</span></span> <span data-ttu-id="969fe-175">참조 [단순 권한 부여](xref:security/authorization/simple) 자세한 특성 사용.</span><span class="sxs-lookup"><span data-stu-id="969fe-175">See [Simple Authorization](xref:security/authorization/simple) for attribute usage details.</span></span>

<span data-ttu-id="969fe-176">ASP.NET Core에서 2.x의 경우는 `[Authorize]` 특성 추가 구성이 필요 *Startup.cs* Windows 인증에 대 한 익명 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-176">In ASP.NET Core 2.x, the `[Authorize]` attribute requires additional configuration in *Startup.cs* to challenge anonymous requests for Windows Authentication.</span></span> <span data-ttu-id="969fe-177">권장된 구성에 사용 중인 웹 서버에 따라 약간씩 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-177">The recommended configuration varies slightly based on the web server being used.</span></span>

> [!NOTE]
> <span data-ttu-id="969fe-178">기본적으로 권한 부여를 페이지에 액세스할 수 없는 사용자는 빈 HTTP 403 응답으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-178">By default, users who lack authorization to access a page are presented with an empty HTTP 403 response.</span></span> <span data-ttu-id="969fe-179">합니다 [StatusCodePages 미들웨어](xref:fundamentals/error-handling#configuring-status-code-pages) "액세스 거부" 더 나은 환경을 제공 하기 위해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-179">The [StatusCodePages middleware](xref:fundamentals/error-handling#configuring-status-code-pages) can be configured to provide users with a better "Access Denied" experience.</span></span>

#### <a name="iis"></a><span data-ttu-id="969fe-180">IIS</span><span class="sxs-lookup"><span data-stu-id="969fe-180">IIS</span></span>

<span data-ttu-id="969fe-181">IIS를 사용 하는 경우 다음을 추가 하 여 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="969fe-181">If using IIS, add the following to the `ConfigureServices` method:</span></span>

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a><span data-ttu-id="969fe-182">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="969fe-182">HTTP.sys</span></span>

<span data-ttu-id="969fe-183">HTTP.sys를 사용 하는 경우 다음을 추가 하 여 `ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="969fe-183">If using HTTP.sys, add the following to the `ConfigureServices` method:</span></span>

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a><span data-ttu-id="969fe-184">가장</span><span class="sxs-lookup"><span data-stu-id="969fe-184">Impersonation</span></span>

<span data-ttu-id="969fe-185">Asp.net 가장을 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-185">ASP.NET Core doesn't implement impersonation.</span></span> <span data-ttu-id="969fe-186">앱 풀 또는 프로세스 id를 사용 하 여 모든 요청에 대해 응용 프로그램 id를 사용 하 여 앱이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-186">Apps run with the application identity for all requests, using app pool or process identity.</span></span> <span data-ttu-id="969fe-187">사용 하 여 명시적으로 사용자를 대신 하 여 작업을 수행 해야 할 경우 `WindowsIdentity.RunImpersonated`합니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-187">If you need to explicitly perform an action on behalf of a user, use `WindowsIdentity.RunImpersonated`.</span></span> <span data-ttu-id="969fe-188">이 컨텍스트에서 단일 작업을 실행 하 고 컨텍스트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-188">Run a single action in this context and then close the context.</span></span>

[!code-csharp[](windowsauth/sample/Startup.cs?name=snippet_Impersonate&highlight=10-18)]

<span data-ttu-id="969fe-189">`RunImpersonated` 비동기 작업을 지원 하지 않으며 복잡 한 시나리오에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-189">Note that `RunImpersonated` doesn't support asynchronous operations and shouldn't be used for complex scenarios.</span></span> <span data-ttu-id="969fe-190">예를 들어 전체 요청 또는 미들웨어 체인 래핑 지원 없거나 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="969fe-190">For example, wrapping entire requests or middleware chains isn't supported or recommended.</span></span>
