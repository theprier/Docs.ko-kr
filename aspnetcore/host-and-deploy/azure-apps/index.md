---
title: Azure App Service에 ASP.NET Core 앱 배포
author: guardrex
description: 이 문서에는 Azure 호스트 및 배포 리소스의 링크가 포함됩니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 12/10/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: b6ff2124aac7e866f630cf359cbd188e88906844
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284697"
---
# <a name="deploy-aspnet-core-apps-to-azure-app-service"></a><span data-ttu-id="ed2b2-103">Azure App Service에 ASP.NET Core 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ed2b2-103">Deploy ASP.NET Core apps to Azure App Service</span></span>

<span data-ttu-id="ed2b2-104">[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="ed2b2-105">유용한 리소스</span><span class="sxs-lookup"><span data-stu-id="ed2b2-105">Useful resources</span></span>

<span data-ttu-id="ed2b2-106">Azure [Web Apps 설명서](/azure/app-service/)는 Azure 앱 설명서, 샘플, 방법 가이드 및 기타 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="ed2b2-107">ASP.NET Core 앱 호스트와 관련하여 두 가지 주목할 만한 자습서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="ed2b2-108">빠른 시작: Azure에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ed2b2-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="ed2b2-109">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 Windows의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="ed2b2-110">빠른 시작: Linux의 App Service에서 .NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ed2b2-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="ed2b2-111">명령줄을 사용하여 ASP.NET Core 웹앱을 만들고 Linux의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="ed2b2-112">다음 문서는 ASP.NET Core 설명서에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-112">The following articles are available in ASP.NET Core documentation:</span></span>

<xref:tutorials/publish-to-azure-webapp-using-vs>  
<span data-ttu-id="ed2b2-113">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-113">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

<xref:host-and-deploy/azure-apps/azure-continuous-deployment>  
<span data-ttu-id="ed2b2-114">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-114">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="ed2b2-115">Azure Pipelines를 사용하여 첫 번째 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="ed2b2-115">Create your first pipeline with Azure Pipelines</span></span>](/azure/devops/pipelines/get-started-yaml)  
<span data-ttu-id="ed2b2-116">ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-116">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="ed2b2-117">Azure Web App 샌드박스</span><span class="sxs-lookup"><span data-stu-id="ed2b2-117">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="ed2b2-118">Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-118">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="ed2b2-119">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ed2b2-119">Application configuration</span></span>

### <a name="platform"></a><span data-ttu-id="ed2b2-120">플랫폼</span><span class="sxs-lookup"><span data-stu-id="ed2b2-120">Platform</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="ed2b2-121">64비트(x64) 및 32비트(x86) 앱은 Azure App Service에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-121">Runtimes for 64-bit (x64) and 32-bit (x86) apps are present on Azure App Service.</span></span> <span data-ttu-id="ed2b2-122">App Service에서 사용 가능한 [.NET Core SDK](/dotnet/core/sdk)는 32비트이지만 [Kudu](https://github.com/projectkudu/kudu/wiki) 콘솔 또는 [Visual Studio 게시 프로필이나 CLI 명령을 사용하는 MSDeploy](xref:host-and-deploy/visual-studio-publish-profiles)를 통해 64비트 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-122">The [.NET Core SDK](/dotnet/core/sdk) available on App Service is 32-bit, but you can deploy 64-bit apps using the [Kudu](https://github.com/projectkudu/kudu/wiki) console or via [MSDeploy with a Visual Studio publish profile or CLI command](xref:host-and-deploy/visual-studio-publish-profiles).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="ed2b2-123">원시 종속 항목을 지원하는 앱의 경우 32비트(x86) 앱의 런타임이 Azure App Service에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-123">For apps with native dependencies, runtimes for 32-bit (x86) apps are present on Azure App Service.</span></span> <span data-ttu-id="ed2b2-124">App Service에서 사용 가능한 [.NET Core SDK](/dotnet/core/sdk)는 32비트입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-124">The [.NET Core SDK](/dotnet/core/sdk) available on App Service is 32-bit.</span></span>

::: moniker-end

### <a name="packages"></a><span data-ttu-id="ed2b2-125">패키지</span><span class="sxs-lookup"><span data-stu-id="ed2b2-125">Packages</span></span>

<span data-ttu-id="ed2b2-126">Azure App Service에 배포된 앱에 대한 자동 로깅 기능을 제공하려면 다음 NuGet 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-126">Include the following NuGet packages to provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="ed2b2-127">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 강화 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-127">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) to provide ASP.NET Core light-up integration with Azure App Service.</span></span> <span data-ttu-id="ed2b2-128">추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-128">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="ed2b2-129">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-129">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="ed2b2-130">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-130">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

