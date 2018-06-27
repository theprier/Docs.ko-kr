---
title: IIS가 있는 Windows에서 ASP.NET Core 호스팅
author: guardrex
description: Windows Server IIS(인터넷 정보 서비스)에서 ASP.NET Core 앱을 호스팅하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2018
uid: host-and-deploy/iis/index
ms.openlocfilehash: ea18c451c2f68dc389cc6dc30ede9a10e3d8e6ac
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275414"
---
# <a name="host-aspnet-core-on-windows-with-iis"></a><span data-ttu-id="a6c4c-103">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="a6c4c-103">Host ASP.NET Core on Windows with IIS</span></span>

<span data-ttu-id="a6c4c-104">이 문서의 작성자: [Luke Latham](https://github.com/guardrex) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a6c4c-104">By [Luke Latham](https://github.com/guardrex) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="a6c4c-105">지원되는 운영 체제</span><span class="sxs-lookup"><span data-stu-id="a6c4c-105">Supported operating systems</span></span>

<span data-ttu-id="a6c4c-106">지원되는 운영 체제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-106">The following operating systems are supported:</span></span>

* <span data-ttu-id="a6c4c-107">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="a6c4c-107">Windows 7 or later</span></span>
* <span data-ttu-id="a6c4c-108">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="a6c4c-108">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="a6c4c-109">[HTTP.sys 서버](xref:fundamentals/servers/httpsys)(이전의 [WebListener](xref:fundamentals/servers/weblistener))는 IIS를 사용하는 역방향 프록시 구성에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-109">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)) doesn't work in a reverse proxy configuration with IIS.</span></span> <span data-ttu-id="a6c4c-110">[Kestrel 서버](xref:fundamentals/servers/kestrel)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-110">Use the [Kestrel server](xref:fundamentals/servers/kestrel).</span></span>

## <a name="application-configuration"></a><span data-ttu-id="a6c4c-111">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a6c4c-111">Application configuration</span></span>

### <a name="enable-the-iisintegration-components"></a><span data-ttu-id="a6c4c-112">IISIntegration 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="a6c4c-112">Enable the IISIntegration components</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="a6c4c-113">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="a6c4c-113">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="a6c4c-114">일반적인 *Program.cs*는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출하여 호스트 설정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-114">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to begin setting up a host.</span></span> <span data-ttu-id="a6c4c-115">`CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-115">`CreateDefaultBuilder` configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and enables IIS integration by configuring the base path and port for the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module):</span></span>

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

<span data-ttu-id="a6c4c-116">ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-116">The ASP.NET Core Module generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="a6c4c-117">`CreateDefaultBuilder`는 메서드는 동적 포트를 선택하고 `http://localhost:{dynamicPort}/`에서 수신 대기하도록 Kestrel을 구성하는 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 메서드를 호합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-117">`CreateDefaultBuilder` calls the [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) method, which picks up the dynamic port and configures Kestrel to listen on `http://localhost:{dynamicPort}/`.</span></span> <span data-ttu-id="a6c4c-118">이는 `UseUrls` 또는 [Kestrel의 수신 API](xref:fundamentals/servers/kestrel#endpoint-configuration)에 대한 호출과 같은 다른 URL 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-118">This overrides other URL configurations, such as calls to `UseUrls` or [Kestrel's Listen API](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span> <span data-ttu-id="a6c4c-119">따라서 모듈을 사용하는 경우 `UseUrls`에 대한 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-119">Therefore, calls to `UseUrls` or Kestrel's `Listen` API aren't required when using the module.</span></span> <span data-ttu-id="a6c4c-120">`UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때 지정된 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-120">If `UseUrls` or `Listen` is called, Kestrel listens on the port specified when running the app without IIS.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="a6c4c-121">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="a6c4c-121">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="a6c4c-122">[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) 패키지에 대한 종속성을 앱의 종속성에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-122">Include a dependency on the [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) package in the app's dependencies.</span></span> <span data-ttu-id="a6c4c-123">[UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 확장 메서드를 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에 추가하여 IIS 통합 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-123">Use IIS Integration middleware by adding the [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) extension method to [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder):</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<span data-ttu-id="a6c4c-124">[UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 및 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration)이 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-124">Both [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) and [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) are required.</span></span> <span data-ttu-id="a6c4c-125">`UseIISIntegration`을 호출하는 코드는 코드 이식성에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-125">Code calling `UseIISIntegration` doesn't affect code portability.</span></span> <span data-ttu-id="a6c4c-126">앱이 IIS 배후에서 실행되지 않는 경우(예를 들어 앱이 Kestrel에서 바로 실행되는 경우)에는 `UseIISIntegration`이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-126">If the app isn't run behind IIS (for example, the app is run directly on Kestrel), `UseIISIntegration` doesn't operate.</span></span>

<span data-ttu-id="a6c4c-127">ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-127">The ASP.NET Core Module generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="a6c4c-128">`UseIISIntegration` 메서드는 동적 포트를 선택하고 `http://locahost:{dynamicPort}/`에서 수신 대기하도록 Kestrel을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-128">The `UseIISIntegration` method picks up the dynamic port and configures Kestrel to listen on `http://locahost:{dynamicPort}/`.</span></span> <span data-ttu-id="a6c4c-129">이는 `UseUrls`에 대한 호출과 같은 다른 URL 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-129">This overrides other URL configurations, such as calls to `UseUrls`.</span></span> <span data-ttu-id="a6c4c-130">따라서 모듈을 사용하는 경우 `UseUrls`에 대한 호출이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-130">Therefore, a call to `UseUrls` isn't required when using the module.</span></span> <span data-ttu-id="a6c4c-131">`UseUrls`를 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때 지정된 포트에서 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-131">If `UseUrls` is called, Kestrel listens on the port specified when running the app without IIS.</span></span>

<span data-ttu-id="a6c4c-132">`UseUrls`를 ASP.NET Core 1.0 앱에서 호출하는 경우 모듈 구성 포트를 덮어 쓰지 않도록 `UseIISIntegration`을 호출하기 **전에** 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-132">If `UseUrls` is called in an ASP.NET Core 1.0 app, call it **before** calling `UseIISIntegration` so that the module-configured port isn't overwritten.</span></span> <span data-ttu-id="a6c4c-133">모듈 설정이 `UseUrls`를 재정의하기 때문에 이 호출 순서는 ASP.NET Core 1.1에서 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-133">This calling order isn't required with ASP.NET Core 1.1 because the module setting overrides `UseUrls`.</span></span>

---

<span data-ttu-id="a6c4c-134">호스팅에 대한 자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/host/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-134">For more information on hosting, see [Host in ASP.NET Core](xref:fundamentals/host/index).</span></span>

### <a name="iis-options"></a><span data-ttu-id="a6c4c-135">IIS 옵션</span><span class="sxs-lookup"><span data-stu-id="a6c4c-135">IIS options</span></span>

<span data-ttu-id="a6c4c-136">IIS 옵션을 구성하려면 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices)에 [IISOptions](/dotnet/api/microsoft.aspnetcore.builder.iisoptions)에 대한 서비스 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-136">To configure IIS options, include a service configuration for [IISOptions](/dotnet/api/microsoft.aspnetcore.builder.iisoptions) in [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices).</span></span> <span data-ttu-id="a6c4c-137">다음 예제에서는 `HttpContext.Connection.ClientCertificate`를 채우기 위해 클라이언트 인증서를 앱에 전달하는 옵션이 사용하지 않도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-137">In the following example, forwarding client certificates to the app to populate `HttpContext.Connection.ClientCertificate` is disabled:</span></span>

```csharp
services.Configure<IISOptions>(options => 
{
    options.ForwardClientCertificate = false;
});
```

| <span data-ttu-id="a6c4c-138">옵션</span><span class="sxs-lookup"><span data-stu-id="a6c4c-138">Option</span></span>                         | <span data-ttu-id="a6c4c-139">기본</span><span class="sxs-lookup"><span data-stu-id="a6c4c-139">Default</span></span> | <span data-ttu-id="a6c4c-140">설정</span><span class="sxs-lookup"><span data-stu-id="a6c4c-140">Setting</span></span> |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | <span data-ttu-id="a6c4c-141">`true`이면 IIS 통합 미들웨어가 [Windows 인증](xref:security/authentication/windowsauth)에 의해 인증된 `HttpContext.User`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-141">If `true`, IIS Integration Middleware sets the `HttpContext.User` authenticated by [Windows Authentication](xref:security/authentication/windowsauth).</span></span> <span data-ttu-id="a6c4c-142">`false`이면 미들웨어가 `HttpContext.User`에게 ID만 제공하고, `AuthenticationScheme`에서 명시적으로 요청될 때 챌린지에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-142">If `false`, the middleware only provides an identity for `HttpContext.User` and responds to challenges when explicitly requested by the `AuthenticationScheme`.</span></span> <span data-ttu-id="a6c4c-143">IIS에서 Windows 인증은 `AutomaticAuthentication`이 작동하기 위해 사용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-143">Windows Authentication must be enabled in IIS for `AutomaticAuthentication` to function.</span></span> <span data-ttu-id="a6c4c-144">자세한 내용은 [Windows 인증](xref:security/authentication/windowsauth) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-144">For more information, see the [Windows Authentication](xref:security/authentication/windowsauth) topic.</span></span> |
| `AuthenticationDisplayName`    | `null`  | <span data-ttu-id="a6c4c-145">로그인 페이지에서 사용자에게 나타나는 표시 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-145">Sets the display name shown to users on login pages.</span></span> |
| `ForwardClientCertificate`     | `true`  | <span data-ttu-id="a6c4c-146">`true`면서 `MS-ASPNETCORE-CLIENTCERT` 요청 헤더가 있는 경우 `HttpContext.Connection.ClientCertificate`가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-146">If `true` and the `MS-ASPNETCORE-CLIENTCERT` request header is present, the `HttpContext.Connection.ClientCertificate` is populated.</span></span> |

### <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="a6c4c-147">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="a6c4c-147">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="a6c4c-148">체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-148">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="a6c4c-149">추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-149">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="a6c4c-150">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-150">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

### <a name="webconfig-file"></a><span data-ttu-id="a6c4c-151">web.config 파일</span><span class="sxs-lookup"><span data-stu-id="a6c4c-151">web.config file</span></span>

<span data-ttu-id="a6c4c-152">*web.config* 파일은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-152">The *web.config* file configures the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="a6c4c-153">*web.config* 파일을 만들고, 변하고, 게시하는 작업은 프로젝트를 게시할 때 MSBuild 대상(`_TransformWebConfig`)에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-153">Creating, transforming, and publishing the *web.config* file is handled by an MSBuild target (`_TransformWebConfig`) when the project is published.</span></span> <span data-ttu-id="a6c4c-154">이 대상은 웹 SDK 대상(`Microsoft.NET.Sdk.Web`)에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-154">This target is present in the Web SDK targets (`Microsoft.NET.Sdk.Web`).</span></span> <span data-ttu-id="a6c4c-155">SDK는 프로젝트 파일을 기반으로 해서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-155">The SDK is set at the top of the project file:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

<span data-ttu-id="a6c4c-156">프로젝트에 *web.config* 파일이 없는 경우, [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 생성되어 [게시된 출력](xref:host-and-deploy/directory-structure)으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-156">If a *web.config* file isn't present in the project, the file is created with the correct *processPath* and *arguments* to configure the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and moved to [published output](xref:host-and-deploy/directory-structure).</span></span>

<span data-ttu-id="a6c4c-157">프로젝트에 *web.config* 파일이 있는 경우, ASP.NET Core 모듈을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 변환되어 게시된 출력으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-157">If a *web.config* file is present in the project, the file is transformed with the correct *processPath* and *arguments* to configure the ASP.NET Core Module and moved to published output.</span></span> <span data-ttu-id="a6c4c-158">변환은 이 파일의 IIS 구성 설정을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-158">The transformation doesn't modify IIS configuration settings in the file.</span></span>

<span data-ttu-id="a6c4c-159">*web.config* 파일은 활성 IIS 모듈을 제어하는 추가 IIS 구성 설정을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-159">The *web.config* file may provide additional IIS configuration settings that control active IIS modules.</span></span> <span data-ttu-id="a6c4c-160">ASP.NET Core 앱을 사용하여 요청을 처리할 수 있는 IIS 모듈에 대한 자세한 내용은 [IIS 모듈](xref:host-and-deploy/iis/modules) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-160">For information on IIS modules that are capable of processing requests with ASP.NET Core apps, see the [IIS modules](xref:host-and-deploy/iis/modules) topic.</span></span>

<span data-ttu-id="a6c4c-161">웹 SDK가 *web.config* 파일을 변환하지 못하게 하려면 프로젝트 파일의 **\<IsTransformWebConfigDisabled>** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-161">To prevent the Web SDK from transforming the *web.config* file, use the **\<IsTransformWebConfigDisabled>** property in the project file:</span></span>

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="a6c4c-162">웹 SDK가 파일을 변환하지 않도록 설정하는 경우 개발자가 *processPath* 및 *인수*를 수동으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-162">When disabling the Web SDK from transforming the file, the *processPath* and *arguments* should be manually set by the developer.</span></span> <span data-ttu-id="a6c4c-163">자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-163">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

### <a name="webconfig-file-location"></a><span data-ttu-id="a6c4c-164">web.config 파일 위치</span><span class="sxs-lookup"><span data-stu-id="a6c4c-164">web.config file location</span></span>

<span data-ttu-id="a6c4c-165">IIS 및 Kestrel 서버 간의 역방향 프록시를 만들려면 배포된 앱의 콘텐츠 루트 경로(일반적으로 앱 기본 경로)에 *web.config* 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-165">In order to create the reverse proxy between IIS and the Kestrel server, the *web.config* file must be present at the content root path (typically the app base path) of the deployed app.</span></span> <span data-ttu-id="a6c4c-166">IIS에 제공되는 웹 사이트 실제 경로와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-166">This is the same location as the website physical path provided to IIS.</span></span> <span data-ttu-id="a6c4c-167">웹 배포를 사용하여 여러 앱을 게시하도록 설정하려면 앱의 루트에 *web.config* 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-167">The *web.config* file is required at the root of the app to enable the publishing of multiple apps using Web Deploy.</span></span>

<span data-ttu-id="a6c4c-168">중요한 파일은 *\<assembly>.runtimeconfig.json*, *\<assembly>.xml*(XML 문서 주석) 및 *\<assembly>.deps.json*과 같은 앱의 실제 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-168">Sensitive files exist on the app's physical path, such as *\<assembly>.runtimeconfig.json*, *\<assembly>.xml* (XML Documentation comments), and *\<assembly>.deps.json*.</span></span> <span data-ttu-id="a6c4c-169">*web.config* 파일이 있고 사이트가 정상적으로 시작되면 IIS는 이러한 중요한 파일이 요청되어도 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-169">When the *web.config* file is present and and the site starts normally, IIS doesn't serve these sensitive files if they're requested.</span></span> <span data-ttu-id="a6c4c-170">*web.config* 파일이 없거나, 이름이 잘못 지정되었거나, 정상적으로 시작되도록 사이트를 구성할 수 없는 경우 IIS에서 중요한 파일을 공개적으로 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-170">If the *web.config* file is missing, incorrectly named, or unable to configure the site for normal startup, IIS may serve sensitive files publicly.</span></span>

<span data-ttu-id="a6c4c-171">***web.config* 파일이 항상 배포에 있어야 하며, 올바르게 이름이 지정되고, 정상적으로 시작되도록 사이트를 구성할 수 있어야 합니다. 프로덕션 배포에서 *web.config* 파일을 제거하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-171">**The *web.config* file must be present in the deployment at all times, correctly named, and able to configure the site for normal start up. Never remove the *web.config* file from a production deployment.**</span></span>

## <a name="iis-configuration"></a><span data-ttu-id="a6c4c-172">IIS 구성</span><span class="sxs-lookup"><span data-stu-id="a6c4c-172">IIS configuration</span></span>

<span data-ttu-id="a6c4c-173">**Windows Server 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-173">**Windows Server operating systems**</span></span>

<span data-ttu-id="a6c4c-174">**웹 서버(IIS)** 서버 역할을 사용하도록 설정하고 역할 서비스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-174">Enable the **Web Server (IIS)** server role and establish role services.</span></span>

1. <span data-ttu-id="a6c4c-175">**관리** 메뉴 또는 **서버 관리자**의 링크를 통해 **역할 및 기능 추가** 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-175">Use the **Add Roles and Features** wizard from the **Manage** menu or the link in **Server Manager**.</span></span> <span data-ttu-id="a6c4c-176">**서버 역할** 단계에서 **웹 서버(IIS)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-176">On the **Server Roles** step, check the box for **Web Server (IIS)**.</span></span>

   ![서버 역할 선택 단계에서 선택된 웹 서버 IIS 역할](index/_static/server-roles-ws2016.png)

1. <span data-ttu-id="a6c4c-178">**기능** 단계 후에는 웹 서버(IIS)에 대한 **역할 서비스** 단계가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-178">After the **Features** step, the **Role services** step loads for Web Server (IIS).</span></span> <span data-ttu-id="a6c4c-179">원하는 IIS 역할 서비스를 선택하거나 제공된 기본 역할 서비스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-179">Select the IIS role services desired or accept the default role services provided.</span></span>

   ![역할 서비스 선택 단계에서 선택된 기본 역할 서비스](index/_static/role-services-ws2016.png)

   <span data-ttu-id="a6c4c-181">**Windows 인증(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-181">**Windows Authentication (Optional)**</span></span>  
   <span data-ttu-id="a6c4c-182">Windows 인증을 사용하도록 설정하려면 **웹 서버** > **보안** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-182">To enable Windows Authentication, expand the following nodes: **Web Server** > **Security**.</span></span> <span data-ttu-id="a6c4c-183">**Windows 인증** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-183">Select the **Windows Authentication** feature.</span></span> <span data-ttu-id="a6c4c-184">자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-184">For more information, see [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) and [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

   <span data-ttu-id="a6c4c-185">**WebSockets(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-185">**WebSockets (Optional)**</span></span>  
   <span data-ttu-id="a6c4c-186">WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-186">WebSockets is supported with ASP.NET Core 1.1 or later.</span></span> <span data-ttu-id="a6c4c-187">WebSockets를 사용하도록 설정하려면 **웹 서버** > **응용 프로그램 개발** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-187">To enable WebSockets, expand the following nodes: **Web Server** > **Application Development**.</span></span> <span data-ttu-id="a6c4c-188">**WebSocket 프로토콜** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-188">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="a6c4c-189">자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-189">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

1. <span data-ttu-id="a6c4c-190">**확인** 단계를 진행하여 웹 서버 역할 및 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-190">Proceed through the **Confirmation** step to install the web server role and services.</span></span> <span data-ttu-id="a6c4c-191">**웹 서버(IIS)** 역할을 설치한 후에 서버/IIS를 다시 시작할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-191">A server/IIS restart isn't required after installing the **Web Server (IIS)** role.</span></span>

<span data-ttu-id="a6c4c-192">**Windows 데스크톱 운영 체제**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-192">**Windows desktop operating systems**</span></span>

<span data-ttu-id="a6c4c-193">**IIS 관리 콘솔** 및 **World Wide Web 서비스**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-193">Enable the **IIS Management Console** and **World Wide Web Services**.</span></span>

1. <span data-ttu-id="a6c4c-194">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-194">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>

1. <span data-ttu-id="a6c4c-195">**인터넷 정보 서비스** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-195">Open the **Internet Information Services** node.</span></span> <span data-ttu-id="a6c4c-196">**웹 관리 도구** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-196">Open the **Web Management Tools** node.</span></span>

1. <span data-ttu-id="a6c4c-197">**IIS 관리 콘솔** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-197">Check the box for **IIS Management Console**.</span></span>

1. <span data-ttu-id="a6c4c-198">**World Wide Web 서비스** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-198">Check the box for **World Wide Web Services**.</span></span>

1. <span data-ttu-id="a6c4c-199">**World Wide Web 서비스**의 기본 기능을 그대로 사용하거나 IIS 기능을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-199">Accept the default features for **World Wide Web Services** or customize the IIS features.</span></span>

   <span data-ttu-id="a6c4c-200">**Windows 인증(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-200">**Windows Authentication (Optional)**</span></span>  
   <span data-ttu-id="a6c4c-201">Windows 인증을 사용하도록 설정하려면 **World Wide Web 서비스** > **보안** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-201">To enable Windows Authentication, expand the following nodes: **World Wide Web Services** > **Security**.</span></span> <span data-ttu-id="a6c4c-202">**Windows 인증** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-202">Select the **Windows Authentication** feature.</span></span> <span data-ttu-id="a6c4c-203">자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-203">For more information, see [Windows Authentication \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) and [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

   <span data-ttu-id="a6c4c-204">**WebSockets(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-204">**WebSockets (Optional)**</span></span>  
   <span data-ttu-id="a6c4c-205">WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-205">WebSockets is supported with ASP.NET Core 1.1 or later.</span></span> <span data-ttu-id="a6c4c-206">WebSockets를 사용하도록 설정하려면 **World Wide Web 서비스** > **응용 프로그램 개발 기능** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-206">To enable WebSockets, expand the following nodes: **World Wide Web Services** > **Application Development Features**.</span></span> <span data-ttu-id="a6c4c-207">**WebSocket 프로토콜** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-207">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="a6c4c-208">자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-208">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

1. <span data-ttu-id="a6c4c-209">IIS 설치 시 다시 시작해야 하는 경우 시스템을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-209">If the IIS installation requires a restart, restart the system.</span></span>

![Windows 기능에서 선택된 IIS 관리 콘솔 및 World Wide Web 서비스](index/_static/windows-features-win10.png)

---

## <a name="install-the-net-core-hosting-bundle"></a><span data-ttu-id="a6c4c-211">.NET Core 호스팅 번들 설치</span><span class="sxs-lookup"><span data-stu-id="a6c4c-211">Install the .NET Core Hosting Bundle</span></span>

1. <span data-ttu-id="a6c4c-212">호스팅 시스템에 *.NET Core 호스팅 번들*을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-212">Install the *.NET Core Hosting Bundle* on the hosting system.</span></span> <span data-ttu-id="a6c4c-213">번들은 .NET Core 런타임, .NET Core 라이브러리 및 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-213">The bundle installs the .NET Core Runtime, .NET Core Library, and the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="a6c4c-214">이 모듈은 IIS와 Kestrel 서버 간에 역방향 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-214">The module creates the reverse proxy between IIS and the Kestrel server.</span></span> <span data-ttu-id="a6c4c-215">시스템이 인터넷에 연결되지 않은 경우 [Microsoft Visual C++ 2015 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=53840)를 설치한 후에 .NET Core 호스팅 번들을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-215">If the system doesn't have an Internet connection, obtain and install the [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840) before installing the .NET Core Hosting Bundle.</span></span>

   1. <span data-ttu-id="a6c4c-216">[.NET 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-216">Navigate to the [.NET All Downloads page](https://www.microsoft.com/net/download/all).</span></span>
   1. <span data-ttu-id="a6c4c-217">테이블의 **런타임** 열에 있는 목록(**X.Y 런타임(vX.Y.Z) 다운로드**)에서 최신 미리 보기 상태가 아닌 .NET Core 런타임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-217">In the **Runtime** column of the table, select the latest non-preview .NET Core runtime from the list (**X.Y Runtime (vX.Y.Z) downloads**).</span></span> <span data-ttu-id="a6c4c-218">최신 런타임에는 **현재** 레이블이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-218">The latest runtime has a **Current** label.</span></span> <span data-ttu-id="a6c4c-219">미리 보기 소프트웨어로 작업하려는 경우가 아니면 해당 링크 텍스트에서 “미리 보기” 또는 “rc”(릴리스 후보)라는 단어가 있는 런타임을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-219">Unless you intend to work with preview software, avoid a runtime with the word "preview" or "rc" (Release Candidate) in its link text.</span></span>
   1. <span data-ttu-id="a6c4c-220">.NET Core 런타임 다운로드 페이지의 **Windows**에서 **호스팅 번들 설치 관리자** 링크를 선택하여 *.NET Core 호스팅 번들* 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-220">On the .NET Core runtime download page under **Windows**, select the **Hosting Bundle Installer** link to download the *.NET Core Hosting Bundle* installer.</span></span>
   1. <span data-ttu-id="a6c4c-221">서버에서 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-221">Run the installer on the server.</span></span>

   <span data-ttu-id="a6c4c-222">**중요!**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-222">**Important!**</span></span> <span data-ttu-id="a6c4c-223">IIS 이전에 호스팅 번들이 설치된 경우 번들 설치를 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-223">If the Hosting Bundle is installed before IIS, the bundle installation must be repaired.</span></span> <span data-ttu-id="a6c4c-224">IIS를 설치한 후 호스팅 번들 설치 프로그램을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-224">Run the Hosting Bundle installer again after installing IIS.</span></span>
   
   <span data-ttu-id="a6c4c-225">설치 관리자가 x64 OS에서 x86 패키지를 설치하지 않도록 방지하려면 `OPT_NO_X86=1` 스위치를 사용하여 관리자 명령 프롬프트에서 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-225">To prevent the installer from installing x86 packages on an x64 OS, run the installer from an administrator command prompt with the switch `OPT_NO_X86=1`.</span></span>

1. <span data-ttu-id="a6c4c-226">시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**, **net start w3svc**를 차례로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-226">Restart the system or execute **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span> <span data-ttu-id="a6c4c-227">IIS를 다시 시작하면 설치 관리자에 의한 시스템 PATH 변경 내용이 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-227">Restarting IIS picks up a change to the system PATH made by the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="a6c4c-228">IIS 공유 구성에 대한 자세한 내용은 [IIS 공유 구성을 사용하는 ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-228">For information on IIS Shared Configuration, see [ASP.NET Core Module with IIS Shared Configuration](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration).</span></span>

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a><span data-ttu-id="a6c4c-229">Visual Studio을 사용하여 게시할 때 웹 배포 설치</span><span class="sxs-lookup"><span data-stu-id="a6c4c-229">Install Web Deploy when publishing with Visual Studio</span></span>

<span data-ttu-id="a6c4c-230">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하여 앱을 서버에 배포하는 경우 최신 버전의 웹 배포를 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-230">When deploying apps to servers with [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy), install the latest version of Web Deploy on the server.</span></span> <span data-ttu-id="a6c4c-231">웹 배포를 설치하려면 [WebPI(웹 플랫폼 설치 관리자)](https://www.microsoft.com/web/downloads/platform.aspx)를 사용하거나 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=43717)에서 직접 설치 관리자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-231">To install Web Deploy, use the [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) or obtain an installer directly from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43717).</span></span> <span data-ttu-id="a6c4c-232">WebPI를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-232">The preferred method is to use WebPI.</span></span> <span data-ttu-id="a6c4c-233">WebPI는 호스팅 공급자에 대한 독립 실행형 설치 및 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-233">WebPI offers a standalone setup and a configuration for hosting providers.</span></span>

## <a name="create-the-iis-site"></a><span data-ttu-id="a6c4c-234">IIS 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="a6c4c-234">Create the IIS site</span></span>

1. <span data-ttu-id="a6c4c-235">호스팅 시스템에서 앱의 게시된 폴더 및 파일을 포함할 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-235">On the hosting system, create a folder to contain the app's published folders and files.</span></span> <span data-ttu-id="a6c4c-236">앱의 배포 레이아웃은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-236">An app's deployment layout is described in the [Directory Structure](xref:host-and-deploy/directory-structure) topic.</span></span>

1. <span data-ttu-id="a6c4c-237">stdout 로깅을 사용하도록 설정할 경우 ASP.NET Core 모듈 stdout 로그를 보관할 *logs* 폴더를 새 폴더 안에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-237">Within the new folder, create a *logs* folder to hold ASP.NET Core Module stdout logs when stdout logging is enabled.</span></span> <span data-ttu-id="a6c4c-238">앱이 페이로드에서 *logs* 폴더로 배포되는 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-238">If the app is deployed with a *logs* folder in the payload, skip this step.</span></span> <span data-ttu-id="a6c4c-239">로컬에서 프로젝트가 빌드될 때 MSBuild에서 *logs* 폴더를 자동으로 만들도록 설정하는 방법에 대한 지침은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-239">For instructions on how to enable MSBuild to create the *logs* folder automatically when the project is built locally, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a6c4c-240">stdout 로그는 앱 시작 오류의 문제 해결 용도로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-240">Only use the stdout log to troubleshoot app startup failures.</span></span> <span data-ttu-id="a6c4c-241">일상적인 앱 로깅에는 stdout 로깅을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-241">Never use stdout logging for routine app logging.</span></span> <span data-ttu-id="a6c4c-242">로그 파일 크기 또는 생성되는 로그 파일 수에 대한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-242">There's no limit on log file size or the number of log files created.</span></span> <span data-ttu-id="a6c4c-243">앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-243">The app pool must have write access to the location where the logs are written.</span></span> <span data-ttu-id="a6c4c-244">로그 위치에 대한 해당 경로에 있는 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-244">All of the folders on the path to the log location must exist.</span></span> <span data-ttu-id="a6c4c-245">stdout 로그에 대한 자세한 내용은 [로그 생성 및 리디렉션](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-245">For more information on the stdout log, see [Log creation and redirection](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection).</span></span> <span data-ttu-id="a6c4c-246">ASP.NET Core 앱의 로깅에 대한 자세한 내용은 [로깅](xref:fundamentals/logging/index) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-246">For information on logging in an ASP.NET Core app, see the [Logging](xref:fundamentals/logging/index) topic.</span></span>

1. <span data-ttu-id="a6c4c-247">**IIS 관리자**의 **연결** 패널에서 서버 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-247">In **IIS Manager**, open the server's node in the **Connections** panel.</span></span> <span data-ttu-id="a6c4c-248">**사이트** 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-248">Right-click the **Sites** folder.</span></span> <span data-ttu-id="a6c4c-249">상황에 맞는 메뉴에서 **웹 사이트 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-249">Select **Add Website** from the contextual menu.</span></span>

1. <span data-ttu-id="a6c4c-250">**사이트 이름**을 제공하고 **실제 경로**를 앱의 배포 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-250">Provide a **Site name** and set the **Physical path** to the app's deployment folder.</span></span> <span data-ttu-id="a6c4c-251">**바인딩** 구성을 제공하고 **확인**을 선택하여 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-251">Provide the **Binding** configuration and create the website by selecting **OK**:</span></span>

   ![[웹 사이트 추가] 단계에서 사이트 이름, 실제 경로 및 호스트 이름을 제공합니다.](index/_static/add-website-ws2016.png)

   > [!WARNING]
   > <span data-ttu-id="a6c4c-253">최상위 와일드카드 바인딩(`http://*:80/` 및 `http://+:80`)을 사용하지 **않아야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-253">Top-level wildcard bindings (`http://*:80/` and `http://+:80`) should **not** be used.</span></span> <span data-ttu-id="a6c4c-254">최상위 와일드카드 바인딩은 보안 취약점에 앱을 노출시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-254">Top-level wildcard bindings can open up your app to security vulnerabilities.</span></span> <span data-ttu-id="a6c4c-255">강력한 와일드카드와 약한 와일드카드 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-255">This applies to both strong and weak wildcards.</span></span> <span data-ttu-id="a6c4c-256">와일드카드보다는 명시적 호스트 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-256">Use explicit host names rather than wildcards.</span></span> <span data-ttu-id="a6c4c-257">전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.mysub.com`)에는 이러한 보안 위험이 없습니다(취약한 `*.com`과 반대임).</span><span class="sxs-lookup"><span data-stu-id="a6c4c-257">Subdomain wildcard binding (for example, `*.mysub.com`) doesn't have this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="a6c4c-258">자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-258">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

1. <span data-ttu-id="a6c4c-259">서버 노드에서 **응용 프로그램 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-259">Under the server's node, select **Application Pools**.</span></span>

1. <span data-ttu-id="a6c4c-260">사이트의 앱 풀을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **기본 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-260">Right-click the site's app pool and select **Basic Settings** from the contextual menu.</span></span>

1. <span data-ttu-id="a6c4c-261">**응용 프로그램 풀 편집** 창에서 **.NET CLR 버전**을 **관리 코드 없음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-261">In the **Edit Application Pool** window, set the **.NET CLR version** to **No Managed Code**:</span></span>

   ![.NET CLR 버전에 대해 관리 코드 없음 설정](index/_static/edit-apppool-ws2016.png)

    <span data-ttu-id="a6c4c-263">ASP.NET Core는 별도의 프로세스에서 실행되며 런타임을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-263">ASP.NET Core runs in a separate process and manages the runtime.</span></span> <span data-ttu-id="a6c4c-264">ASP.NET Core에서는 데스크톱 CLR을 로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-264">ASP.NET Core doesn't rely on loading the desktop CLR.</span></span> <span data-ttu-id="a6c4c-265">**.NET CLR 버전**을 **관리 코드 없음**으로 설정하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-265">Setting the **.NET CLR version** to **No Managed Code** is optional.</span></span>

1. <span data-ttu-id="a6c4c-266">프로세스 모델 ID에 적절한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-266">Confirm the process model identity has the proper permissions.</span></span>

   <span data-ttu-id="a6c4c-267">응용 프로그램 풀의 기본 ID(**프로세스 모델** > **ID**)가 **ApplicationPoolIdentity**에서 다른 ID로 변경되면, 새 ID에 앱의 폴더, 데이터베이스 및 기타 필요한 리소스에 액세스하는 데 필요한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-267">If the default identity of the app pool (**Process Model** > **Identity**) is changed from **ApplicationPoolIdentity** to another identity, verify that the new identity has the required permissions to access the app's folder, database, and other required resources.</span></span> <span data-ttu-id="a6c4c-268">예를 들어 앱 풀에는 앱이 파일을 읽고 쓰는 폴더에 대한 읽기 및 쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-268">For example, the app pool requires read and write access to folders where the app reads and writes files.</span></span>

<span data-ttu-id="a6c4c-269">**Windows 인증 구성(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-269">**Windows Authentication configuration (Optional)**</span></span>  
<span data-ttu-id="a6c4c-270">자세한 내용은 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-270">For more information, see [Configure Windows authentication](xref:security/authentication/windowsauth).</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="a6c4c-271">앱 배포</span><span class="sxs-lookup"><span data-stu-id="a6c4c-271">Deploy the app</span></span>

<span data-ttu-id="a6c4c-272">호스팅 시스템에 만든 폴더에 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-272">Deploy the app to the folder created on the hosting system.</span></span> <span data-ttu-id="a6c4c-273">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 배포에 권장되는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-273">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) is the recommended mechanism for deployment.</span></span>

### <a name="web-deploy-with-visual-studio"></a><span data-ttu-id="a6c4c-274">Visual Studio를 사용한 웹 배포</span><span class="sxs-lookup"><span data-stu-id="a6c4c-274">Web Deploy with Visual Studio</span></span>

<span data-ttu-id="a6c4c-275">웹 배포에서 사용할 게시 프로필을 만드는 방법은 [ASP.NET Core 앱 배포용 Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-275">See the [Visual Studio publish profiles for ASP.NET Core app deployment](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) topic to learn how to create a publish profile for use with Web Deploy.</span></span> <span data-ttu-id="a6c4c-276">호스팅 공급자가 게시 프로필을 제공하거나 게시 프로필을 만들 수 있도록 지원하는 경우 해당 프로필을 다운로드하고 Visual Studio **게시** 대화 상자를 사용하여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-276">If the hosting provider provides a Publish Profile or support for creating one, download their profile and import it using the Visual Studio **Publish** dialog.</span></span>

![게시 대화 상자 페이지](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a><span data-ttu-id="a6c4c-278">Visual Studio 외부에서 웹 배포</span><span class="sxs-lookup"><span data-stu-id="a6c4c-278">Web Deploy outside of Visual Studio</span></span>

<span data-ttu-id="a6c4c-279">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 Visual Studio 외부에서 명령줄을 통해 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-279">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) can also be used outside of Visual Studio from the command line.</span></span> <span data-ttu-id="a6c4c-280">자세한 내용은 [웹 배포 도구](/iis/publish/using-web-deploy/use-the-web-deployment-tool)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-280">For more information, see [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool).</span></span>

### <a name="alternatives-to-web-deploy"></a><span data-ttu-id="a6c4c-281">웹 배포에 대한 대안</span><span class="sxs-lookup"><span data-stu-id="a6c4c-281">Alternatives to Web Deploy</span></span>

<span data-ttu-id="a6c4c-282">수동 복사, Xcopy, Robocopy, PowerShell 등의 여러 방법 중 하나를 사용하여 앱을 호스팅 시스템으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-282">Use any of several methods to move the app to the hosting system, such as manual copy, Xcopy, Robocopy, or PowerShell.</span></span>

<span data-ttu-id="a6c4c-283">IIS에 ASP.NET Core 배포에 대한 자세한 내용은 [IIS 관리자를 위한 배포 리소스](#deployment-resources-for-iis-administrators) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-283">For more information on ASP.NET Core deployment to IIS, see the [Deployment resources for IIS administrators](#deployment-resources-for-iis-administrators) section.</span></span>

## <a name="browse-the-website"></a><span data-ttu-id="a6c4c-284">웹 사이트 찾아보기</span><span class="sxs-lookup"><span data-stu-id="a6c4c-284">Browse the website</span></span>

![IIS 시작 페이지가 로드된 Microsoft Edge 브라우저](index/_static/browsewebsite.png)

## <a name="locked-deployment-files"></a><span data-ttu-id="a6c4c-286">배포 파일이 잠겨 있음</span><span class="sxs-lookup"><span data-stu-id="a6c4c-286">Locked deployment files</span></span>

<span data-ttu-id="a6c4c-287">앱이 실행 중이면 배포 폴더의 파일이 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-287">Files in the deployment folder are locked when the app is running.</span></span> <span data-ttu-id="a6c4c-288">잠긴 파일은 배포 중에 덮어쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-288">Locked files can't be overwritten during deployment.</span></span> <span data-ttu-id="a6c4c-289">배포에서 잠긴 파일을 해제하려면 다음 방법 중 **하나**를 사용하여 앱 풀을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-289">To release locked files in a deployment, stop the app pool using **one** of the following approaches:</span></span>

* <span data-ttu-id="a6c4c-290">웹 배포를 사용하고 프로젝트 파일에서 `Microsoft.NET.Sdk.Web`을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-290">Use Web Deploy and reference `Microsoft.NET.Sdk.Web` in the project file.</span></span> <span data-ttu-id="a6c4c-291">*app_offline.htm* 파일은 웹앱 디렉터리의 루트에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-291">An *app_offline.htm* file is placed at the root of the web app directory.</span></span> <span data-ttu-id="a6c4c-292">파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-292">When the file is present, the ASP.NET Core Module gracefully shuts down the app and serves the *app_offline.htm* file during the deployment.</span></span> <span data-ttu-id="a6c4c-293">자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-293">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#app_offlinehtm).</span></span>
* <span data-ttu-id="a6c4c-294">서버의 IIS 관리자에서 앱 풀을 수동으로 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-294">Manually stop the app pool in the IIS Manager on the server.</span></span>
* <span data-ttu-id="a6c4c-295">PowerShell을 사용하여 응용 프로그램 풀을 중지하고 다시 시작합니다(PowerShell 5 이상 필요).</span><span class="sxs-lookup"><span data-stu-id="a6c4c-295">Use PowerShell to stop and restart the app pool (requires PowerShell 5 or later):</span></span>

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

## <a name="data-protection"></a><span data-ttu-id="a6c4c-296">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="a6c4c-296">Data protection</span></span>

<span data-ttu-id="a6c4c-297">[ASP.NET Core 데이터 보호 스택](xref:security/data-protection/index)은 인증에 사용되는 미들웨어를 포함하여 여러 ASP.NET Core [미들웨어](xref:fundamentals/middleware/index)에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-297">The [ASP.NET Core Data Protection stack](xref:security/data-protection/index) is used by several ASP.NET Core [middlewares](xref:fundamentals/middleware/index), including middleware used in authentication.</span></span> <span data-ttu-id="a6c4c-298">사용자 코드에서 데이터 보호 API가 호출되지 않더라도 배포 스크립트 또는 사용자 코드를 통해 영구적 암호화 [키 저장소](xref:security/data-protection/implementation/key-management)를 만들도록 데이터 보호를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-298">Even if Data Protection APIs aren't called by user code, data protection should be configured with a deployment script or in user code to create a persistent cryptographic [key store](xref:security/data-protection/implementation/key-management).</span></span> <span data-ttu-id="a6c4c-299">데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-299">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="a6c4c-300">키 링이 메모리에 저장된 경우 앱을 다시 시작하면 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-300">If the key ring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="a6c4c-301">모든 쿠키 기반 인증 토큰이 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-301">All cookie-based authentication tokens are invalidated.</span></span> 
* <span data-ttu-id="a6c4c-302">사용자는 다음 요청에서 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-302">Users are required to sign in again on their next request.</span></span> 
* <span data-ttu-id="a6c4c-303">키 링으로 보호된 데이터의 암호를 더 이상 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-303">Any data protected with the key ring can no longer be decrypted.</span></span> <span data-ttu-id="a6c4c-304">여기에는 [CSRF 토큰](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) 및 [ASP.NET Core MVC TempData 쿠키](xref:fundamentals/app-state#tempdata)가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-304">This may include [CSRF tokens](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) and [ASP.NET Core MVC TempData cookies](xref:fundamentals/app-state#tempdata).</span></span>

<span data-ttu-id="a6c4c-305">IIS에서 키 링을 저장하도록 데이터 보호를 구성하려면 다음 방법 중 **하나**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-305">To configure data protection under IIS to persist the key ring, use **one** of the following approaches:</span></span>

* <span data-ttu-id="a6c4c-306">**데이터 보호 레지스트리키 만들기**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-306">**Create Data Protection Registry Keys**</span></span>

  <span data-ttu-id="a6c4c-307">ASP.NET 앱에서 사용되는 데이터 보호 키는 앱 외부의 레지스트리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-307">Data protection keys used by ASP.NET Core apps are stored in the registry external to the apps.</span></span> <span data-ttu-id="a6c4c-308">지정된 앱의 키를 저장하려면 앱 풀에 대한 레지스트리 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-308">To persist the keys for a given app, create registry keys for the app pool.</span></span>

  <span data-ttu-id="a6c4c-309">WebFarm이 아닌 독립 실행형 IIS 설치의 경우 [Data Protection Provision-AutoGenKeys.ps1 PowerShell 스크립트](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1)를 ASP.NET Core 앱과 함께 사용되는 각 응용 프로그램 풀에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-309">For standalone, non-webfarm IIS installations, the [Data Protection Provision-AutoGenKeys.ps1 PowerShell script](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1) can be used for each app pool used with an ASP.NET Core app.</span></span> <span data-ttu-id="a6c4c-310">이 스크립트는 앱의 앱 풀 작업자 프로세스 계정만 액세스할 수 있는 HKLM 레지스트리에 레지스트리 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-310">This script creates a registry key in the HKLM registry that's accessible only to the worker process account of the app's app pool.</span></span> <span data-ttu-id="a6c4c-311">미사용 키는 컴퓨터 전체 키가 있는 DPAPI를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-311">Keys are encrypted at rest using DPAPI with a machine-wide key.</span></span>

  <span data-ttu-id="a6c4c-312">웹 팜 시나리오에서는 UNC 경로를 사용하여 데이터 보호 키 링을 저장하도록 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-312">In web farm scenarios, an app can be configured to use a UNC path to store its data protection key ring.</span></span> <span data-ttu-id="a6c4c-313">기본적으로 데이터 보호 키는 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-313">By default, the data protection keys aren't encrypted.</span></span> <span data-ttu-id="a6c4c-314">네트워크 공유에 대한 파일 권한은 앱 실행에 사용되는 Windows 계정으로 제한되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-314">Ensure that the file permissions for the network share are limited to the Windows account the app runs under.</span></span> <span data-ttu-id="a6c4c-315">X509 인증서를 사용하여 미사용 키를 보호할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-315">An X509 certificate can be used to protect keys at rest.</span></span> <span data-ttu-id="a6c4c-316">사용자가 인증서를 업로드할 수 있는 메커니즘을 사용하는 것이 좋습니다. 즉 사용자의 신뢰할 수 있는 인증서 저장소에 인증서를 배치하고, 사용자의 앱이 실행되는 모든 컴퓨터에서 이 인증서를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-316">Consider a mechanism to allow users to upload certificates: Place certificates into the user's trusted certificate store and ensure they're available on all machines where the user's app runs.</span></span> <span data-ttu-id="a6c4c-317">자세한 내용은 [ASP.NET Core 데이터 보호 구성](xref:security/data-protection/configuration/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-317">See [Configure ASP.NET Core Data Protection](xref:security/data-protection/configuration/overview) for details.</span></span>

* <span data-ttu-id="a6c4c-318">**사용자 프로필을 로드하도록 IIS 응용 프로그램 풀 구성**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-318">**Configure the IIS Application Pool to load the user profile**</span></span>

  <span data-ttu-id="a6c4c-319">이 설정은 앱 풀에 대한 **고급 설정** 아래의 **프로세스 모델** 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-319">This setting is in the **Process Model** section under the **Advanced Settings** for the app pool.</span></span> <span data-ttu-id="a6c4c-320">사용자 프로필 로드를 `True`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-320">Set Load User Profile to `True`.</span></span> <span data-ttu-id="a6c4c-321">이렇게 하면 사용자 프로필 디렉터리 아래에 키가 저장되고, 앱 풀에서 사용되는 사용자 계정과 관련된 키로 DPAPI를 사용하여 키가 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-321">This stores keys under the user profile directory and protects them using DPAPI with a key specific to the user account used by the app pool.</span></span>

* <span data-ttu-id="a6c4c-322">**파일 시스템을 키 링 저장소로 사용**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-322">**Use the file system as a key ring store**</span></span>

  <span data-ttu-id="a6c4c-323">[파일 시스템을 키 링 저장소로 사용](xref:security/data-protection/configuration/overview)하도록 앱 코드를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-323">Adjust the app code to [use the file system as a key ring store](xref:security/data-protection/configuration/overview).</span></span> <span data-ttu-id="a6c4c-324">X509 인증서를 사용하여 키 링을 보호하고 신뢰할 수 있는 인증서인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-324">Use an X509 certificate to protect the key ring and ensure the certificate is a trusted certificate.</span></span> <span data-ttu-id="a6c4c-325">자체 서명된 인증서인 경우 신뢰할 수 있는 루트 저장소에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-325">If the certificate is self-signed, place the certificate in the Trusted Root store.</span></span>

  <span data-ttu-id="a6c4c-326">웹 팜에서 IIS를 사용하는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-326">When using IIS in a web farm:</span></span>

  * <span data-ttu-id="a6c4c-327">모든 컴퓨터에서 액세스할 수 있는 파일 공유를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-327">Use a file share that all machines can access.</span></span>
  * <span data-ttu-id="a6c4c-328">각 시스템에 X509 인증서를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-328">Deploy an X509 certificate to each machine.</span></span> <span data-ttu-id="a6c4c-329">[코드에 데이터 보호](xref:security/data-protection/configuration/overview)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-329">Configure [data protection in code](xref:security/data-protection/configuration/overview).</span></span>

* <span data-ttu-id="a6c4c-330">**데이터 보호에 대한 컴퓨터 수준 정책 설정**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-330">**Set a machine-wide policy for data protection**</span></span>

  <span data-ttu-id="a6c4c-331">데이터 보호 시스템은 데이터 보호 API를 사용하는 모든 앱에 대한 기본 [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy) 설정을 제한적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-331">The data protection system has limited support for setting a default [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy) for all apps that consume the Data Protection APIs.</span></span> <span data-ttu-id="a6c4c-332">자세한 내용은 [데이터 보호 문서](xref:security/data-protection/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-332">See the [data protection documentation](xref:security/data-protection/index) for details.</span></span>

## <a name="sub-application-configuration"></a><span data-ttu-id="a6c4c-333">하위 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a6c4c-333">Sub-application configuration</span></span>

<span data-ttu-id="a6c4c-334">루트 앱 아래에 추가된 하위 앱에는 ASP.NET Core 모듈이 처리기로 포함되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-334">Sub-apps added under the root app shouldn't include the ASP.NET Core Module as a handler.</span></span> <span data-ttu-id="a6c4c-335">하위 앱의 *web.config* 파일에 모듈이 처리기로 추가되면, 하위 앱을 찾으려고 할 때 잘못된 구성 파일을 참조하는 *500.19 내부 서버 오류*가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-335">If the module is added as a handler in a sub-app's *web.config* file, a *500.19 Internal Server Error* referencing the faulty config file is received when attempting to browse the sub-app.</span></span>

<span data-ttu-id="a6c4c-336">다음 예제에서는 ASP.NET Core 하위 앱에 대해 게시된 *web.config* 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-336">The following example shows a published *web.config* file for an ASP.NET Core sub-app:</span></span>

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

<span data-ttu-id="a6c4c-337">ASP.NET Core 앱 아래에 비ASP .NET Core 하위 앱을 호스팅하는 경우, 하위 앱의 *web.config* 파일에서 상속된 처리기를 명시적으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-337">When hosting a non-ASP.NET Core sub-app underneath an ASP.NET Core app, explicitly remove the inherited handler in the sub-app *web.config* file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore" />
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="a6c4c-338">ASP.NET Core 모듈을 구성하는 방법에 대한 자세한 내용은 [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module) 항목 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-338">For more information on configuring the ASP.NET Core Module, see the [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic and the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

## <a name="configuration-of-iis-with-webconfig"></a><span data-ttu-id="a6c4c-339">web.config를 사용하여 IIS 구성</span><span class="sxs-lookup"><span data-stu-id="a6c4c-339">Configuration of IIS with web.config</span></span>

<span data-ttu-id="a6c4c-340">IIS 구성은 역방향 프록시 구성에 적용되는 IIS 기능에 대한 *web.config*에 포함된 **\<system.webServer>** 섹션의 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-340">IIS configuration is influenced by the **\<system.webServer>** section of *web.config* for those IIS features that apply to a reverse proxy configuration.</span></span> <span data-ttu-id="a6c4c-341">IIS가 서버 수준에서 동적 압축을 사용하도록 구성된 경우 앱의 *web.config* 파일에 있는 **\<urlCompression>** 요소를 통해 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-341">If IIS is configured at the server level to use dynamic compression, the **\<urlCompression>** element in the app's *web.config* file can disable it.</span></span>

<span data-ttu-id="a6c4c-342">자세한 내용은 [\<system.webServer>에 대한 구성 참조](/iis/configuration/system.webServer/), [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module) 및 [ASP.NET Core와 IIS 모듈](xref:host-and-deploy/iis/modules)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-342">For more information, see the [configuration reference for \<system.webServer>](/iis/configuration/system.webServer/), [ASP.NET Core Module Configuration Reference](xref:host-and-deploy/aspnet-core-module), and [IIS Modules with ASP.NET Core](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="a6c4c-343">격리된 앱 풀에서 실행되는 개별 앱에 대해 환경 변수를 설정하려면(IIS 10.0 이상에서 지원됨), IIS 참조 문서에서 [환경 변수 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목의 *AppCmd.exe 명령* 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-343">To set environment variables for individual apps running in isolated app pools (supported for IIS 10.0 or later), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic in the IIS reference documentation.</span></span>

## <a name="configuration-sections-of-webconfig"></a><span data-ttu-id="a6c4c-344">web.config 구성 섹션</span><span class="sxs-lookup"><span data-stu-id="a6c4c-344">Configuration sections of web.config</span></span>

<span data-ttu-id="a6c4c-345">*web.config*에 있는 ASP.NET 4.x 앱의 구성 섹션은 ASP.NET Core 앱의 구성에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-345">Configuration sections of ASP.NET 4.x apps in *web.config* aren't used by ASP.NET Core apps for configuration:</span></span>

* <span data-ttu-id="a6c4c-346">**\<system.web>**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-346">**\<system.web>**</span></span>
* <span data-ttu-id="a6c4c-347">**\<appSettings>**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-347">**\<appSettings>**</span></span>
* <span data-ttu-id="a6c4c-348">**\<connectionStrings>**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-348">**\<connectionStrings>**</span></span>
* <span data-ttu-id="a6c4c-349">**\<location>**</span><span class="sxs-lookup"><span data-stu-id="a6c4c-349">**\<location>**</span></span>

<span data-ttu-id="a6c4c-350">ASP.NET Core 앱은 다른 구성 공급자를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-350">ASP.NET Core apps are configured using other configuration providers.</span></span> <span data-ttu-id="a6c4c-351">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-351">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="application-pools"></a><span data-ttu-id="a6c4c-352">응용 프로그램 풀</span><span class="sxs-lookup"><span data-stu-id="a6c4c-352">Application Pools</span></span>

<span data-ttu-id="a6c4c-353">서버에서 여러 웹 사이트를 호스트하는 경우 각 앱을 해당 앱 풀에서 실행하여 서로 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-353">When hosting multiple websites on a server, isolate the apps from each other by running each app in its own app pool.</span></span> <span data-ttu-id="a6c4c-354">이 구성은 IIS **웹 사이트 추가** 대화 상자의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-354">The IIS **Add Website** dialog defaults to this configuration.</span></span> <span data-ttu-id="a6c4c-355">**사이트 이름**을 제공하면 해당 텍스트가 자동으로 **응용 프로그램 풀** 텍스트 상자로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-355">When **Site name** is provided, the text is automatically transferred to the **Application pool** textbox.</span></span> <span data-ttu-id="a6c4c-356">사이트를 추가할 때 이 사이트 이름을 사용하여 새로운 앱 풀이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-356">A new app pool is created using the site name when the site is added.</span></span>

## <a name="application-pool-identity"></a><span data-ttu-id="a6c4c-357">응용 프로그램 풀 ID</span><span class="sxs-lookup"><span data-stu-id="a6c4c-357">Application Pool Identity</span></span>

<span data-ttu-id="a6c4c-358">응용 프로그램 풀 ID 계정을 사용하면 도메인 또는 로컬 계정을 만들고 관리할 필요 없이 고유한 계정으로 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-358">An app pool identity account allows an app to run under a unique account without having to create and manage domains or local accounts.</span></span> <span data-ttu-id="a6c4c-359">IIS 8.0 이상에서 IIS WAS(관리 작업자 프로세스)는 새로운 앱 풀의 이름으로 가상 계정을 만들고, 기본적으로 이 계정으로 앱 풀의 작업자 프로세스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-359">On IIS 8.0 or later, the IIS Admin Worker Process (WAS) creates a virtual account with the name of the new app pool and runs the app pool's worker processes under this account by default.</span></span> <span data-ttu-id="a6c4c-360">IIS 관리 콘솔의 응용 프로그램 풀에 대한 **고급 설정** 아래에서 **ID**가 **ApplicationPoolIdentity**를 사용하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-360">In the IIS Management Console under **Advanced Settings** for the app pool, ensure that the **Identity** is set to use **ApplicationPoolIdentity**:</span></span>

![응용 프로그램 풀 고급 설정 대화 상자](index/_static/apppool-identity.png)

<span data-ttu-id="a6c4c-362">IIS 관리 프로세스는 Windows 보안 시스템에 앱 풀 이름이 포함된 보안 식별자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-362">The IIS management process creates a secure identifier with the name of the app pool in the Windows Security System.</span></span> <span data-ttu-id="a6c4c-363">리소스는 이 ID를 사용하여 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-363">Resources can be secured using this identity.</span></span> <span data-ttu-id="a6c4c-364">그러나 이 ID는 실제 사용자 계정이 아니며 Windows 사용자 관리 콘솔에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-364">However, this identity isn't a real user account and doesn't show up in the Windows User Management Console.</span></span>

<span data-ttu-id="a6c4c-365">IIS 작업자 프로세스에서 앱에 대한 높은 액세스 권한이 필요한 경우 앱이 포함된 디렉터리에 대한 ACL(액세스 제어 목록)을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-365">If the IIS worker process requires elevated access to the app, modify the Access Control List (ACL) for the directory containing the app:</span></span>

1. <span data-ttu-id="a6c4c-366">[Windows 탐색기]를 열고 해당 하위 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-366">Open Windows Explorer and navigate to the directory.</span></span>

1. <span data-ttu-id="a6c4c-367">디렉터리를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-367">Right-click on the directory and select **Properties**.</span></span>

1. <span data-ttu-id="a6c4c-368">**보안** 탭 아래에서 **편집** 단추, **추가** 단추를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-368">Under the **Security** tab, select the **Edit** button and then the **Add** button.</span></span>

1. <span data-ttu-id="a6c4c-369">**위치** 단추를 선택하고 시스템이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-369">Select the **Locations** button and make sure the system is selected.</span></span>

1. <span data-ttu-id="a6c4c-370">**선택할 개체 이름 입력** 영역에 **IIS AppPool\\<app_pool_name>** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-370">Enter **IIS AppPool\\<app_pool_name>** in **Enter the object names to select** area.</span></span> <span data-ttu-id="a6c4c-371">**이름 확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-371">Select the **Check Names** button.</span></span> <span data-ttu-id="a6c4c-372">*DefaultAppPool*의 경우 **IIS AppPool\DefaultAppPool**을 사용하는 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-372">For the *DefaultAppPool* check the names using **IIS AppPool\DefaultAppPool**.</span></span> <span data-ttu-id="a6c4c-373">**이름 확인** 단추를 선택하면 개체 이름 영역에 **DefaultAppPool** 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-373">When the **Check Names** button is selected, a value of **DefaultAppPool** is indicated in the object names area.</span></span> <span data-ttu-id="a6c4c-374">개체 이름 영역에 앱 풀 이름을 직접 입력할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-374">It isn't possible to enter the app pool name directly into the object names area.</span></span> <span data-ttu-id="a6c4c-375">개체 이름을 확인할 때는 **IIS AppPool\\<app_pool_name>** 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-375">Use the **IIS AppPool\\<app_pool_name>** format when checking for the object name.</span></span>

   ![앱 폴더에 대한 사용자 또는 그룹 대화 상자 선택: “이름 확인”을 선택하기 전에 개체 이름 영역의 “IIS AppPool\"에 앱 풀 이름 “DefaultAppPool”이 추가됩니다.](index/_static/select-users-or-groups-1.png)

1. <span data-ttu-id="a6c4c-377">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-377">Select **OK**.</span></span>

   ![앱 폴더에 대한 사용자 또는 그룹 대화 상자 선택: “이름 확인”을 선택하면 개체 이름 영역에 개체 이름 “DefaultAppPool”이 표시됩니다.](index/_static/select-users-or-groups-2.png)

1. <span data-ttu-id="a6c4c-379">읽기 및 실행 권한은 기본적으로 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-379">Read &amp; execute permissions should be granted by default.</span></span> <span data-ttu-id="a6c4c-380">필요에 따라 추가 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-380">Provide additional permissions as needed.</span></span>

<span data-ttu-id="a6c4c-381">**ICACLS** 도구를 사용하여 명령 프롬프트에서 액세스 권한을 부여할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-381">Access can also be granted at a command prompt using the **ICACLS** tool.</span></span> <span data-ttu-id="a6c4c-382">*DefaultAppPool*을 예로 들면, 다음 명령이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-382">Using the *DefaultAppPool* as an example, the following command is used:</span></span>

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

<span data-ttu-id="a6c4c-383">자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-383">For more information, see the [icacls](/windows-server/administration/windows-commands/icacls) topic.</span></span>

## <a name="deployment-resources-for-iis-administrators"></a><span data-ttu-id="a6c4c-384">IIS 관리자를 위한 배포 리소스</span><span class="sxs-lookup"><span data-stu-id="a6c4c-384">Deployment resources for IIS administrators</span></span>

<span data-ttu-id="a6c4c-385">IIS 설명서에서 IIS에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-385">Learn about IIS in-depth in the IIS documentation.</span></span>  
[<span data-ttu-id="a6c4c-386">IIS 설명서</span><span class="sxs-lookup"><span data-stu-id="a6c4c-386">IIS documentation</span></span>](/iis)

<span data-ttu-id="a6c4c-387">.NET Core 앱 배포 모델에 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-387">Learn about .NET Core app deployment models.</span></span>  
[<span data-ttu-id="a6c4c-388">.NET Core 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="a6c4c-388">.NET Core application deployment</span></span>](/dotnet/core/deploying/)

<span data-ttu-id="a6c4c-389">ASP.NET Core 모듈이 Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 어떻게 사용하도록 허용하는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-389">Learn how the ASP.NET Core Module allows the Kestrel web server to use IIS or IIS Express as a reverse proxy server.</span></span>  
[<span data-ttu-id="a6c4c-390">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="a6c4c-390">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)

<span data-ttu-id="a6c4c-391">ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-391">Learn how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span>  
[<span data-ttu-id="a6c4c-392">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="a6c4c-392">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)

<span data-ttu-id="a6c4c-393">게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-393">Learn about the directory structure of published ASP.NET Core apps.</span></span>  
[<span data-ttu-id="a6c4c-394">디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="a6c4c-394">Directory structure</span></span>](xref:host-and-deploy/directory-structure)

<span data-ttu-id="a6c4c-395">ASP.NET Core 앱용 활성 및 비활성 IIS 모듈과 IIS 모듈을 관리하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-395">Discover active and inactive IIS modules for ASP.NET Core apps and how to manage IIS modules.</span></span>  
[<span data-ttu-id="a6c4c-396">IIS 모듈</span><span class="sxs-lookup"><span data-stu-id="a6c4c-396">IIS modules</span></span>](xref:host-and-deploy/iis/troubleshoot)

<span data-ttu-id="a6c4c-397">ASP.NET Core 앱의 IIS 배포에 대한 문제 진단 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-397">Learn how to diagnose problems with IIS deployments of ASP.NET Core apps.</span></span>  
[<span data-ttu-id="a6c4c-398">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a6c4c-398">Troubleshoot</span></span>](xref:host-and-deploy/iis/troubleshoot)

<span data-ttu-id="a6c4c-399">IIS에서 ASP.NET Core 앱을 호스팅할 때 일반적인 오류를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="a6c4c-399">Distinguish common errors when hosting ASP.NET Core apps on IIS.</span></span>  
[<span data-ttu-id="a6c4c-400">Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="a6c4c-400">Common errors reference for Azure App Service and IIS</span></span>](xref:host-and-deploy/azure-iis-errors-reference)

## <a name="additional-resources"></a><span data-ttu-id="a6c4c-401">추가 자료</span><span class="sxs-lookup"><span data-stu-id="a6c4c-401">Additional resources</span></span>

* [<span data-ttu-id="a6c4c-402">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="a6c4c-402">Introduction to ASP.NET Core</span></span>](xref:index)
* [<span data-ttu-id="a6c4c-403">공식 Microsoft IIS 사이트</span><span class="sxs-lookup"><span data-stu-id="a6c4c-403">The Official Microsoft IIS Site</span></span>](https://www.iis.net/)
* [<span data-ttu-id="a6c4c-404">Windows Server 기술 콘텐츠 라이브러리</span><span class="sxs-lookup"><span data-stu-id="a6c4c-404">Windows Server technical content library</span></span>](/windows-server/windows-server)
