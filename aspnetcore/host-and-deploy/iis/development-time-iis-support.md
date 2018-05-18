---
title: ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원
author: shirhatti
description: Windows Server에서 IIS 뒤에서 실행 하는 경우 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원이 검색 합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: 0bf4585d44e61c5e7e5b89ce9d8dfdfa10d5460e
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="4cadb-103">ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원</span><span class="sxs-lookup"><span data-stu-id="4cadb-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="4cadb-104">여 [Sourabh Shirhatti](https://twitter.com/sshirhatti) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="4cadb-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="4cadb-105">이 문서에서는 설명 [Visual Studio](https://www.visualstudio.com/vs/) Windows 서버에서 IIS 뒤에서 실행 되는 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="4cadb-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="4cadb-106">이 항목에서는이 기능을 사용 하도록 설정 하 고 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cadb-107">전제 조건</span><span class="sxs-lookup"><span data-stu-id="4cadb-107">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a><span data-ttu-id="4cadb-108">IIS 활성화</span><span class="sxs-lookup"><span data-stu-id="4cadb-108">Enable IIS</span></span>

1. <span data-ttu-id="4cadb-109">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-109">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="4cadb-110">선택 된 **인터넷 정보 서비스** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-110">Select the **Internet Information Services** check box.</span></span>

![Windows 기능 보여 주는 인터넷 정보 서비스 확인란을 선택한 IIS 기능 중 일부는 사용할 수 있음을 나타내는 검은색 사각형 (하지: 확인 표시)으로](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="4cadb-112">IIS 설치는 시스템 다시 시작을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-112">The IIS installation may require a system restart.</span></span>

## <a name="configure-iis"></a><span data-ttu-id="4cadb-113">IIS 구성</span><span class="sxs-lookup"><span data-stu-id="4cadb-113">Configure IIS</span></span>

<span data-ttu-id="4cadb-114">IIS 웹 사이트를 다음으로 구성 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-114">IIS must have a website configured with the following:</span></span>

* <span data-ttu-id="4cadb-115">응용 프로그램의 실행 프로필 URL 호스트 이름과 일치 하는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-115">A host name that matches the app's launch profile URL host name.</span></span>
* <span data-ttu-id="4cadb-116">할당 된 인증서로 포트 443에 대 한 바인딩입니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-116">Binding for port 443 with an assigned certificate.</span></span>

<span data-ttu-id="4cadb-117">예를 들어는 **호스트 이름** 에서 추가 된 웹 사이트 ("실행 프로필은 또한 localhost" 사용이 항목의 뒷부분에 나오는) "localhost"으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-117">For example, the **Host name** for an added website is set to "localhost" (the launch profile will also use "localhost" later in this topic).</span></span> <span data-ttu-id="4cadb-118">포트는 "443" (HTTPS)로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-118">The port is set to "443" (HTTPS).</span></span> <span data-ttu-id="4cadb-119">**IIS Express 개발 인증서** works는 웹 사이트 이지만 유효한 모든 인증서에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-119">The **IIS Express Development Certificate** is assigned to the website, but any valid certificate works:</span></span>

![할당 된 인증서로 포트 443에서 localhost에 대 한 바인딩 집합을 표시 하는 IIS에서 웹 사이트 창을 추가 합니다.](development-time-iis-support/_static/add-website-window.png)

<span data-ttu-id="4cadb-121">IIS 설치 된 이미는 **기본 웹 사이트** 응용 프로그램의 실행 프로필 URL 호스트 이름과 일치 하는 호스트 이름의:</span><span class="sxs-lookup"><span data-stu-id="4cadb-121">If the IIS installation already has a **Default Web Site** with a host name that matches the app's launch profile URL host name:</span></span>

* <span data-ttu-id="4cadb-122">포트 443 (HTTPS)에 대 한 포트 바인딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-122">Add a port binding for port 443 (HTTPS).</span></span>
* <span data-ttu-id="4cadb-123">유효한 인증서를 웹 사이트에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-123">Assign a valid certificate to the website.</span></span>

## <a name="enable-development-time-iis-support-in-visual-studio"></a><span data-ttu-id="4cadb-124">Visual Studio에서 개발 시 IIS 지원을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4cadb-124">Enable development-time IIS support in Visual Studio</span></span>

1. <span data-ttu-id="4cadb-125">Visual Studio 설치 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-125">Launch the Visual Studio installer.</span></span>
1. <span data-ttu-id="4cadb-126">선택 된 **IIS 지원 개발 시간** 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-126">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="4cadb-127">구성 요소에 옵션으로 나열 됩니다는 **요약** 패널에 대 한는 **ASP.NET 및 웹 개발** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-127">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="4cadb-128">구성 요소 설치는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module), 하는 역방향 프록시 구성에서 ASP.NET Core IIS 뒤에 있는 앱을 실행 하는 데 필요한 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-128">The component installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps behind IIS in a reverse proxy configuration.</span></span>

![Visual Studio 기능 수정: 워크로드 탭이 선택되어 있습니다.](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="4cadb-132">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="4cadb-132">Configure the project</span></span>

### <a name="https-redirection"></a><span data-ttu-id="4cadb-133">HTTPS 리디렉션</span><span class="sxs-lookup"><span data-stu-id="4cadb-133">HTTPS redirection</span></span>

<span data-ttu-id="4cadb-134">새 프로젝트에 대 한 확인란을 선택 **HTTPS에 대 한 구성** 에 **새 ASP.NET Core 웹 응용 프로그램** 창:</span><span class="sxs-lookup"><span data-stu-id="4cadb-134">For a new project, select the check box to **Configure for HTTPS** in the **New ASP.NET Core Web Application** window:</span></span>

![새 ASP.NET Core 웹 응용 프로그램 창 HTTPS 확인란을 선택에 대 한 구성입니다.](development-time-iis-support/_static/new-app.png)

<span data-ttu-id="4cadb-136">기존 프로젝트를 HTTPS 리디렉션 미들웨어에서 사용 하 여 `Startup.Configure` 호출 하 여는 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 확장 메서드:</span><span class="sxs-lookup"><span data-stu-id="4cadb-136">In an existing project, use HTTPS Redirection Middleware in `Startup.Configure` by calling the [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) extension method:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseStaticFiles();
    app.UseCookiePolicy();

    app.UseMvc();
}
```

### <a name="iis-launch-profile"></a><span data-ttu-id="4cadb-137">IIS 시작 프로필</span><span class="sxs-lookup"><span data-stu-id="4cadb-137">IIS launch profile</span></span>

<span data-ttu-id="4cadb-138">개발 시 IIS 지원을 추가 하려면 새 실행 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-138">Create a new launch profile to add development-time IIS support:</span></span>

1. <span data-ttu-id="4cadb-139">에 대 한 **프로필**, 선택는 **새로** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-139">For **Profile**, select the **New** button.</span></span> <span data-ttu-id="4cadb-140">팝업 창에서 프로필 "IIS" 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-140">Name the profile "IIS" in the popup window.</span></span> <span data-ttu-id="4cadb-141">선택 **확인** 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-141">Select **OK** to create the profile.</span></span>
1. <span data-ttu-id="4cadb-142">에 대 한는 **시작** 선택 설정을 **IIS** 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-142">For the **Launch** setting, select **IIS** from the list.</span></span>
1. <span data-ttu-id="4cadb-143">에 대 한 확인란을 선택 **실행 브라우저** 끝점 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-143">Select the check box for **Launch browser** and provide the endpoint URL.</span></span> <span data-ttu-id="4cadb-144">HTTPS 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-144">Use the HTTPS protocol.</span></span> <span data-ttu-id="4cadb-145">이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-145">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="4cadb-146">에 **환경 변수** 섹션에서는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-146">In the **Environment variables** section, select the **Add** button.</span></span> <span data-ttu-id="4cadb-147">키로 환경 변수를 제공 `ASPNETCORE_ENVIRONMENT` 값 `Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-147">Provide an environment variable with a key of `ASPNETCORE_ENVIRONMENT` and a value of `Development`.</span></span>
1. <span data-ttu-id="4cadb-148">에 **웹 서버 설정** 영역 설정에서 **앱 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-148">In the **Web Server Settings** area, set the **App URL**.</span></span> <span data-ttu-id="4cadb-149">이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-149">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="4cadb-150">프로필을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-150">Save the profile.</span></span>

![디버그 탭이 선택된 프로젝트 속성 창입니다.](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="4cadb-155">또는 실행 프로필을 수동으로 추가할는 [launchSettings.json](http://json.schemastore.org/launchsettings) 앱에서 파일:</span><span class="sxs-lookup"><span data-stu-id="4cadb-155">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iis": {
      "applicationUrl": "https://localhost/WebApplication1",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS": {
      "commandName": "IIS",
      "launchBrowser": true,
      "launchUrl": "https://localhost/WebApplication1",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

## <a name="run-the-project"></a><span data-ttu-id="4cadb-156">프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="4cadb-156">Run the project</span></span>

<span data-ttu-id="4cadb-157">VS UI에서 [실행] 단추를 설정 된 **IIS** 프로 파일링 하 고 앱을 시작 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-157">In the VS UI, set the Run button to the **IIS** profile and select the button to start the app:</span></span>

!["IIS" 프로 파일링 하도록 설정 하 고 VS 도구 모음에서 단추를 실행 합니다.](development-time-iis-support/_static/toolbar.png)

<span data-ttu-id="4cadb-159">관리자 권한으로 실행 되 고 있지 visual Studio를 다시 시작을 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-159">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="4cadb-160">메시지가 표시되면 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-160">If prompted, restart Visual Studio.</span></span>

<span data-ttu-id="4cadb-161">신뢰할 수 없는 개발 인증서를 사용 하는 경우 신뢰할 수 없는 인증서에 대 한 예외를 만들 수 있습니다 브라우저 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cadb-161">If an untrusted development certificate is used, the browser may require you to create an exception for the untrusted certificate.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4cadb-162">추가 자료</span><span class="sxs-lookup"><span data-stu-id="4cadb-162">Additional resources</span></span>

* [<span data-ttu-id="4cadb-163">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="4cadb-163">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="4cadb-164">ASP.NET Core 모듈 소개</span><span class="sxs-lookup"><span data-stu-id="4cadb-164">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="4cadb-165">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="4cadb-165">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="4cadb-166">HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="4cadb-166">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