<span data-ttu-id="ed2b2-131">이전의 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-131">The preceding packages aren't available from the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="ed2b2-132">.NET Framework를 대상으로 하거나 `Microsoft.AspNetCore.App` 메타패키지를 참조하는 앱은 앱 프로젝트 파일의 개별 패키지를 명시적으로 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-132">Apps that target .NET Framework or reference the `Microsoft.AspNetCore.App` metapackage must explicitly reference the individual packages in the app's project file.</span></span>

## <a name="override-app-configuration-using-the-azure-portal"></a><span data-ttu-id="ed2b2-133">Azure Portal을 사용하여 앱 구성 재정의</span><span class="sxs-lookup"><span data-stu-id="ed2b2-133">Override app configuration using the Azure Portal</span></span>

<span data-ttu-id="ed2b2-134">Azure Portal의 앱 설정을 사용하면 앱의 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-134">App settings in the Azure Portal permit you to set environment variables for the app.</span></span> <span data-ttu-id="ed2b2-135">환경 변수는 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-135">Environment variables can be consumed by the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="ed2b2-136">Azure Portal에서 앱 설정을 만들거나 수정하고**저장** 단추를 선택하면 Azure 앱이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-136">When an app setting is created or modified in the Azure Portal and the **Save** button is selected, the Azure App is restarted.</span></span> <span data-ttu-id="ed2b2-137">서비스를 다시 시작한 후에 환경 변수를 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-137">The environment variable is available to the app after the service restarts.</span></span>

<span data-ttu-id="ed2b2-138">앱이 [웹 호스트](xref:fundamentals/host/web-host)를 사용하고 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 사용하여 호스트를 빌드하는 경우 호스트를 구성하는 환경 변수는 `ASPNETCORE_` 접두사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-138">When an app uses the [Web Host](xref:fundamentals/host/web-host) and builds the host using [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), environment variables that configure the host use the `ASPNETCORE_` prefix.</span></span> <span data-ttu-id="ed2b2-139">자세한 내용은 <xref:fundamentals/host/web-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-139">For more information, see <xref:fundamentals/host/web-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="ed2b2-140">앱이 [일반 호스트](xref:fundamentals/host/generic-host)를 사용하는 경우에는 기본적으로 환경 변수가 앱 구성으로 로드되지 않으며 개발자가 구성 공급자를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-140">When an app uses the [Generic Host](xref:fundamentals/host/generic-host), environment variables aren't loaded into an app's configuration by default and the configuration provider must be added by the developer.</span></span> <span data-ttu-id="ed2b2-141">개발자가 구성 공급자를 추가할 때 환경 변수 접두사를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-141">The developer determines the environment variable prefix when the configuration provider is added.</span></span> <span data-ttu-id="ed2b2-142">자세한 내용은 <xref:fundamentals/host/generic-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-142">For more information, see <xref:fundamentals/host/generic-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="ed2b2-143">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="ed2b2-143">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="ed2b2-144">체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-144">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="ed2b2-145">추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-145">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="ed2b2-146">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-146">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="ed2b2-147">모니터링 및 로깅</span><span class="sxs-lookup"><span data-stu-id="ed2b2-147">Monitoring and logging</span></span>

