---
title: Azure App Service에 ASP.NET Core 앱 배포
author: guardrex
description: 이 문서에는 Azure 호스트 및 배포 리소스의 링크가 포함됩니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: c55a5202643bb947b3f38f67aec55ee5cf7b1496
ms.sourcegitcommit: c43a6f1fe72d7c2db4b5815fd532f2b45d964e07
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244751"
---
# <a name="deploy-aspnet-core-apps-to-azure-app-service"></a><span data-ttu-id="7cac3-103">Azure App Service에 ASP.NET Core 앱 배포</span><span class="sxs-lookup"><span data-stu-id="7cac3-103">Deploy ASP.NET Core apps to Azure App Service</span></span>

<span data-ttu-id="7cac3-104">[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="7cac3-105">유용한 리소스</span><span class="sxs-lookup"><span data-stu-id="7cac3-105">Useful resources</span></span>

<span data-ttu-id="7cac3-106">Azure [Web Apps 설명서](/azure/app-service/)는 Azure 앱 설명서, 샘플, 방법 가이드 및 기타 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="7cac3-107">ASP.NET Core 앱 호스트와 관련하여 두 가지 주목할 만한 자습서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="7cac3-108">빠른 시작: Azure에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7cac3-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="7cac3-109">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 Windows의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="7cac3-110">빠른 시작: Linux의 App Service에서 .NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7cac3-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="7cac3-111">명령줄을 사용하여 ASP.NET Core 웹앱을 만들고 Linux의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="7cac3-112">다음 문서는 ASP.NET Core 설명서에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-112">The following articles are available in ASP.NET Core documentation:</span></span>

<xref:tutorials/publish-to-azure-webapp-using-vs>  
<span data-ttu-id="7cac3-113">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-113">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

<xref:host-and-deploy/azure-apps/azure-continuous-deployment>  
<span data-ttu-id="7cac3-114">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-114">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="7cac3-115">Azure Pipelines를 사용하여 첫 번째 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="7cac3-115">Create your first pipeline with Azure Pipelines</span></span>](/azure/devops/pipelines/get-started-yaml)  
<span data-ttu-id="7cac3-116">ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-116">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="7cac3-117">Azure Web App 샌드박스</span><span class="sxs-lookup"><span data-stu-id="7cac3-117">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="7cac3-118">Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-118">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="application-configuration"></a><span data-ttu-id="7cac3-119">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="7cac3-119">Application configuration</span></span>

<span data-ttu-id="7cac3-120">다음 NuGet 패키지는 Azure App Service에 배포된 앱에 대한 자동 로깅 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-120">The following NuGet packages provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="7cac3-121">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 강화 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-121">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) to provide ASP.NET Core light-up integration with Azure App Service.</span></span> <span data-ttu-id="7cac3-122">추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-122">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="7cac3-123">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-123">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="7cac3-124">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-124">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

<span data-ttu-id="7cac3-125">.NET Core를 대상으로 지정하고 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)를 참조하는 경우 이전 패키지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-125">If targeting .NET Core and referencing the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage), the preceding packages are included.</span></span> <span data-ttu-id="7cac3-126">패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-126">The packages are absent from the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="7cac3-127">.NET Framework를 대상으로 지정하거나 `Microsoft.AspNetCore.App` 메타패키지를 참조하는 경우 개별 로깅 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-127">If targeting .NET Framework or referencing the `Microsoft.AspNetCore.App` metapackage, reference the individual logging packages.</span></span>

::: moniker-end

## <a name="override-app-configuration-using-the-azure-portal"></a><span data-ttu-id="7cac3-128">Azure Portal을 사용하여 앱 구성 재정의</span><span class="sxs-lookup"><span data-stu-id="7cac3-128">Override app configuration using the Azure Portal</span></span>

<span data-ttu-id="7cac3-129">**응용 프로그램 설정** 블레이드의 **앱 설정** 영역에서는 앱의 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-129">The **App Settings** area of the **Application settings** blade permits you to set environment variables for the app.</span></span> <span data-ttu-id="7cac3-130">환경 변수는 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-130">Environment variables can be consumed by the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="7cac3-131">Azure Portal에서 앱 설정을 만들거나 수정하고**저장** 단추를 선택하면 Azure 앱이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-131">When an app setting is created or modified in the Azure Portal and the **Save** button is selected, the Azure App is restarted.</span></span> <span data-ttu-id="7cac3-132">서비스를 다시 시작한 후에 환경 변수를 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-132">The environment variable is available to the app after the service restarts.</span></span>

