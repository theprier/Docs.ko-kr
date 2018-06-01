---
title: ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원
author: shirhatti
description: Windows Server에서 IIS를 통해 실행될 경우 ASP.NET Core 앱 디버그에 대한 지원을 확인해 보세요.
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
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34233081"
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="ec6e2-103">ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원</span><span class="sxs-lookup"><span data-stu-id="ec6e2-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="ec6e2-104">작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="ec6e2-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="ec6e2-105">이 문서에서는 Windows Server에서 IIS를 통해 실행되는 ASP.NET Core 앱을 디버그하기 위한 [Visual Studio](https://www.visualstudio.com/vs/) 지원에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="ec6e2-106">이 항목에서는 이 기능을 사용하도록 설정하고 프로젝트를 설정하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec6e2-107">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ec6e2-107">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a><span data-ttu-id="ec6e2-108">IIS 활성화</span><span class="sxs-lookup"><span data-stu-id="ec6e2-108">Enable IIS</span></span>

1. <span data-ttu-id="ec6e2-109">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-109">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="ec6e2-110">**인터넷 정보 서비스** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-110">Select the **Internet Information Services** check box.</span></span>

![인터넷 정보 서비스 확인란이 검은 사각형(확인 표시 아님)으로 표시되어 있고 IIS 기능 중 일부가 활성화되었음을 보여주는 Windows 기능](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="ec6e2-112">IIS를 설치하려면 시스템을 다시 시작해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-112">The IIS installation may require a system restart.</span></span>

## <a name="configure-iis"></a><span data-ttu-id="ec6e2-113">IIS 구성</span><span class="sxs-lookup"><span data-stu-id="ec6e2-113">Configure IIS</span></span>

<span data-ttu-id="ec6e2-114">IIS에서 웹 사이트는 다음과 같이 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-114">IIS must have a website configured with the following:</span></span>

* <span data-ttu-id="ec6e2-115">앱의 시작 프로필 URL 호스트 이름과 일치하는 호스트 이름.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-115">A host name that matches the app's launch profile URL host name.</span></span>
* <span data-ttu-id="ec6e2-116">할당된 인증서가 있는 포트 443에 대한 바인딩.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-116">Binding for port 443 with an assigned certificate.</span></span>

<span data-ttu-id="ec6e2-117">예를 들어 추가된 웹 사이트의 **호스트 이름**은 “localhost”로 설정됩니다(이 항목의 뒷부분에서 시작 프로필에도 “localhost”를 사용함).</span><span class="sxs-lookup"><span data-stu-id="ec6e2-117">For example, the **Host name** for an added website is set to "localhost" (the launch profile will also use "localhost" later in this topic).</span></span> <span data-ttu-id="ec6e2-118">포트가 “443”(HTTPS)으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-118">The port is set to "443" (HTTPS).</span></span> <span data-ttu-id="ec6e2-119">**IIS Express 개발 인증서**가 웹 사이트에 할당되지만 모든 유효한 인증서가 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-119">The **IIS Express Development Certificate** is assigned to the website, but any valid certificate works:</span></span>

![인증서가 할당된 포트 443에서 localhost에 대한 바인딩 집합을 표시하는 [웹 사이트] 창을 IIS에서 추가합니다.](development-time-iis-support/_static/add-website-window.png)

<span data-ttu-id="ec6e2-121">IIS 설치에 앱의 시작 프로필 URL 호스트 이름과 일치하는 호스트 이름을 가진 **기본 웹 사이트**가 이미 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="ec6e2-121">If the IIS installation already has a **Default Web Site** with a host name that matches the app's launch profile URL host name:</span></span>

* <span data-ttu-id="ec6e2-122">포트 443(HTTPS)에 포트 바인딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-122">Add a port binding for port 443 (HTTPS).</span></span>
* <span data-ttu-id="ec6e2-123">웹 사이트에 유효한 인증서를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-123">Assign a valid certificate to the website.</span></span>

## <a name="enable-development-time-iis-support-in-visual-studio"></a><span data-ttu-id="ec6e2-124">Visual Studio에서 개발 시간 IIS 지원 사용</span><span class="sxs-lookup"><span data-stu-id="ec6e2-124">Enable development-time IIS support in Visual Studio</span></span>

1. <span data-ttu-id="ec6e2-125">Visual Studio 설치 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-125">Launch the Visual Studio installer.</span></span>
1. <span data-ttu-id="ec6e2-126">**개발 시간 IIS 지원** 구성 요소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-126">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="ec6e2-127">이 구성 요소는 **ASP.NET 및 웹 개발** 워크로드에 대한 **요약** 패널에 선택 사항으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-127">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="ec6e2-128">구성 요소는 역방향 프록시 구성에서 IIS를 통해 ASP.NET Core 앱을 실행하는 데 필요한 네이티브 IIS 모듈인 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-128">The component installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps behind IIS in a reverse proxy configuration.</span></span>

![Visual Studio 기능 수정: 워크로드 탭이 선택되어 있습니다.](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="ec6e2-132">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="ec6e2-132">Configure the project</span></span>

### <a name="https-redirection"></a><span data-ttu-id="ec6e2-133">HTTPS 리디렉션</span><span class="sxs-lookup"><span data-stu-id="ec6e2-133">HTTPS redirection</span></span>

<span data-ttu-id="ec6e2-134">새 프로젝트의 경우 **새 ASP.NET Core 웹 응용 프로그램** 창에서 **HTTPS에 대한 구성** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-134">For a new project, select the check box to **Configure for HTTPS** in the **New ASP.NET Core Web Application** window:</span></span>

![HTTPS에 대한 구성 확인란이 선택된 새 ASP.NET Core 웹 응용 프로그램 창.](development-time-iis-support/_static/new-app.png)

<span data-ttu-id="ec6e2-136">기존 프로젝트에서는 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 확장 메서드를 호출하여 `Startup.Configure`에서 HTTPS 리디렉션 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-136">In an existing project, use HTTPS Redirection Middleware in `Startup.Configure` by calling the [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) extension method:</span></span>

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

### <a name="iis-launch-profile"></a><span data-ttu-id="ec6e2-137">IIS 시작 프로필</span><span class="sxs-lookup"><span data-stu-id="ec6e2-137">IIS launch profile</span></span>

<span data-ttu-id="ec6e2-138">새 시작 프로필을 만들어 개발 시간 IIS 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-138">Create a new launch profile to add development-time IIS support:</span></span>

1. <span data-ttu-id="ec6e2-139">**프로필**의 경우 **새로 만들기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-139">For **Profile**, select the **New** button.</span></span> <span data-ttu-id="ec6e2-140">팝업 창에서 프로필 이름을 “IIS”로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-140">Name the profile "IIS" in the popup window.</span></span> <span data-ttu-id="ec6e2-141">**확인**을 선택하여 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-141">Select **OK** to create the profile.</span></span>
1. <span data-ttu-id="ec6e2-142">**시작** 설정의 경우 목록에서 **IIS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-142">For the **Launch** setting, select **IIS** from the list.</span></span>
1. <span data-ttu-id="ec6e2-143">**브라우저 시작** 확인란을 선택하고 끝점 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-143">Select the check box for **Launch browser** and provide the endpoint URL.</span></span> <span data-ttu-id="ec6e2-144">HTTPS 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-144">Use the HTTPS protocol.</span></span> <span data-ttu-id="ec6e2-145">이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-145">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="ec6e2-146">**환경 변수** 섹션에서 **추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-146">In the **Environment variables** section, select the **Add** button.</span></span> <span data-ttu-id="ec6e2-147">`ASPNETCORE_ENVIRONMENT` 키 및 `Development` 값을 사용하여 환경 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-147">Provide an environment variable with a key of `ASPNETCORE_ENVIRONMENT` and a value of `Development`.</span></span>
1. <span data-ttu-id="ec6e2-148">**웹 서버 설정** 영역에서 **앱 URL**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-148">In the **Web Server Settings** area, set the **App URL**.</span></span> <span data-ttu-id="ec6e2-149">이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-149">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="ec6e2-150">프로필을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-150">Save the profile.</span></span>

![디버그 탭이 선택된 프로젝트 속성 창입니다.](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="ec6e2-155">또는 앱의 [launchSettings.json](http://json.schemastore.org/launchsettings) 파일에 시작 프로필을 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-155">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

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

## <a name="run-the-project"></a><span data-ttu-id="ec6e2-156">프로젝트 실행</span><span class="sxs-lookup"><span data-stu-id="ec6e2-156">Run the project</span></span>

<span data-ttu-id="ec6e2-157">VS UI에서 [실행] 단추를 **IIS** 프로필로 설정하고 단추를 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-157">In the VS UI, set the Run button to the **IIS** profile and select the button to start the app:</span></span>

![“IIS” 프로필로 설정된 VS 도구 모음의 실행 단추.](development-time-iis-support/_static/toolbar.png)

<span data-ttu-id="ec6e2-159">관리자로 실행하고 있지 않으면 Visual Studio에서 다시 시작하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-159">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="ec6e2-160">메시지가 표시되면 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-160">If prompted, restart Visual Studio.</span></span>

<span data-ttu-id="ec6e2-161">신뢰할 수 없는 개발 인증서를 사용하는 경우 브라우저에서 신뢰할 수 없는 인증서에 대한 예외를 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec6e2-161">If an untrusted development certificate is used, the browser may require you to create an exception for the untrusted certificate.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec6e2-162">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ec6e2-162">Additional resources</span></span>

* [<span data-ttu-id="ec6e2-163">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="ec6e2-163">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="ec6e2-164">ASP.NET Core 모듈 소개</span><span class="sxs-lookup"><span data-stu-id="ec6e2-164">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="ec6e2-165">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="ec6e2-165">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="ec6e2-166">HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="ec6e2-166">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