<span data-ttu-id="ed2b2-148">App Service에 배포된 ASP.NET Core 앱은 자동으로 App Service 확장인 **ASP.NET Core 로깅 확장**을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-148">ASP.NET Core apps deployed to App Service automatically receive an App Service extension, **ASP.NET Core Logging Extensions**.</span></span> <span data-ttu-id="ed2b2-149">이 확장은 Azure 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-149">The extension enables Azure logging.</span></span>

<span data-ttu-id="ed2b2-150">모니터링, 로깅 및 문제 해결에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-150">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="ed2b2-151">방법: Azure App Service에서 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="ed2b2-151">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="ed2b2-152">앱 및 App Service 계획의 할당량 및 메트릭을 검토하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-152">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="ed2b2-153">Azure App Service에서 웹앱에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="ed2b2-153">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="ed2b2-154">HTTP 상태 코드, 실패한 요청 및 웹 서버 활동에 대한 진단 로깅을 활성화하고 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-154">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

<xref:fundamentals/error-handling>  
<span data-ttu-id="ed2b2-155">ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-155">Understand common approaches to handling errors in ASP.NET Core apps.</span></span>

<xref:host-and-deploy/azure-apps/troubleshoot>  
<span data-ttu-id="ed2b2-156">ASP.NET Core 앱을 사용하는 Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-156">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

<xref:host-and-deploy/azure-iis-errors-reference>  
<span data-ttu-id="ed2b2-157">Azure App Service/IIS에서 호스트하는 앱의 일반적인 배포 구성 오류와 문제 해결에 대한 조언을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-157">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="ed2b2-158">데이터 보호 키 링 및 배포 슬롯</span><span class="sxs-lookup"><span data-stu-id="ed2b2-158">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="ed2b2-159">[데이터 보호 키](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-159">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="ed2b2-160">이 폴더는 네트워크 저장소에서 지원하고, 앱을 호스트하는 모든 컴퓨터에서 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-160">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="ed2b2-161">저장된 키는 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-161">Keys aren't protected at rest.</span></span> <span data-ttu-id="ed2b2-162">이 폴더는 단일 배포 슬롯에 앱의 모든 인스턴스에 대한 키 링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-162">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="ed2b2-163">준비 및 프로덕션과 같은 별도의 배포 슬롯은 키 링을 공유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-163">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="ed2b2-164">배포 슬롯을 바꿀 경우 데이터 보호를 사용하는 모든 시스템은 이전 슬롯 내에 있는 키 링을 사용하여 저장된 데이터의 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-164">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="ed2b2-165">ASP.NET 쿠키 미들웨어는 데이터 보호를 사용하여 쿠키를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-165">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="ed2b2-166">이로 인해 표준 ASP.NET 쿠키 미들웨어를 사용하는 앱에서 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-166">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="ed2b2-167">슬롯에 관계없는 키 링 솔루션의 경우 다음과 같은 외부 키 링 공급자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-167">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="ed2b2-168">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="ed2b2-168">Azure Blob Storage</span></span>
* <span data-ttu-id="ed2b2-169">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ed2b2-169">Azure Key Vault</span></span>
* <span data-ttu-id="ed2b2-170">SQL 저장소</span><span class="sxs-lookup"><span data-stu-id="ed2b2-170">SQL store</span></span>
* <span data-ttu-id="ed2b2-171">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="ed2b2-171">Redis cache</span></span>

<span data-ttu-id="ed2b2-172">자세한 내용은 <xref:security/data-protection/implementation/key-storage-providers>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-172">For more information, see <xref:security/data-protection/implementation/key-storage-providers>.</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="ed2b2-173">Azure App Service에 ASP.NET Core 미리 보기 릴리스 배포</span><span class="sxs-lookup"><span data-stu-id="ed2b2-173">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="ed2b2-174">다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-174">Use one of the following approaches:</span></span>