<span data-ttu-id="7cac3-133">앱이 [웹 호스트](xref:fundamentals/host/web-host)를 사용하고 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 사용하여 호스트를 빌드하는 경우 호스트를 구성하는 환경 변수는 `ASPNETCORE_` 접두사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-133">When an app uses the [Web Host](xref:fundamentals/host/web-host) and builds the host using [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), environment variables that configure the host use the `ASPNETCORE_` prefix.</span></span> <span data-ttu-id="7cac3-134">자세한 내용은 <xref:fundamentals/host/web-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-134">For more information, see <xref:fundamentals/host/web-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="7cac3-135">앱이 [일반 호스트](xref:fundamentals/host/generic-host)를 사용하는 경우에는 기본적으로 환경 변수가 앱 구성으로 로드되지 않으며 개발자가 구성 공급자를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-135">When an app uses the [Generic Host](xref:fundamentals/host/generic-host), environment variables aren't loaded into an app's configuration by default and the configuration provider must be added by the developer.</span></span> <span data-ttu-id="7cac3-136">개발자가 구성 공급자를 추가할 때 환경 변수 접두사를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-136">The developer determines the environment variable prefix when the configuration provider is added.</span></span> <span data-ttu-id="7cac3-137">자세한 내용은 <xref:fundamentals/host/generic-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-137">For more information, see <xref:fundamentals/host/generic-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="7cac3-138">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="7cac3-138">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="7cac3-139">체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-139">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="7cac3-140">추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-140">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="7cac3-141">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-141">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="7cac3-142">모니터링 및 로깅</span><span class="sxs-lookup"><span data-stu-id="7cac3-142">Monitoring and logging</span></span>

<span data-ttu-id="7cac3-143">모니터링, 로깅 및 문제 해결에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-143">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="7cac3-144">방법: Azure App Service에서 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="7cac3-144">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="7cac3-145">앱 및 App Service 계획의 할당량 및 메트릭을 검토하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-145">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="7cac3-146">Azure App Service에서 웹앱에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="7cac3-146">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="7cac3-147">HTTP 상태 코드, 실패한 요청 및 웹 서버 활동에 대한 진단 로깅을 활성화하고 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-147">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

<xref:fundamentals/error-handling>  
<span data-ttu-id="7cac3-148">ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-148">Understand common approaches to handling errors in ASP.NET Core apps.</span></span>

<xref:host-and-deploy/azure-apps/troubleshoot>  
<span data-ttu-id="7cac3-149">ASP.NET Core 앱을 사용하는 Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-149">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

<xref:host-and-deploy/azure-iis-errors-reference>  
<span data-ttu-id="7cac3-150">Azure App Service/IIS에서 호스트하는 앱의 일반적인 배포 구성 오류와 문제 해결에 대한 조언을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-150">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="7cac3-151">데이터 보호 키 링 및 배포 슬롯</span><span class="sxs-lookup"><span data-stu-id="7cac3-151">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="7cac3-152">[데이터 보호 키](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-152">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="7cac3-153">이 폴더는 네트워크 저장소에서 지원하고, 앱을 호스트하는 모든 컴퓨터에서 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-153">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="7cac3-154">저장된 키는 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-154">Keys aren't protected at rest.</span></span> <span data-ttu-id="7cac3-155">이 폴더는 단일 배포 슬롯에 앱의 모든 인스턴스에 대한 키 링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-155">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="7cac3-156">준비 및 프로덕션과 같은 별도의 배포 슬롯은 키 링을 공유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-156">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="7cac3-157">배포 슬롯을 바꿀 경우 데이터 보호를 사용하는 모든 시스템은 이전 슬롯 내에 있는 키 링을 사용하여 저장된 데이터의 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-157">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="7cac3-158">ASP.NET 쿠키 미들웨어는 데이터 보호를 사용하여 쿠키를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-158">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="7cac3-159">이로 인해 표준 ASP.NET 쿠키 미들웨어를 사용하는 앱에서 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-159">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="7cac3-160">슬롯에 관계없는 키 링 솔루션의 경우 다음과 같은 외부 키 링 공급자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-160">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="7cac3-161">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="7cac3-161">Azure Blob Storage</span></span>
* <span data-ttu-id="7cac3-162">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="7cac3-162">Azure Key Vault</span></span>
* <span data-ttu-id="7cac3-163">SQL 저장소</span><span class="sxs-lookup"><span data-stu-id="7cac3-163">SQL store</span></span>
* <span data-ttu-id="7cac3-164">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="7cac3-164">Redis cache</span></span>

