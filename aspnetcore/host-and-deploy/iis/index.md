---
title: "IIS가 있는 Windows에서 ASP.NET Core 호스팅"
author: guardrex
description: "Windows Server IIS(인터넷 정보 서비스)에서 ASP.NET Core 앱을 호스팅하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/index
ms.openlocfilehash: 1df438af2394f41b686413cd1ce5ad73a9416ec5
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="host-aspnet-core-on-windows-with-iis"></a><span data-ttu-id="a586e-103">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="a586e-103">Host ASP.NET Core on Windows with IIS</span></span>

<span data-ttu-id="a586e-104">이 문서의 작성자: [Luke Latham](https://github.com/guardrex) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a586e-104">By [Luke Latham](https://github.com/guardrex) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="a586e-105">지원되는 운영 체제</span><span class="sxs-lookup"><span data-stu-id="a586e-105">Supported operating systems</span></span>

<span data-ttu-id="a586e-106">지원되는 운영 체제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-106">The following operating systems are supported:</span></span>

* <span data-ttu-id="a586e-107">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="a586e-107">Windows 7 and newer</span></span>
* <span data-ttu-id="a586e-108">Windows Server 2008 R2 이상&#8224;</span><span class="sxs-lookup"><span data-stu-id="a586e-108">Windows Server 2008 R2 and newer&#8224;</span></span>

<span data-ttu-id="a586e-109">&#8224;개념적으로 이 문서에서 설명하는 IIS 구성은 Nano Server IIS에서 ASP.NET Core 앱을 호스팅하는 데에도 적용되지만, 구체적인 지침은 [Nano Server의 ASP.NET Core 및 IIS](xref:tutorials/nano-server)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-109">&#8224;Conceptually, the IIS configuration described in this document also applies to hosting ASP.NET Core apps on Nano Server IIS, but refer to [ASP.NET Core with IIS on Nano Server](xref:tutorials/nano-server) for specific instructions.</span></span>

<span data-ttu-id="a586e-110">[HTTP.sys 서버](xref:fundamentals/servers/httpsys)(이전의 [WebListener](xref:fundamentals/servers/weblistener))는 IIS가 있는 역방향 프록시 구성에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-110">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)) won't work in a reverse proxy configuration with IIS.</span></span> <span data-ttu-id="a586e-111">[Kestrel 서버](xref:fundamentals/servers/kestrel)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-111">Use the [Kestrel server](xref:fundamentals/servers/kestrel).</span></span>

## <a name="iis-configuration"></a><span data-ttu-id="a586e-112">IIS 구성</span><span class="sxs-lookup"><span data-stu-id="a586e-112">IIS configuration</span></span>

<span data-ttu-id="a586e-113">**웹 서버(IIS)** 역할을 사용하도록 설정하고 역할 서비스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-113">Enable the **Web Server (IIS)** role and establish role services.</span></span>

### <a name="windows-desktop-operating-systems"></a><span data-ttu-id="a586e-114">Windows 데스크톱 운영 체제</span><span class="sxs-lookup"><span data-stu-id="a586e-114">Windows desktop operating systems</span></span>

<span data-ttu-id="a586e-115">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-115">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="a586e-116">**인터넷 정보 서비스** 및 **웹 관리 도구** 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-116">Open the group for **Internet Information Services** and **Web Management Tools**.</span></span> <span data-ttu-id="a586e-117">**IIS 관리 콘솔** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-117">Check the box for **IIS Management Console**.</span></span> <span data-ttu-id="a586e-118">**World Wide Web 서비스** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-118">Check the box for **World Wide Web Services**.</span></span> <span data-ttu-id="a586e-119">**World Wide Web 서비스**의 기본 기능을 그대로 사용하거나 IIS 기능을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-119">Accept the default features for **World Wide Web Services** or customize the IIS features.</span></span>

![Windows 기능에서 선택된 IIS 관리 콘솔 및 World Wide Web 서비스](index/_static/windows-features-win10.png)

### <a name="windows-server-operating-systems"></a><span data-ttu-id="a586e-121">Windows Server 운영 체제</span><span class="sxs-lookup"><span data-stu-id="a586e-121">Windows Server operating systems</span></span>

<span data-ttu-id="a586e-122">서버 운영 체제의 경우 **관리** 메뉴 또는 **서버 관리자**의 링크를 통해 **역할 및 기능 추가** 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-122">For server operating systems, use the **Add Roles and Features** wizard via the **Manage** menu or the link in **Server Manager**.</span></span> <span data-ttu-id="a586e-123">**서버 역할** 단계에서 **웹 서버(IIS)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-123">On the **Server Roles** step, check the box for **Web Server (IIS)**.</span></span>

![서버 역할 선택 단계에서 선택된 웹 서버 IIS 역할](index/_static/server-roles-ws2016.png)

<span data-ttu-id="a586e-125">**역할 서비스** 단계에서 원하는 IIS 역할 서비스를 선택하거나 제공된 기본 역할 서비스를 받아들입니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-125">On the **Role services** step, select the IIS role services desired or accept the default role services provided.</span></span>

![역할 서비스 선택 단계에서 선택된 기본 역할 서비스](index/_static/role-services-ws2016.png)

<span data-ttu-id="a586e-127">**확인** 단계를 진행하여 웹 서버 역할 및 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-127">Proceed through the **Confirmation** step to install the web server role and services.</span></span> <span data-ttu-id="a586e-128">웹 서버(IIS) 역할을 설치한 후에 서버/IIS를 다시 시작할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-128">A server/IIS restart isn't required after installing the Web Server (IIS) role.</span></span>

## <a name="install-the-net-core-windows-server-hosting-bundle"></a><span data-ttu-id="a586e-129">.NET Core Windows Server 호스팅 번들 설치</span><span class="sxs-lookup"><span data-stu-id="a586e-129">Install the .NET Core Windows Server Hosting bundle</span></span>

1. <span data-ttu-id="a586e-130">호스팅 시스템에 [.NET Core Windows Server 호스팅 번들](https://aka.ms/dotnetcore-2-windowshosting)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-130">Install the [.NET Core Windows Server Hosting bundle](https://aka.ms/dotnetcore-2-windowshosting) on the hosting system.</span></span> <span data-ttu-id="a586e-131">번들은 .NET Core 런타임, .NET Core 라이브러리 및 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-131">The bundle installs the .NET Core Runtime, .NET Core Library, and the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="a586e-132">이 모듈은 IIS와 Kestrel 서버 간에 역방향 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-132">The module creates the reverse proxy between IIS and the Kestrel server.</span></span> <span data-ttu-id="a586e-133">시스템이 인터넷에 연결되지 않은 경우 [Microsoft Visual C++ 2015 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=53840)를 설치한 후에 .NET Core Windows Server 호스팅 번들을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-133">If the system doesn't have an Internet connection, obtain and install the [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840) before installing the .NET Core Windows Server Hosting bundle.</span></span>

2. <span data-ttu-id="a586e-134">시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 시스템 PATH에 대한 변경 내용을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-134">Restart the system or execute **net stop was /y** followed by **net start w3svc** from a command prompt to pick up a change to the system PATH.</span></span>

> [!NOTE]
> <span data-ttu-id="a586e-135">IIS 공유 구성에 대한 자세한 내용은 [IIS 공유 구성을 사용하는 ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-135">For information on IIS Shared Configuration, see [ASP.NET Core Module with IIS Shared Configuration](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration).</span></span>

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a><span data-ttu-id="a586e-136">Visual Studio을 사용하여 게시할 때 웹 배포 설치</span><span class="sxs-lookup"><span data-stu-id="a586e-136">Install Web Deploy when publishing with Visual Studio</span></span>

<span data-ttu-id="a586e-137">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하여 앱을 서버에 배포하는 경우 최신 버전의 웹 배포를 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-137">When deploying apps to servers with [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy), install the latest version of Web Deploy on the server.</span></span> <span data-ttu-id="a586e-138">웹 배포를 설치하려면 [WebPI(웹 플랫폼 설치 관리자)](https://www.microsoft.com/web/downloads/platform.aspx)를 사용하거나 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=43717)에서 직접 설치 관리자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-138">To install Web Deploy, use the [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) or obtain an installer directly from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43717).</span></span> <span data-ttu-id="a586e-139">WebPI를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-139">The preferred method is to use WebPI.</span></span> <span data-ttu-id="a586e-140">WebPI는 호스팅 공급자에 대한 독립 실행형 설치 및 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-140">WebPI offers a standalone setup and a configuration for hosting providers.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="a586e-141">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a586e-141">Application configuration</span></span>

### <a name="enabling-the-iisintegration-components"></a><span data-ttu-id="a586e-142">IISIntegration 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="a586e-142">Enabling the IISIntegration components</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a586e-143">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a586e-143">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="a586e-144">일반적인 *Program.cs*는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출하여 호스트 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-144">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to begin setting up a host.</span></span> <span data-ttu-id="a586e-145">`CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-145">`CreateDefaultBuilder` configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and enables IIS integration by configuring the base path and port for the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module):</span></span>

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a586e-146">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a586e-146">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="a586e-147">[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) 패키지에 대한 종속성을 앱의 종속성에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-147">Include a dependency on the [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) package in the app's dependencies.</span></span> <span data-ttu-id="a586e-148">*UseIISIntegration* 확장 메서드를 *WebHostBuilder*에 추가하여 IIS 통합 미들웨어를 앱에 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-148">Incorporate IIS Integration middleware into the app by adding the *UseIISIntegration* extension method to *WebHostBuilder*:</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<span data-ttu-id="a586e-149">`UseKestrel` 및 `UseIISIntegration`이 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-149">Both `UseKestrel` and `UseIISIntegration` are required.</span></span> <span data-ttu-id="a586e-150">`UseIISIntegration`을 호출하는 코드는 코드 이식성에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-150">Code calling `UseIISIntegration` doesn't affect code portability.</span></span> <span data-ttu-id="a586e-151">앱이 IIS 배후에서 실행되지 않는 경우(예를 들어 앱이 Kestrel에서 바로 실행되는 경우) `UseIISIntegration`은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-151">If the app isn't run behind IIS (for example, the app is run directly on Kestrel), `UseIISIntegration` no-ops.</span></span>

---

<span data-ttu-id="a586e-152">호스팅에 대한 자세한 내용은 [ASP.NET Core에서 호스팅](xref:fundamentals/hosting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-152">For more information on hosting, see [Hosting in ASP.NET Core](xref:fundamentals/hosting).</span></span>

### <a name="iis-options"></a><span data-ttu-id="a586e-153">IIS 옵션</span><span class="sxs-lookup"><span data-stu-id="a586e-153">IIS options</span></span>

<span data-ttu-id="a586e-154">IIS 옵션을 구성하려면 `IISOptions`에 대한 서비스 구성을 `ConfigureServices`에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-154">To configure IIS options, include a service configuration for `IISOptions` in `ConfigureServices`:</span></span>

```csharp
services.Configure<IISOptions>(options => 
{
    ...
});
```

| <span data-ttu-id="a586e-155">옵션</span><span class="sxs-lookup"><span data-stu-id="a586e-155">Option</span></span>                         | <span data-ttu-id="a586e-156">기본</span><span class="sxs-lookup"><span data-stu-id="a586e-156">Default</span></span> | <span data-ttu-id="a586e-157">설정</span><span class="sxs-lookup"><span data-stu-id="a586e-157">Setting</span></span> |
| ------------------------------ | ------- | ------- |
| `AutomaticAuthentication`      | `true`  | <span data-ttu-id="a586e-158">`true`면 인증 미들웨어가 `HttpContext.User`를 설정하고 제네릭 과제에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-158">If `true`, the authentication middleware sets the `HttpContext.User` and responds to generic challenges.</span></span> <span data-ttu-id="a586e-159">`false`면 인증 미들웨어가 ID(`HttpContext.User`)만 제공하고, `AuthenticationScheme`에 의해 명시적으로 요청될 때 과제에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-159">If `false`, the authentication middleware only provides an identity (`HttpContext.User`) and responds to challenges when explicitly requested by the `AuthenticationScheme`.</span></span> <span data-ttu-id="a586e-160">IIS에서 Windows 인증은 `AutomaticAuthentication`이 작동하기 위해 사용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-160">Windows Authentication must be enabled in IIS for `AutomaticAuthentication` to function.</span></span> |
| `AuthenticationDisplayName`    | `null`  | <span data-ttu-id="a586e-161">로그인 페이지에서 사용자에게 나타나는 표시 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-161">Sets the display name shown to users on login pages.</span></span> |
| `ForwardClientCertificate`     | `true`  | <span data-ttu-id="a586e-162">`true`면서 `MS-ASPNETCORE-CLIENTCERT` 요청 헤더가 있는 경우 `HttpContext.Connection.ClientCertificate`가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-162">If `true` and the `MS-ASPNETCORE-CLIENTCERT` request header is present, the `HttpContext.Connection.ClientCertificate` is populated.</span></span> |

### <a name="webconfig"></a><span data-ttu-id="a586e-163">web.config</span><span class="sxs-lookup"><span data-stu-id="a586e-163">web.config</span></span>

<span data-ttu-id="a586e-164">*web.config* 파일의 기본 목적은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-164">The *web.config* file's primary purpose is to configure the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="a586e-165">선택적으로 추가 IIS 구성 설정을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-165">It may optionally provide additional IIS configuration settings.</span></span> <span data-ttu-id="a586e-166">*web.config*의 생성, 변환 및 게시는 .NET Core Web SDK(`Microsoft.NET.Sdk.Web`)에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-166">Creating, transforming, and publishing *web.config* is handled by the .NET Core Web SDK (`Microsoft.NET.Sdk.Web`).</span></span> <span data-ttu-id="a586e-167">SDK는 프로젝트 파일(`<Project Sdk="Microsoft.NET.Sdk.Web">`)의 맨 위에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-167">The SDK is set  at the top of the project file, `<Project Sdk="Microsoft.NET.Sdk.Web">`.</span></span> <span data-ttu-id="a586e-168">SDK가 *web.config* 파일을 변환하지 못하게 하려면 프로젝트 파일에 `true` 설정을 갖는 **\<IsTransformWebConfigDisabled>** 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-168">To prevent the SDK from transforming the *web.config* file, add the **\<IsTransformWebConfigDisabled>** property to the project file with a setting of `true`:</span></span>

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="a586e-169">프로젝트에 *web.config* 파일이 있는 경우, 올바른 *processPath* 및 *arguments*를 통해 변환되어 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성하고 [게시된 출력](xref:host-and-deploy/directory-structure)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-169">If a *web.config* file is in the project, it's transformed with the correct *processPath* and *arguments* to configure the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and moved to [published output](xref:host-and-deploy/directory-structure).</span></span> <span data-ttu-id="a586e-170">변환은 이 파일의 IIS 구성 설정을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-170">The transformation doesn't modify IIS configuration settings in the file.</span></span>

### <a name="webconfig-location"></a><span data-ttu-id="a586e-171">web.config 위치</span><span class="sxs-lookup"><span data-stu-id="a586e-171">web.config location</span></span>

<span data-ttu-id="a586e-172">.NET Core 앱은 IIS와 Kestrel 서버 간의 역방향 프록시를 통해 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-172">.NET Core apps are hosted via a reverse proxy between IIS and the Kestrel server.</span></span> <span data-ttu-id="a586e-173">역방향 프록시를 만들려면 IIS에 제공되는 웹 사이트 실제 경로인 배포된 앱의 콘텐츠 루트 경로(일반적으로 앱 기본 경로)에 *web.config* 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-173">In order to create the reverse proxy, the *web.config* file must be present at the content root path (typically the app base path) of the deployed app, which is the website physical path provided to IIS.</span></span> <span data-ttu-id="a586e-174">웹 배포를 사용하여 여러 앱을 게시하도록 설정하려면 앱의 루트에 *web.config* 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-174">The *web.config* file is required at the root of the app to enable the publishing of multiple apps using Web Deploy.</span></span>

<span data-ttu-id="a586e-175">중요한 파일은 *\<assembly_name>.runtimeconfig.json*, *\<assembly_name>.xml*(XML 문서 주석) 및 *\<assembly_name>.deps.json*과 같은 하위 폴더를 포함한 앱의 실제 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-175">Sensitive files exist on the app's physical path, including subfolders, such as *\<assembly_name>.runtimeconfig.json*, *\<assembly_name>.xml* (XML Documentation comments), and *\<assembly_name>.deps.json*.</span></span> <span data-ttu-id="a586e-176">*web.config* 파일이 있고 사이트를 구성하는 경우 IIS는 이러한 중요한 파일이 제공되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-176">When the *web.config* file is present and configures the site, IIS prevents these sensitive files from being served.</span></span> <span data-ttu-id="a586e-177">**따라서 *web.config* 파일을 실수로 이름을 변경하거나 배포에서 제거하지 않아야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a586e-177">**Therefore, it's important that the *web.config* file isn't accidently renamed or removed from the deployment.**</span></span>

## <a name="create-the-iis-website"></a><span data-ttu-id="a586e-178">IIS 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="a586e-178">Create the IIS Website</span></span>

1. <span data-ttu-id="a586e-179">대상 IIS 시스템에서는 [디렉터리 구조](xref:host-and-deploy/directory-structure)에서 설명하는 앱의 게시된 폴더와 파일을 포함할 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-179">On the target IIS system, create a folder to contain the app's published folders and files, which are described in [Directory Structure](xref:host-and-deploy/directory-structure).</span></span>

2. <span data-ttu-id="a586e-180">폴더 내에서 *logs* 폴더를 만들어 stdout 로깅이 활성화될 때 stdout 로그를 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-180">Within the folder, create a *logs* folder to hold stdout logs when stdout logging is enabled.</span></span> <span data-ttu-id="a586e-181">앱이 페이로드에서 *logs* 폴더와 함께 배포되는 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-181">If the app is deployed with a *logs* folder in the payload, skip this step.</span></span> <span data-ttu-id="a586e-182">MSBuild에서 *logs* 폴더를 만드는 방법에 대한 지침은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-182">For instructions on how to make MSBuild create the *logs* folder, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>

3. <span data-ttu-id="a586e-183">**IIS 관리자**에서 새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-183">In **IIS Manager**, create a new website.</span></span> <span data-ttu-id="a586e-184">**사이트 이름**을 제공하고 **실제 경로**를 앱의 배포 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-184">Provide a **Site name** and set the **Physical path** to the app's deployment folder.</span></span> <span data-ttu-id="a586e-185">**바인딩** 구성을 제공하고 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-185">Provide the **Binding** configuration and create the website.</span></span>

4. <span data-ttu-id="a586e-186">응용 프로그램 풀을 **관리 코드 없음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-186">Set the application pool to **No Managed Code**.</span></span> <span data-ttu-id="a586e-187">ASP.NET Core는 별도의 프로세스에서 실행되며 런타임을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-187">ASP.NET Core runs in a separate process and manages the runtime.</span></span>

5. <span data-ttu-id="a586e-188">**웹 사이트 추가** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-188">Open the **Add Website** window.</span></span>

   ![[사이트] 상황에 맞는 메뉴에서 '웹 사이트 추가'를 선택합니다.](index/_static/add-website-context-menu-ws2016.png)

6. <span data-ttu-id="a586e-190">웹 사이트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-190">Configure the website.</span></span>

   ![[웹 사이트 추가] 단계에서 사이트 이름, 실제 경로 및 호스트 이름을 제공합니다.](index/_static/add-website-ws2016.png)

7. <span data-ttu-id="a586e-192">**응용 프로그램 풀** 패널에서 웹 사이트의 앱 풀을 마우스 오른쪽 단추로 클릭하고 팝업 메뉴에서 **기본 설정...**을 선택하여 **응용 프로그램 풀 편집** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-192">In the **Application Pools** panel, open the **Edit Application Pool** window by right-clicking on the website's app pool and selecting **Basic Settings...** from the popup menu.</span></span>

   ![[응용 프로그램 풀]의 상황에 맞는 메뉴에서 [기본 설정]을 선택합니다.](index/_static/apppools-basic-settings-ws2016.png)

8. <span data-ttu-id="a586e-194">**.NET CLR 버전**을 **관리 코드 없음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-194">Set the **.NET CLR version** to **No Managed Code**.</span></span>

   ![관리 코드 없음으로 설정된 .NET CLR 버전](index/_static/edit-apppool-ws2016.png)
     
    <span data-ttu-id="a586e-196">참고: **.NET CLR 버전**을 **관리 코드 없음**으로 설정하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-196">Note: Setting the **.NET CLR version** to **No Managed Code** is optional.</span></span> <span data-ttu-id="a586e-197">ASP.NET Core에서는 데스크톱 CLR을 로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-197">ASP.NET Core doesn't rely on loading the desktop CLR.</span></span>

9. <span data-ttu-id="a586e-198">프로세스 모델 ID에 적절한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-198">Confirm the process model identity has the proper permissions.</span></span>

   <span data-ttu-id="a586e-199">응용 프로그램 풀의 기본 ID(**프로세스 모델** > **ID**)가 **ApplicationPoolIdentity**에서 다른 ID로 변경되면, 새 ID에 앱의 폴더, 데이터베이스 및 기타 필요한 리소스에 액세스하는 데 필요한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-199">If the default identity of the app pool (**Process Model** > **Identity**) is changed from **ApplicationPoolIdentity** to another identity, verify that the new identity has the required permissions to access the app's folder, database, and other required resources.</span></span>
   
## <a name="deploy-the-app"></a><span data-ttu-id="a586e-200">앱 배포</span><span class="sxs-lookup"><span data-stu-id="a586e-200">Deploy the app</span></span>

<span data-ttu-id="a586e-201">대상 IIS 시스템에서 만든 폴더에 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-201">Deploy the app to the folder created on the target IIS system.</span></span> <span data-ttu-id="a586e-202">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 배포에 권장되는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-202">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) is the recommended mechanism for deployment.</span></span>

<span data-ttu-id="a586e-203">게시된 배포용 앱이 실행되고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-203">Confirm that the published app for deployment isn't running.</span></span> <span data-ttu-id="a586e-204">앱이 실행 중이면 *publish* 폴더의 파일이 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-204">Files in the *publish* folder are locked when the app is running.</span></span> <span data-ttu-id="a586e-205">잠긴 파일은 덮어쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-205">Locked files can't be overwritten.</span></span> <span data-ttu-id="a586e-206">배포에서 잠긴 파일을 해제하려면 응용 프로그램 풀을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-206">To release locked files in a deployment, stop the app pool:</span></span>

* <span data-ttu-id="a586e-207">서버의 IIS 관리자에서 수동으로 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-207">Manually in the IIS Manager on the server.</span></span>
* <span data-ttu-id="a586e-208">웹 배포를 사용하고 프로젝트 파일에서 `Microsoft.NET.Sdk.Web`을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-208">Using Web Deploy and referencing `Microsoft.NET.Sdk.Web` in the project file.</span></span> <span data-ttu-id="a586e-209">*app_offline.htm* 파일은 웹앱 디렉터리의 루트에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-209">An *app_offline.htm* file is placed at the root of the web app directory.</span></span> <span data-ttu-id="a586e-210">파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-210">When the file is present, the ASP.NET Core Module gracefully shuts down the app and serves the *app_offline.htm* file during the deployment.</span></span> <span data-ttu-id="a586e-211">자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#appofflinehtm)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-211">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#appofflinehtm).</span></span>
* <span data-ttu-id="a586e-212">PowerShell을 사용하여 응용 프로그램 풀을 중지하고 다시 시작합니다(PowerShell 5 이상 필요).</span><span class="sxs-lookup"><span data-stu-id="a586e-212">Use PowerShell to stop and restart the app pool (requires PowerShell 5 or later):</span></span>
  ```PowerShell
  $webAppPoolName = 'APP_POOL_NAME'

  # Stop the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
      Stop-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Stopped
  }

  # Provide script commands here to deploy the app

  # Restart the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
      Start-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Started
  }
  ```

### <a name="web-deploy-with-visual-studio"></a><span data-ttu-id="a586e-213">Visual Studio를 사용한 웹 배포</span><span class="sxs-lookup"><span data-stu-id="a586e-213">Web Deploy with Visual Studio</span></span>

<span data-ttu-id="a586e-214">웹 배포에서 사용할 게시 프로필을 만드는 방법은 [ASP.NET Core 앱 배포용 Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-214">See the [Visual Studio publish profiles for ASP.NET Core app deployment](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) topic to learn how to create a publish profile for use with Web Deploy.</span></span> <span data-ttu-id="a586e-215">호스팅 공급자에서 게시 프로필을 제공하거나 프로필을 만들 수 있도록 지원하는 경우 해당 프로필을 다운로드하고 Visual Studio **게시** 대화 상자를 사용하여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-215">If the hosting provider supplies a Publish Profile or support for creating one, download their profile and import it using the Visual Studio **Publish** dialog.</span></span>

![게시 대화 상자 페이지](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a><span data-ttu-id="a586e-217">Visual Studio 외부에서 웹 배포</span><span class="sxs-lookup"><span data-stu-id="a586e-217">Web Deploy outside of Visual Studio</span></span>

<span data-ttu-id="a586e-218">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 Visual Studio 외부에서 명령줄을 통해 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-218">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) can also be used outside of Visual Studio from the command line.</span></span> <span data-ttu-id="a586e-219">자세한 내용은 [웹 배포 도구](/iis/publish/using-web-deploy/use-the-web-deployment-tool)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-219">For more information, see [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool).</span></span>

### <a name="alternatives-to-web-deploy"></a><span data-ttu-id="a586e-220">웹 배포에 대한 대안</span><span class="sxs-lookup"><span data-stu-id="a586e-220">Alternatives to Web Deploy</span></span>

<span data-ttu-id="a586e-221">여러 가지 방법 중 하나를 사용하여 앱을 호스팅 시스템(예: Xcopy, Robocopy 또는 PowerShell)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-221">Use any of several methods to move the app to the hosting system, such as Xcopy, Robocopy, or PowerShell.</span></span> <span data-ttu-id="a586e-222">Visual Studio 사용자는 [게시 샘플(영문)](https://github.com/aspnet/vsweb-publish/blob/master/samples/samples.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-222">Visual Studio users may use the [Publish Samples](https://github.com/aspnet/vsweb-publish/blob/master/samples/samples.md).</span></span>

## <a name="browse-the-website"></a><span data-ttu-id="a586e-223">웹 사이트 찾아보기</span><span class="sxs-lookup"><span data-stu-id="a586e-223">Browse the website</span></span>

![IIS 시작 페이지가 로드된 Microsoft Edge 브라우저](index/_static/browsewebsite.png)

## <a name="data-protection"></a><span data-ttu-id="a586e-225">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="a586e-225">Data protection</span></span>

<span data-ttu-id="a586e-226">데이터 보호는 인증에 사용되는 것을 포함하여 여러 ASP.NET 미들웨어에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-226">Data Protection is used by several ASP.NET middlewares, including those used in authentication.</span></span> <span data-ttu-id="a586e-227">사용자의 코드에서 데이터 보호 API가 호출되지 않더라도 데이터 보호는 배포 스크립트 또는 사용자 코드를 사용하여 영구 키 저장소를 만들도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-227">Even if Data Protection APIs aren't called from user's code, Data Protection should be configured with a deployment script or in user code to create a persistent key store.</span></span> <span data-ttu-id="a586e-228">데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-228">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="a586e-229">키 링이 메모리에 저장되는 경우 앱을 다시 시작할 때 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-229">If the keyring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="a586e-230">모든 폼 인증 토큰이 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-230">All forms authentication tokens are invalidated.</span></span> 
* <span data-ttu-id="a586e-231">사용자는 다음 요청에서 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-231">Users are required to sign in again on their next request.</span></span> 
* <span data-ttu-id="a586e-232">키 링으로 보호된 모든 데이터는 더 이상 암호 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-232">Any data protected with the keyring can no longer be decrypted.</span></span>

<span data-ttu-id="a586e-233">IIS에서 데이터 보호를 구성하려면 다음 방법 중 **하나**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-233">To configure Data Protection under IIS, use **one** of the following approaches:</span></span>

### <a name="create-a-data-protection-registry-hive"></a><span data-ttu-id="a586e-234">데이터 보호 레지스트리 하이브 만들기</span><span class="sxs-lookup"><span data-stu-id="a586e-234">Create a Data Protection Registry Hive</span></span>

<span data-ttu-id="a586e-235">ASP.NET 앱에서 사용되는 데이터 보호 키는 앱 외부의 레지스트리 하이브에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-235">Data Protection keys used by ASP.NET apps are stored in registry hives external to the apps.</span></span> <span data-ttu-id="a586e-236">지정된 앱에 대한 키를 유지하려면 해당 응용 프로그램 풀에 대한 레지스트리 하이브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-236">To persist the keys for a given app, create a registry hive for the app pool.</span></span>

<span data-ttu-id="a586e-237">WebFarm이 아닌 독립 실행형 IIS 설치의 경우 [Data Protection Provision-AutoGenKeys.ps1 PowerShell 스크립트](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1)를 ASP.NET Core 앱과 함께 사용되는 각 응용 프로그램 풀에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-237">For standalone, non-webfarm IIS installations, the [Data Protection Provision-AutoGenKeys.ps1 PowerShell script](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1) can be used for each app pool used with an ASP.NET Core app.</span></span> <span data-ttu-id="a586e-238">이 스크립트는 작업자 프로세스 계정에만 ACL로 지정된 특수 레지스트리 키를 HKLM 레지스트리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-238">This script creates a special registry key in the HKLM registry that's ACLed only to the worker process account.</span></span> <span data-ttu-id="a586e-239">미사용 키는 컴퓨터 전체 키가 있는 DPAPI를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-239">Keys are encrypted at rest using DPAPI with a machine-wide key.</span></span>

<span data-ttu-id="a586e-240">웹 팜 시나리오에서는 UNC 경로를 사용하여 데이터 보호 키 링을 저장하도록 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-240">In web farm scenarios, an app can be configured to use a UNC path to store its data protection keyring.</span></span> <span data-ttu-id="a586e-241">기본적으로 데이터 보호 키는 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-241">By default, the data protection keys are not encrypted.</span></span> <span data-ttu-id="a586e-242">이러한 공유에 대한 파일 권한은 앱이 실행되는 Windows 계정으로 제한되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-242">Ensure that the file permissions for such a share are limited to the Windows account the app runs as.</span></span> <span data-ttu-id="a586e-243">또한 X509 인증서를 사용하여 미사용 키를 보호할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-243">In addition, an X509 certificate can be used to protect keys at rest.</span></span> <span data-ttu-id="a586e-244">사용자가 인증서를 업로드할 수 있는 메커니즘을 사용하는 것이 좋습니다. 즉 사용자의 신뢰할 수 있는 인증서 저장소에 인증서를 배치하고, 사용자의 앱이 실행되는 모든 컴퓨터에서 이 인증서를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-244">Consider a mechanism to allow users to upload certificates: Place certificates into the user's trusted certificate store and ensure they're available on all machines where the user's app runs.</span></span> <span data-ttu-id="a586e-245">자세한 내용은 [데이터 보호 구성](xref:security/data-protection/configuration/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-245">See [Configuring Data Protection](xref:security/data-protection/configuration/overview) for details.</span></span>

### <a name="configure-the-iis-application-pool-to-load-the-user-profile"></a><span data-ttu-id="a586e-246">사용자 프로필을 로드하도록 IIS 응용 프로그램 풀 구성</span><span class="sxs-lookup"><span data-stu-id="a586e-246">Configure the IIS Application Pool to load the user profile</span></span>

<span data-ttu-id="a586e-247">이 설정은 앱 풀에 대한 **고급 설정** 아래의 **프로세스 모델** 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-247">This setting is in the **Process Model** section under the **Advanced Settings** for the app pool.</span></span> <span data-ttu-id="a586e-248">사용자 프로필 로드를 `True`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-248">Set Load User Profile to `True`.</span></span> <span data-ttu-id="a586e-249">이렇게 하면 사용자 프로필 디렉터리 아래에 키가 저장되고, 앱 풀에 사용되는 사용자 계정과 관련된 키가 있는 DPAPI를 사용하여 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-249">This stores keys under the user profile directory and protects them using DPAPI with a key specific to the user account used for the app pool.</span></span>

### <a name="use-the-file-system-as-a-key-ring-store"></a><span data-ttu-id="a586e-250">파일 시스템을 키 링 저장소로 사용</span><span class="sxs-lookup"><span data-stu-id="a586e-250">Use the file system as a key ring store</span></span>

<span data-ttu-id="a586e-251">[파일 시스템을 키 링 저장소로 사용](xref:security/data-protection/configuration/overview)하도록 앱 코드를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-251">Adjust the app code to [use the file system as a key ring store](xref:security/data-protection/configuration/overview).</span></span> <span data-ttu-id="a586e-252">X509 인증서를 사용하여 키 링을 보호하고 신뢰할 수 있는 인증서인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-252">Use an X509 certificate to protect the keyring and ensure the certificate is a trusted certificate.</span></span> <span data-ttu-id="a586e-253">자체 서명된 인증서인 경우 신뢰할 수 있는 루트 저장소에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-253">If it's a self signed certificate, place the certificate in the Trusted Root store.</span></span>

<span data-ttu-id="a586e-254">웹 팜에서 IIS를 사용하는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-254">When using IIS in a web farm:</span></span>

* <span data-ttu-id="a586e-255">모든 컴퓨터에서 액세스할 수 있는 파일 공유를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-255">Use a file share that all machines can access.</span></span>
* <span data-ttu-id="a586e-256">각 시스템에 X509 인증서를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-256">Deploy an X509 certificate to each machine.</span></span> <span data-ttu-id="a586e-257">[코드에 데이터 보호](xref:security/data-protection/configuration/overview)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-257">Configure [data protection in code](xref:security/data-protection/configuration/overview).</span></span>

### <a name="set-a-machine-wide-policy-for-data-protection"></a><span data-ttu-id="a586e-258">데이터 보호에 대한 컴퓨터 수준 정책</span><span class="sxs-lookup"><span data-stu-id="a586e-258">Set a machine-wide policy for data protection</span></span>

<span data-ttu-id="a586e-259">데이터 보호 시스템은 데이터 보호 API를 사용하는 모든 앱에 대한 기본 [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy) 설정을 제한적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-259">The data protection system has limited support for setting a default [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy) for all apps that consume the Data Protection APIs.</span></span> <span data-ttu-id="a586e-260">자세한 내용은 [데이터 보호](xref:security/data-protection/index) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-260">See the [data protection](xref:security/data-protection/index) documentation for more details.</span></span>

## <a name="configuration-of-sub-applications"></a><span data-ttu-id="a586e-261">하위 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a586e-261">Configuration of sub-applications</span></span>

<span data-ttu-id="a586e-262">루트 앱 아래에 추가된 하위 앱에는 ASP.NET Core 모듈이 처리기로 포함되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-262">Sub-apps added under the root app shouldn't include the ASP.NET Core Module as a handler.</span></span> <span data-ttu-id="a586e-263">하위 앱의 *web.config* 파일에 모듈이 처리기로 추가되면, 하위 앱을 찾아보려고 할 때 잘못된 구성 파일을 참조하는 500.19(내부 서버 오류)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-263">If the module is added as a handler in a sub-app's *web.config* file, a 500.19 (Internal Server Error) referencing the faulty config file is received when attempting to browse the sub-app.</span></span> <span data-ttu-id="a586e-264">다음 예제에서는 ASP.NET Core 하위 앱에 대해 게시된 *web.config* 파일의 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-264">The following example shows the contents of a published *web.config* file for an ASP.NET Core sub-app:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="a586e-265">ASP.NET Core 앱 아래에 비ASP .NET Core 하위 앱을 호스팅하는 경우, 하위 앱의 *web.config* 파일에서 상속된 처리기를 명시적으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-265">When hosting a non-ASP.NET Core sub-app underneath an ASP.NET Core app, explicitly remove the inherited handler in the sub-app *web.config* file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore"/>
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="a586e-266">ASP.NET Core 모듈을 구성하는 방법에 대한 자세한 내용은 [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module) 항목 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-266">For more information on configuring the ASP.NET Core Module, see the [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic and the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

## <a name="configuration-of-iis-with-webconfig"></a><span data-ttu-id="a586e-267">web.config를 사용하여 IIS 구성</span><span class="sxs-lookup"><span data-stu-id="a586e-267">Configuration of IIS with web.config</span></span>

<span data-ttu-id="a586e-268">IIS 구성은 역방향 프록시 구성에 적용되는 IIS 기능에 대한 *web.config*에 포함된 **\<system.webServer>** 섹션의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-268">IIS configuration is influenced by the **\<system.webServer>** section of *web.config* for those IIS features that apply to a reverse proxy configuration.</span></span> <span data-ttu-id="a586e-269">IIS가 동적 압축을 사용하도록 시스템 수준에서 구성된 경우, 해당 설정은 응용 프로그램의 *web.config* 파일에서 **\<urlCompression>** 요소를 사용하여 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-269">If IIS is configured at the system level to use dynamic compression, that setting can be disabled for an app with the **\<urlCompression>** element in the app's *web.config* file.</span></span> <span data-ttu-id="a586e-270">자세한 내용은 [\<system.webServer>에 대한 구성 참조](https://docs.microsoft.com/iis/configuration/system.webServer/), [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module) 및 [ASP.NET Core와 함께 IIS 모듈 사용](xref:host-and-deploy/iis/modules)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-270">For more information, see the [configuration reference for \<system.webServer>](https://docs.microsoft.com/iis/configuration/system.webServer/), [ASP.NET Core Module Configuration Reference](xref:host-and-deploy/aspnet-core-module) and [Using IIS Modules with ASP.NET Core](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="a586e-271">격리된 응용 프로그램 풀(IIS 10.0 이상에서 지원됨)에서 실행되는 개별 앱에 대한 환경 변수를 설정해야 하는 경우, IIS 참조 설명서에서 *AppCmd.exe 명령* 섹션의 [\<environmentVariables> 환경 변수](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-271">If there's a need to set environment variables for individual apps running in isolated app pools (supported on IIS 10.0+), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic in the IIS reference documentation.</span></span>

## <a name="configuration-sections-of-webconfig"></a><span data-ttu-id="a586e-272">web.config 구성 섹션</span><span class="sxs-lookup"><span data-stu-id="a586e-272">Configuration sections of web.config</span></span>

<span data-ttu-id="a586e-273">*web.config*에 있는 ASP.NET Framework 앱의 다음 구성 섹션은 ASP.NET Core 앱의 구성에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-273">Configruation sections of ASP.NET Framework apps in *web.config* aren't used by ASP.NET Core apps for configuration:</span></span>

* <span data-ttu-id="a586e-274">**\<system.web>**</span><span class="sxs-lookup"><span data-stu-id="a586e-274">**\<system.web>**</span></span>
* <span data-ttu-id="a586e-275">**\<appSettings>**</span><span class="sxs-lookup"><span data-stu-id="a586e-275">**\<appSettings>**</span></span>
* <span data-ttu-id="a586e-276">**\<connectionStrings>**</span><span class="sxs-lookup"><span data-stu-id="a586e-276">**\<connectionStrings>**</span></span>
* <span data-ttu-id="a586e-277">**\<location>**</span><span class="sxs-lookup"><span data-stu-id="a586e-277">**\<location>**</span></span>

<span data-ttu-id="a586e-278">ASP.NET Core 앱은 다른 구성 공급자를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-278">ASP.NET Core apps are configured using other configuration providers.</span></span> <span data-ttu-id="a586e-279">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a586e-279">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="application-pools"></a><span data-ttu-id="a586e-280">응용 프로그램 풀</span><span class="sxs-lookup"><span data-stu-id="a586e-280">Application Pools</span></span>

<span data-ttu-id="a586e-281">단일 시스템에서 여러 웹 사이트를 호스팅하는 경우 각 앱을 자체의 응용 프로그램 풀에서 실행하여 서로 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-281">When hosting multiple websites on a single system, isolate the apps from each other by running each app in its own app pool.</span></span> <span data-ttu-id="a586e-282">이 구성은 IIS **웹 사이트 추가** 대화 상자의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-282">The IIS **Add Website** dialog defaults to this configuration.</span></span> <span data-ttu-id="a586e-283">**사이트 이름**을 제공하면 해당 텍스트가 자동으로 **응용 프로그램 풀** 텍스트 상자로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-283">When **Site name** is provided, the text is automatically transferred to the **Application pool** textbox.</span></span> <span data-ttu-id="a586e-284">웹 사이트를 추가할 때 이 사이트 이름을 사용하여 새 응용 프로그램 풀이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-284">A new app pool is created using the site name when the website is added.</span></span>

## <a name="application-pool-identity"></a><span data-ttu-id="a586e-285">응용 프로그램 풀 ID</span><span class="sxs-lookup"><span data-stu-id="a586e-285">Application Pool Identity</span></span>

<span data-ttu-id="a586e-286">응용 프로그램 풀 ID 계정을 사용하면 도메인 또는 로컬 계정을 만들고 관리할 필요 없이 고유한 계정으로 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-286">An app pool identity account allows an app to run under a unique account without having to create and manage domains or local accounts.</span></span> <span data-ttu-id="a586e-287">IIS 8.0 이상에서 IIS 관리 작업자 프로세스(WAS)는 새 응용 프로그램 풀의 이름으로 가상 계정을 만들고, 기본적으로 이 계정으로 응용 프로그램 풀의 작업자 프로세스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-287">On IIS 8.0+, the IIS Admin Worker Process (WAS) creates a virtual account with the name of the new app pool and runs the app pool's worker processes under this account by default.</span></span> <span data-ttu-id="a586e-288">IIS 관리 콘솔의 응용 프로그램 풀에 대한 **고급 설정** 아래에서 **ID**가 **ApplicationPoolIdentity**를 사용하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-288">In the IIS Management Console under **Advanced Settings** for the app pool, ensure that the **Identity** is set to use **ApplicationPoolIdentity**:</span></span>

![응용 프로그램 풀 고급 설정 대화 상자](index/_static/apppool-identity.png)

<span data-ttu-id="a586e-290">IIS 관리 프로세스는 Windows 보안 시스템에 앱 풀 이름이 포함된 보안 식별자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-290">The IIS management process creates a secure identifier with the name of the app pool in the Windows Security System.</span></span> <span data-ttu-id="a586e-291">리소스는 이 ID를 사용하여 보호할 수 있습니다. 그러나 이 ID는 실제 사용자 계정이 아니며 Windows 사용자 관리 콘솔에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-291">Resources can be secured by using this identity; however, this identity isn't a real user account and won't show up in the Windows User Management Console.</span></span>

<span data-ttu-id="a586e-292">IIS 작업자 프로세스에서 앱에 대한 높은 액세스 권한이 필요한 경우 앱이 포함된 디렉터리에 대한 ACL(액세스 제어 목록)을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-292">If the IIS worker process requires elevated access to the app, modify the Access Control List (ACL) for the directory containing the app:</span></span>

1. <span data-ttu-id="a586e-293">[Windows 탐색기]를 열고 해당 하위 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-293">Open Windows Explorer and navigate to the directory.</span></span>

2. <span data-ttu-id="a586e-294">디렉터리를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-294">Right-click on the directory and select **Properties**.</span></span>

3. <span data-ttu-id="a586e-295">**보안** 탭 아래에서 **편집** 단추, **추가** 단추를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-295">Under the **Security** tab, select the **Edit** button and then the **Add** button.</span></span>

4. <span data-ttu-id="a586e-296">**위치** 단추를 선택하고 시스템이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-296">Select the **Locations** button and make sure the system is selected.</span></span>

5. <span data-ttu-id="a586e-297">**선택할 개체 이름 입력** 텍스트 상자에서 **IIS AppPool\DefaultAppPool**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-297">Enter **IIS AppPool\DefaultAppPool** in **Enter the object names to select** textbox.</span></span>

   ![앱 폴더에 대한 사용자 또는 그룹 선택 대화 상자](index/_static/select-users-or-groups-1.png)

6. <span data-ttu-id="a586e-299">**이름 확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-299">Select the **Check Names** button.</span></span> <span data-ttu-id="a586e-300">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-300">Select **OK**.</span></span>

   ![앱 폴더에 대한 사용자 또는 그룹 선택 대화 상자](index/_static/select-users-or-groups-2.png)

<span data-ttu-id="a586e-302">또한 이 작업은 **ICACLS** 도구를 사용하는 명령 프롬프트를 통해 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a586e-302">This can also be accomplished via a command prompt using the **ICACLS** tool:</span></span>

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

## <a name="additional-resources"></a><span data-ttu-id="a586e-303">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a586e-303">Additional resources</span></span>

* [<span data-ttu-id="a586e-304">IIS에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a586e-304">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="a586e-305">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="a586e-305">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="a586e-306">ASP.NET Core 모듈 소개</span><span class="sxs-lookup"><span data-stu-id="a586e-306">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="a586e-307">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="a586e-307">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="a586e-308">ASP.NET Core와 함께 IIS 모듈 사용</span><span class="sxs-lookup"><span data-stu-id="a586e-308">Using IIS Modules with ASP.NET Core</span></span>](xref:host-and-deploy/iis/modules)
* [<span data-ttu-id="a586e-309">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="a586e-309">Introduction to ASP.NET Core</span></span>](../index.md)
* [<span data-ttu-id="a586e-310">공식 Microsoft IIS 사이트</span><span class="sxs-lookup"><span data-stu-id="a586e-310">The Official Microsoft IIS Site</span></span>](https://www.iis.net/)
* [<span data-ttu-id="a586e-311">Microsoft TechNet 라이브러리: Windows Server</span><span class="sxs-lookup"><span data-stu-id="a586e-311">Microsoft TechNet Library: Windows Server</span></span>](https://docs.microsoft.com/windows-server/windows-server-versions)