* <span data-ttu-id="ed2b2-175">[미리 보기 사이트 확장을 설치](#install-the-preview-site-extension)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-175">[Install the preview site extension](#install-the-preview-site-extension).</span></span>
* <span data-ttu-id="ed2b2-176">[자체 포함된 앱을 배포](#deploy-the-app-self-contained)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-176">[Deploy the app self-contained](#deploy-the-app-self-contained).</span></span>
* <span data-ttu-id="ed2b2-177">[Web Apps for Containers에서 Docker를 사용](#use-docker-with-web-apps-for-containers)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-177">[Use Docker with Web Apps for containers](#use-docker-with-web-apps-for-containers).</span></span>

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="ed2b2-178">미리 보기 사이트 확장 설치</span><span class="sxs-lookup"><span data-stu-id="ed2b2-178">Install the preview site extension</span></span>

<span data-ttu-id="ed2b2-179">미리 보기 사이트 확장을 사용하는 데 문제가 발생하는 경우 [GitHub](https://github.com/aspnet/azureintegration/issues/new)에서 문제를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-179">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

1. <span data-ttu-id="ed2b2-180">Azure Portal에서 App Service로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-180">From the Azure Portal, navigate to the App Service.</span></span>
1. <span data-ttu-id="ed2b2-181">웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-181">Select the web app.</span></span>
1. <span data-ttu-id="ed2b2-182">검색 상자에 "ex"를 입력하여 "확장"으로 필터링하거나 관리 도구 목록을 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-182">Type "ex" in the search box to filter for "Extensions" or scroll down the list of management tools.</span></span>
1. <span data-ttu-id="ed2b2-183">**확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-183">Select **Extensions**.</span></span>
1. <span data-ttu-id="ed2b2-184">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-184">Select **Add**.</span></span>
1. <span data-ttu-id="ed2b2-185">목록에서 **ASP.NET Core {X.Y}({x64|x86}) 런타임** 확장을 선택합니다. 여기서 `{X.Y}`는 ASP.NET Core 미리 보기 버전이며 `{x64|x86}`은 플랫폼을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-185">Select the **ASP.NET Core {X.Y} ({x64|x86}) Runtime** extension from the list, where `{X.Y}` is the ASP.NET Core preview version and `{x64|x86}` specifies the platform.</span></span>
1. <span data-ttu-id="ed2b2-186">**확인**을 선택하여 적합한 조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-186">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="ed2b2-187">확장을 설치하려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-187">Select **OK** to install the extension.</span></span>

<span data-ttu-id="ed2b2-188">작업이 완료되면 최신.NET Core 미리 보기가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-188">When the operation completes, the latest .NET Core preview is installed.</span></span> <span data-ttu-id="ed2b2-189">설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-189">Verify the installation:</span></span>

1. <span data-ttu-id="ed2b2-190">**고급 도구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-190">Select **Advanced Tools**.</span></span>
1. <span data-ttu-id="ed2b2-191">**고급 도구**에서 **Go**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-191">Select **Go** in **Advanced Tools**.</span></span>
1. <span data-ttu-id="ed2b2-192">**디버그 콘솔** > **PowerShell** 메뉴 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-192">Select the **Debug console** > **PowerShell** menu item.</span></span>
1. <span data-ttu-id="ed2b2-193">PowerShell 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-193">At the PowerShell prompt, execute the following command.</span></span> <span data-ttu-id="ed2b2-194">명령에서 `{X.Y}`를 ASP.NET Core 런타임 버전으로 대체하고, `{PLATFORM}`을 플랫폼으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-194">Substitute the ASP.NET Core runtime version for `{X.Y}` and the platform for `{PLATFORM}` in the command:</span></span>

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.{X.Y}.{PLATFORM}\
   ```
   <span data-ttu-id="ed2b2-195">x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-195">The command returns `True` when the x64 preview runtime is installed.</span></span>

> [!NOTE]
> <span data-ttu-id="ed2b2-196">A 시리즈 컴퓨팅 또는 더 나은 호스트 계층에서 호스트되는 앱이 필요한 경우 Azure Portal의 앱 설정에서 App Services 앱의 플랫폼 아키텍처(x86/x64)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-196">The platform architecture (x86/x64) of an App Services app is set in the app's settings in the Azure Portal for apps that are hosted on an A-series compute or better hosting tier.</span></span> <span data-ttu-id="ed2b2-197">앱이 in-process 모드에서 실행되고 플랫폼 아키텍처가 64비트(x64)에 대해 구성되는 경우 ASP.NET Core 모듈은 64비트 미리 보기 런타임을 사용합니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="ed2b2-197">If the app is run in in-process mode and the platform architecture is configured for 64-bit (x64), the ASP.NET Core Module uses the 64-bit preview runtime, if present.</span></span> <span data-ttu-id="ed2b2-198">**ASP.NET Core {X.Y}(x64) 런타임** 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-198">Install the **ASP.NET Core {X.Y} (x64) Runtime** extension.</span></span>
>
> <span data-ttu-id="ed2b2-199">x64 미리 보기 런타임을 설치한 후에 Kudu PowerShell 명령 창에서 다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-199">After installing the x64 preview runtime, run the following command in the Kudu PowerShell command window to verify the installation.</span></span> <span data-ttu-id="ed2b2-200">명령에서 `{X.Y}`에 대한 ASP.NET Core 런타임 버전을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-200">Substitute the ASP.NET Core runtime version for `{X.Y}` in the command:</span></span>
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.{X.Y}.x64\
> ```
> <span data-ttu-id="ed2b2-201">x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-201">The command returns `True` when the x64 preview runtime is installed.</span></span>

> [!NOTE]
> <span data-ttu-id="ed2b2-202">**ASP.NET Core 확장**을 사용하면 Azure 로깅을 사용하는 등 Azure App Services에서 ASP.NET Core에 대한 추가 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-202">**ASP.NET Core Extensions** enables additional functionality for ASP.NET Core on Azure App Services, such as enabling Azure logging.</span></span> <span data-ttu-id="ed2b2-203">Visual Studio에서 배포할 경우 확장은 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-203">The extension is installed automatically when deploying from Visual Studio.</span></span> <span data-ttu-id="ed2b2-204">확장이 설치되지 않은 경우 앱에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-204">If the extension isn't installed, install it for the app.</span></span>

<span data-ttu-id="ed2b2-205">**ARM 템플릿에서 미리 보기 사이트 확장 사용**</span><span class="sxs-lookup"><span data-stu-id="ed2b2-205">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="ed2b2-206">ARM 템플릿을 사용하여 앱을 만들고 배포하는 경우 `siteextensions` 리소스 형식을 사용하여 웹앱에 사이트 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-206">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="ed2b2-207">예:</span><span class="sxs-lookup"><span data-stu-id="ed2b2-207">For example:</span></span>

[!code-json[](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a><span data-ttu-id="ed2b2-208">자체 포함된 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ed2b2-208">Deploy the app self-contained</span></span>

<span data-ttu-id="ed2b2-209">미리 보기 런타임을 대상으로 하는 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)는 배포 시 미리 보기 런타임을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-209">A [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) that targets a preview runtime carries the preview runtime in the deployment.</span></span>

<span data-ttu-id="ed2b2-210">자체 포함된 앱을 배포하는 경우:</span><span class="sxs-lookup"><span data-stu-id="ed2b2-210">When deploying a self-contained app:</span></span>

* <span data-ttu-id="ed2b2-211">Azure App Service의 사이트에는 [미리 보기 사이트 확장](#install-the-preview-site-extension)이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-211">The site in Azure App Service doesn't require the [preview site extension](#install-the-preview-site-extension).</span></span>
* <span data-ttu-id="ed2b2-212">앱은 [FDD(프레임워크 종속 배포)](/dotnet/core/deploying#framework-dependent-deployments-fdd)에 대해 게시할 때와 다른 접근 방식으로 공개해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-212">The app must be published following a different approach than when publishing for a [framework-dependent deployment (FDD)](/dotnet/core/deploying#framework-dependent-deployments-fdd).</span></span>

#### <a name="publish-from-visual-studio"></a><span data-ttu-id="ed2b2-213">Visual Studio에서 게시</span><span class="sxs-lookup"><span data-stu-id="ed2b2-213">Publish from Visual Studio</span></span>

1. <span data-ttu-id="ed2b2-214">Visual Studio 도구 모음에서 **빌드** > **{응용 프로그램 이름} 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-214">Select **Build** > **Publish {Application Name}** from the Visual Studio toolbar.</span></span>
1. <span data-ttu-id="ed2b2-215">**공개 대상 선택** 대화 상자에서 **App Service**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-215">In the **Pick a publish target** dialog, confirm that **App Service** is selected.</span></span>
1. <span data-ttu-id="ed2b2-216">**고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-216">Select **Advanced**.</span></span> <span data-ttu-id="ed2b2-217">**게시** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-217">The **Publish** dialog opens.</span></span>
1. <span data-ttu-id="ed2b2-218">**게시** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="ed2b2-218">In the **Publish** dialog:</span></span>
   * <span data-ttu-id="ed2b2-219">**릴리스** 구성이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-219">Confirm that the **Release** configuration is selected.</span></span>
   * <span data-ttu-id="ed2b2-220">**배포 모드** 드롭다운 목록을 열고 **자체 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-220">Open the **Deployment Mode** drop-down list and select **Self-Contained**.</span></span>
   * <span data-ttu-id="ed2b2-221">**대상 런타임** 드롭다운 목록에서 대상 런타임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-221">Select the target runtime from the **Target Runtime** drop-down list.</span></span> <span data-ttu-id="ed2b2-222">기본값은 `win-x86`입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-222">The default is `win-x86`.</span></span>
   * <span data-ttu-id="ed2b2-223">배포 시 추가 파일을 제거해야 하는 경우 **파일 게시 옵션**을 열고 대상에서 추가 파일을 제거하는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-223">If you need to remove additional files upon deployment, open **File Publish Options** and select the check box to remove additional files at the destination.</span></span>
   * <span data-ttu-id="ed2b2-224">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-224">Select **Save**.</span></span>
1. <span data-ttu-id="ed2b2-225">게시 마법사의 나머지 프롬프트를 따라 새 사이트를 작성하거나 기존 사이트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-225">Create a new site or update an existing site by following the remaining prompts of the publish wizard.</span></span>

#### <a name="publish-using-command-line-interface-cli-tools"></a><span data-ttu-id="ed2b2-226">CLI(명령줄 인터페이스) 도구를 사용하여 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-226">Publish using command-line interface (CLI) tools</span></span>

1. <span data-ttu-id="ed2b2-227">프로젝트 파일에서 하나 이상의 [RID(런타임 ID)](/dotnet/core/rid-catalog)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-227">In the project file, specify one or more [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog).</span></span> <span data-ttu-id="ed2b2-228">단일 RID에 `<RuntimeIdentifier>`(단수)을 사용하거나, `<RuntimeIdentifiers>`(복수)를 사용하여 세미콜론으로 구분된 RID 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-228">Use `<RuntimeIdentifier>` (singular) for a single RID, or use `<RuntimeIdentifiers>` (plural) to provide a semicolon-delimited list of RIDs.</span></span> <span data-ttu-id="ed2b2-229">다음 예제에서는 `win-x86` RID가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-229">In the following example, the `win-x86` RID is specified:</span></span>

   ```xml
   <PropertyGroup>
     <TargetFramework>netcoreapp2.1</TargetFramework>
     <RuntimeIdentifier>win-x86</RuntimeIdentifier>
   </PropertyGroup>
   ```
1. <span data-ttu-id="ed2b2-230">명령 셸에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 사용하여 호스트의 런타임에 대한 릴리스 구성에 있는 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-230">From a command shell, publish the app in Release configuration for the host's runtime with the [dotnet publish](/dotnet/core/tools/dotnet-publish) command.</span></span> <span data-ttu-id="ed2b2-231">다음 예제에서 앱은 `win-x86` RID에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-231">In the following example, the app is published for the `win-x86` RID.</span></span> <span data-ttu-id="ed2b2-232">`--runtime` 옵션에 제공된 RID를 프로젝트 파일의 `<RuntimeIdentifier>`(또는 `<RuntimeIdentifiers>`) 속성에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-232">The RID supplied to the `--runtime` option must be provided in the `<RuntimeIdentifier>` (or `<RuntimeIdentifiers>`) property in the project file.</span></span>

   ```console
   dotnet publish --configuration Release --runtime win-x86
   ```
1. <span data-ttu-id="ed2b2-233">*bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish* 디렉터리의 콘텐츠를 App Service의 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-233">Move the contents of the *bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish* directory to the site in App Service.</span></span>

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="ed2b2-234">Web Apps for Containers에서 Docker 사용</span><span class="sxs-lookup"><span data-stu-id="ed2b2-234">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="ed2b2-235">[Docker 허브](https://hub.docker.com/r/microsoft/aspnetcore/)에는 최신 미리 보기 Docker 이미지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-235">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest preview Docker images.</span></span> <span data-ttu-id="ed2b2-236">이미지는 기본 이미지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-236">The images can be used as a base image.</span></span> <span data-ttu-id="ed2b2-237">이미지를 사용하고 일반적으로 Web App for Containers에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-237">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="protocol-settings-https"></a><span data-ttu-id="ed2b2-238">프로토콜 설정(HTTPS)</span><span class="sxs-lookup"><span data-stu-id="ed2b2-238">Protocol settings (HTTPS)</span></span>

<span data-ttu-id="ed2b2-239">보안 프로토콜 바인딩을 사용하면 HTTPS를 통한 요청에 응답할 때 사용할 인증서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-239">Secure protocol bindings allow you specify a certificate to use when responding to requests over HTTPS.</span></span> <span data-ttu-id="ed2b2-240">바인딩을 위해서는 특정 호스트 이름에 대해 발행된 유효한 개인 인증서(*.pfx*)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-240">Binding requires a valid private certificate (*.pfx*) issued for the specific hostname.</span></span> <span data-ttu-id="ed2b2-241">자세한 내용은 [자습서: 기존 사용자 지정 SSL 인증서를 Azure Web Apps에 바인딩](/azure/app-service/app-service-web-tutorial-custom-ssl)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-241">For more information, see [Tutorial: Bind an existing custom SSL certificate to Azure Web Apps](/azure/app-service/app-service-web-tutorial-custom-ssl).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed2b2-242">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ed2b2-242">Additional resources</span></span>

* [<span data-ttu-id="ed2b2-243">Web Apps 개요(5분 개요 동영상)</span><span class="sxs-lookup"><span data-stu-id="ed2b2-243">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="ed2b2-244">Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 동영상)</span><span class="sxs-lookup"><span data-stu-id="ed2b2-244">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="ed2b2-245">Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 동영상)</span><span class="sxs-lookup"><span data-stu-id="ed2b2-245">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="ed2b2-246">Azure App Service 진단 개요</span><span class="sxs-lookup"><span data-stu-id="ed2b2-246">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

<span data-ttu-id="ed2b2-247">Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-247">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="ed2b2-248">다음 항목은 기본 IIS 기술과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2b2-248">The following topics pertain to the underlying IIS technology:</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [<span data-ttu-id="ed2b2-249">Microsoft TechNet 라이브러리: Windows Server</span><span class="sxs-lookup"><span data-stu-id="ed2b2-249">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