<span data-ttu-id="7cac3-165">자세한 내용은 <xref:security/data-protection/implementation/key-storage-providers>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-165">For more information, see <xref:security/data-protection/implementation/key-storage-providers>.</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="7cac3-166">Azure App Service에 ASP.NET Core 미리 보기 릴리스 배포</span><span class="sxs-lookup"><span data-stu-id="7cac3-166">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="7cac3-167">다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-167">Use one of the following approaches:</span></span>

* <span data-ttu-id="7cac3-168">[미리 보기 사이트 확장을 설치](#install-the-preview-site-extension)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-168">[Install the preview site extension](#install-the-preview-site-extension).</span></span>
* <span data-ttu-id="7cac3-169">[자체 포함된 앱을 배포](#deploy-the-app-self-contained)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-169">[Deploy the app self-contained](#deploy-the-app-self-contained).</span></span>
* <span data-ttu-id="7cac3-170">[Web Apps for Containers에서 Docker를 사용](#use-docker-with-web-apps-for-containers)합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-170">[Use Docker with Web Apps for containers](#use-docker-with-web-apps-for-containers).</span></span>

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="7cac3-171">미리 보기 사이트 확장 설치</span><span class="sxs-lookup"><span data-stu-id="7cac3-171">Install the preview site extension</span></span>

<span data-ttu-id="7cac3-172">미리 보기 사이트 확장을 사용하는 데 문제가 발생하는 경우 [GitHub](https://github.com/aspnet/azureintegration/issues/new)에서 문제를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-172">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

1. <span data-ttu-id="7cac3-173">Azure Portal에서 App Service 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-173">From the Azure Portal, navigate to the App Service blade.</span></span>
1. <span data-ttu-id="7cac3-174">웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-174">Select the web app.</span></span>
1. <span data-ttu-id="7cac3-175">검색 상자에 "ex"를 입력하거나 관리 섹션 목록을 **개발 도구** 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-175">Type "ex" in the search box or scroll down the list of management sections to **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="7cac3-176">**개발 도구** > **확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-176">Select **DEVELOPMENT TOOLS** > **Extensions**.</span></span>
1. <span data-ttu-id="7cac3-177">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-177">Select **Add**.</span></span>
1. <span data-ttu-id="7cac3-178">목록에서 **ASP.NET Core &lt;x.y&gt;(x86) 런타임** 확장을 선택합니다. 여기서 `<x.y>`는 ASP.NET Core 미리 보기 버전입니다(예: **ASP.NET Core 2.2(x86) 런타임**).</span><span class="sxs-lookup"><span data-stu-id="7cac3-178">Select the **ASP.NET Core &lt;x.y&gt; (x86) Runtime** extension from the list, where `<x.y>` is the ASP.NET Core preview version (for example, **ASP.NET Core 2.2 (x86) Runtime**).</span></span> <span data-ttu-id="7cac3-179">x86 런타임은ASP.NET Core 모듈에 의해 호스트되는 out-of-process를 사용하는 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-179">The x86 runtime is appropriate for [framework-dependent deployments](/dotnet/core/deploying/#framework-dependent-deployments-fdd) that rely on out-of-process hosting by the ASP.NET Core Module.</span></span>
1. <span data-ttu-id="7cac3-180">**확인**을 선택하여 적합한 조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-180">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="7cac3-181">확장을 설치하려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-181">Select **OK** to install the extension.</span></span>

<span data-ttu-id="7cac3-182">작업이 완료되면 최신.NET Core 미리 보기가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-182">When the operation completes, the latest .NET Core preview is installed.</span></span> <span data-ttu-id="7cac3-183">설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-183">Verify the installation:</span></span>

1. <span data-ttu-id="7cac3-184">**개발 도구** 아래에서 **고급 도구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-184">Select **Advanced Tools** under **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="7cac3-185">**고급 도구** 블레이드에서 **이동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-185">Select **Go** on the **Advanced Tools** blade.</span></span>
1. <span data-ttu-id="7cac3-186">**디버그 콘솔** > **PowerShell** 메뉴 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-186">Select the **Debug console** > **PowerShell** menu item.</span></span>
1. <span data-ttu-id="7cac3-187">PowerShell 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-187">At the PowerShell prompt, execute the following command.</span></span> <span data-ttu-id="7cac3-188">명령에서 `<x.y>`에 대한 ASP.NET Core 런타임 버전을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-188">Substitute the ASP.NET Core runtime version for `<x.y>` in the command:</span></span>

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x86\
   ```
   <span data-ttu-id="7cac3-189">설치된 미리 보기 런타임이 ASP.NET Core 2.2용인 경우 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-189">If the installed preview runtime is for ASP.NET Core 2.2, the command is:</span></span>
   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x86\
   ```
   <span data-ttu-id="7cac3-190">x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-190">The command returns `True` when the x64 preview runtime is installed.</span></span>

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> <span data-ttu-id="7cac3-191">App Services 앱의 플랫폼 아키텍처(x86/x64)를 A 시리즈 계산 또는 더 나은 호스트 계층에서 호스트되는 앱에 대한 **일반 설정** 아래의 **응용 프로그램 설정** 블레이드에서 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-191">The platform architecture (x86/x64) of an App Services app is set in the **Application Settings** blade under **General Settings** for apps that are hosted on an A-series compute or better hosting tier.</span></span> <span data-ttu-id="7cac3-192">앱이 in-process 모드에서 실행되고 플랫폼 아키텍처가 64비트(x64)에 대해 구성되는 경우 ASP.NET Core 모듈은 64비트 미리 보기 런타임을 사용합니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="7cac3-192">If the app is run in in-process mode and the platform architecture is configured for 64-bit (x64), the ASP.NET Core Module uses the 64-bit preview runtime, if present.</span></span> <span data-ttu-id="7cac3-193">**ASP.NET Core &lt;x.y&gt;(x64) 런타임** 확장을 설치합니다(예: **ASP.NET Core 2.2(x64) 런타임**).</span><span class="sxs-lookup"><span data-stu-id="7cac3-193">Install the **ASP.NET Core &lt;x.y&gt; (x64) Runtime** extension (for example, **ASP.NET Core 2.2 (x64) Runtime**).</span></span>
>
> <span data-ttu-id="7cac3-194">x64 미리 보기 런타임을 설치한 후에 Kudu PowerShell 명령 창에서 다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-194">After installing the x64 preview runtime, run the following command in the Kudu PowerShell command window to verify the installation.</span></span> <span data-ttu-id="7cac3-195">명령에서 `<x.y>`에 대한 ASP.NET Core 런타임 버전을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-195">Substitute the ASP.NET Core runtime version for `<x.y>` in the command:</span></span>
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x64\
> ```
> <span data-ttu-id="7cac3-196">설치된 미리 보기 런타임이 ASP.NET Core 2.2용인 경우 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-196">If the installed preview runtime is for ASP.NET Core 2.2, the command is:</span></span>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x64\
> ```
> <span data-ttu-id="7cac3-197">x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-197">The command returns `True` when the x64 preview runtime is installed.</span></span>

::: moniker-end

> [!NOTE]
> <span data-ttu-id="7cac3-198">**ASP.NET Core 확장**을 사용하면 Azure 로깅을 사용하는 등 Azure App Services에서 ASP.NET Core에 대한 추가 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-198">**ASP.NET Core Extensions** enables additional functionality for ASP.NET Core on Azure App Services, such as enabling Azure logging.</span></span> <span data-ttu-id="7cac3-199">Visual Studio에서 배포할 경우 확장은 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-199">The extension is installed automatically when deploying from Visual Studio.</span></span> <span data-ttu-id="7cac3-200">확장이 설치되지 않은 경우 앱에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-200">If the extension isn't installed, install it for the app.</span></span>

<span data-ttu-id="7cac3-201">**ARM 템플릿에서 미리 보기 사이트 확장 사용**</span><span class="sxs-lookup"><span data-stu-id="7cac3-201">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="7cac3-202">ARM 템플릿을 사용하여 앱을 만들고 배포하는 경우 `siteextensions` 리소스 형식을 사용하여 웹앱에 사이트 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-202">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="7cac3-203">예:</span><span class="sxs-lookup"><span data-stu-id="7cac3-203">For example:</span></span>

[!code-json[](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a><span data-ttu-id="7cac3-204">자체 포함된 앱 배포</span><span class="sxs-lookup"><span data-stu-id="7cac3-204">Deploy the app self-contained</span></span>

<span data-ttu-id="7cac3-205">미리 보기 런타임을 대상으로 하는 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)는 배포 시 미리 보기 런타임을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-205">A [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) that targets a preview runtime carries the preview runtime in the deployment.</span></span>

<span data-ttu-id="7cac3-206">자체 포함된 앱을 배포하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7cac3-206">When deploying a self-contained app:</span></span>

* <span data-ttu-id="7cac3-207">Azure App Service의 사이트에는 [미리 보기 사이트 확장](#install-the-preview-site-extension)이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-207">The site in Azure App Service doesn't require the [preview site extension](#install-the-preview-site-extension).</span></span>
* <span data-ttu-id="7cac3-208">앱은 [FDD(프레임워크 종속 배포)](/dotnet/core/deploying#framework-dependent-deployments-fdd)에 대해 게시할 때와 다른 접근 방식으로 공개해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-208">The app must be published following a different approach than when publishing for a [framework-dependent deployment (FDD)](/dotnet/core/deploying#framework-dependent-deployments-fdd).</span></span>

#### <a name="publish-from-visual-studio"></a><span data-ttu-id="7cac3-209">Visual Studio에서 게시</span><span class="sxs-lookup"><span data-stu-id="7cac3-209">Publish from Visual Studio</span></span>

1. <span data-ttu-id="7cac3-210">Visual Studio 도구 모음에서 **빌드** > **{응용 프로그램 이름} 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-210">Select **Build** > **Publish {Application Name}** from the Visual Studio toolbar.</span></span>
1. <span data-ttu-id="7cac3-211">**공개 대상 선택** 대화 상자에서 **App Service**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-211">In the **Pick a publish target** dialog, confirm that **App Service** is selected.</span></span>
1. <span data-ttu-id="7cac3-212">**고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-212">Select **Advanced**.</span></span> <span data-ttu-id="7cac3-213">**게시** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-213">The **Publish** dialog opens.</span></span>
1. <span data-ttu-id="7cac3-214">**게시** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="7cac3-214">In the **Publish** dialog:</span></span>
   * <span data-ttu-id="7cac3-215">**릴리스** 구성이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-215">Confirm that the **Release** configuration is selected.</span></span>
   * <span data-ttu-id="7cac3-216">**배포 모드** 드롭다운 목록을 열고 **자체 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-216">Open the **Deployment Mode** drop-down list and select **Self-Contained**.</span></span>
   * <span data-ttu-id="7cac3-217">**대상 런타임** 드롭다운 목록에서 대상 런타임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-217">Select the target runtime from the **Target Runtime** drop-down list.</span></span> <span data-ttu-id="7cac3-218">기본값은 `win-x86`입니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-218">The default is `win-x86`.</span></span>
   * <span data-ttu-id="7cac3-219">배포 시 추가 파일을 제거해야 하는 경우 **파일 게시 옵션**을 열고 대상에서 추가 파일을 제거하는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-219">If you need to remove additional files upon deployment, open **File Publish Options** and select the check box to remove additional files at the destination.</span></span>
   * <span data-ttu-id="7cac3-220">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-220">Select **Save**.</span></span>
1. <span data-ttu-id="7cac3-221">게시 마법사의 나머지 프롬프트를 따라 새 사이트를 작성하거나 기존 사이트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-221">Create a new site or update an existing site by following the remaining prompts of the publish wizard.</span></span>

#### <a name="publish-using-command-line-interface-cli-tools"></a><span data-ttu-id="7cac3-222">CLI(명령줄 인터페이스) 도구를 사용하여 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-222">Publish using command-line interface (CLI) tools</span></span>

1. <span data-ttu-id="7cac3-223">프로젝트 파일에서 하나 이상의 [RID(런타임 ID)](/dotnet/core/rid-catalog)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-223">In the project file, specify one or more [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog).</span></span> <span data-ttu-id="7cac3-224">단일 RID에 `<RuntimeIdentifier>`(단수)을 사용하거나, `<RuntimeIdentifiers>`(복수)를 사용하여 세미콜론으로 구분된 RID 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-224">Use `<RuntimeIdentifier>` (singular) for a single RID, or use `<RuntimeIdentifiers>` (plural) to provide a semicolon-delimited list of RIDs.</span></span> <span data-ttu-id="7cac3-225">다음 예제에서는 `win-x86` RID가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-225">In the following example, the `win-x86` RID is specified:</span></span>

   ```xml
   <PropertyGroup>
     <TargetFramework>netcoreapp2.1</TargetFramework>
     <RuntimeIdentifier>win-x86</RuntimeIdentifier>
   </PropertyGroup>
   ```
1. <span data-ttu-id="7cac3-226">명령 셸에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 사용하여 호스트의 런타임에 대한 릴리스 구성에 있는 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-226">From a command shell, publish the app in Release configuration for the host's runtime with the [dotnet publish](/dotnet/core/tools/dotnet-publish) command.</span></span> <span data-ttu-id="7cac3-227">다음 예제에서 앱은 `win-x86` RID에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-227">In the following example, the app is published for the `win-x86` RID.</span></span> <span data-ttu-id="7cac3-228">`--runtime` 옵션에 제공된 RID를 프로젝트 파일의 `<RuntimeIdentifier>`(또는 `<RuntimeIdentifiers>`) 속성에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-228">The RID supplied to the `--runtime` option must be provided in the `<RuntimeIdentifier>` (or `<RuntimeIdentifiers>`) property in the project file.</span></span>

   ```console
   dotnet publish --configuration Release --runtime win-x86
   ```
1. <span data-ttu-id="7cac3-229">*bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish* 디렉터리의 콘텐츠를 App Service의 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-229">Move the contents of the *bin/Release/{TARGET FRAMEWORK}/{RUNTIME IDENTIFIER}/publish* directory to the site in App Service.</span></span>

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="7cac3-230">Web Apps for Containers에서 Docker 사용</span><span class="sxs-lookup"><span data-stu-id="7cac3-230">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="7cac3-231">[Docker 허브](https://hub.docker.com/r/microsoft/aspnetcore/)에는 최신 미리 보기 Docker 이미지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-231">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest preview Docker images.</span></span> <span data-ttu-id="7cac3-232">이미지는 기본 이미지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-232">The images can be used as a base image.</span></span> <span data-ttu-id="7cac3-233">이미지를 사용하고 일반적으로 Web App for Containers에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-233">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="protocol-settings-https"></a><span data-ttu-id="7cac3-234">프로토콜 설정(HTTPS)</span><span class="sxs-lookup"><span data-stu-id="7cac3-234">Protocol settings (HTTPS)</span></span>

<span data-ttu-id="7cac3-235">보안 프로토콜 바인딩을 사용하면 HTTPS를 통한 요청에 응답할 때 사용할 인증서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-235">Secure protocol bindings allow you specify a certificate to use when responding to requests over HTTPS.</span></span> <span data-ttu-id="7cac3-236">바인딩을 위해서는 특정 호스트 이름에 대해 발행된 유효한 개인 인증서(*.pfx*)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-236">Binding requires a valid private certificate (*.pfx*) issued for the specific hostname.</span></span> <span data-ttu-id="7cac3-237">자세한 내용은 [자습서: 기존 사용자 지정 SSL 인증서를 Azure Web Apps에 바인딩](/azure/app-service/app-service-web-tutorial-custom-ssl)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cac3-237">For more information, see [Tutorial: Bind an existing custom SSL certificate to Azure Web Apps](/azure/app-service/app-service-web-tutorial-custom-ssl).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7cac3-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7cac3-238">Additional resources</span></span>

* [<span data-ttu-id="7cac3-239">Web Apps 개요(5분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="7cac3-239">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="7cac3-240">Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="7cac3-240">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="7cac3-241">Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 비디오)</span><span class="sxs-lookup"><span data-stu-id="7cac3-241">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="7cac3-242">Azure App Service 진단 개요</span><span class="sxs-lookup"><span data-stu-id="7cac3-242">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

<span data-ttu-id="7cac3-243">Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-243">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="7cac3-244">다음 항목은 기본 IIS 기술과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cac3-244">The following topics pertain to the underlying IIS technology:</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [<span data-ttu-id="7cac3-245">Microsoft TechNet 라이브러리: Windows Server</span><span class="sxs-lookup"><span data-stu-id="7cac3-245">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
