---
title: Azure App Service에서 ASP.NET Core 호스트
author: guardrex
description: 유용한 리소스에 대한 링크를 통해 Azure App Service에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 08/29/2018
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: 23289823e154d93e4bedd23a1efae0e58c71eae0
ms.sourcegitcommit: 57eccdea7d89a62989272f71aad655465f1c600a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44340188"
---
# <a name="host-aspnet-core-on-azure-app-service"></a><span data-ttu-id="33c4e-103">Azure App Service에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="33c4e-103">Host ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="33c4e-104">[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="33c4e-105">유용한 리소스</span><span class="sxs-lookup"><span data-stu-id="33c4e-105">Useful resources</span></span>

<span data-ttu-id="33c4e-106">Azure [Web Apps 설명서](/azure/app-service/)는 Azure 앱 설명서, 샘플, 방법 가이드 및 기타 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="33c4e-107">ASP.NET Core 앱 호스트와 관련하여 두 가지 주목할 만한 자습서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="33c4e-108">빠른 시작: Azure에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="33c4e-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="33c4e-109">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 Windows의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="33c4e-110">빠른 시작: Linux의 App Service에서 .NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="33c4e-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="33c4e-111">명령줄을 사용하여 ASP.NET Core 웹앱을 만들고 Linux의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="33c4e-112">다음 문서는 ASP.NET Core 설명서에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="33c4e-113">Visual Studio를 사용하여 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="33c4e-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="33c4e-114">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="33c4e-115">CLI 도구를 사용하여 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="33c4e-115">Publish to Azure with CLI tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli)  
<span data-ttu-id="33c4e-116">Git 명령줄 클라이언트를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-116">Learn how to publish an ASP.NET Core app to Azure App Service using the Git command-line client.</span></span>

[<span data-ttu-id="33c4e-117">Visual Studio 및 Git을 사용하여 Azure에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="33c4e-117">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="33c4e-118">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-118">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="33c4e-119">Azure Pipelines를 사용하여 첫 번째 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="33c4e-119">Create your first pipeline with Azure Pipelines</span></span>](/azure/devops/pipelines/get-started-yaml)  
<span data-ttu-id="33c4e-120">ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-120">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="33c4e-121">Azure Web App 샌드박스</span><span class="sxs-lookup"><span data-stu-id="33c4e-121">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="33c4e-122">Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-122">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="application-configuration"></a><span data-ttu-id="33c4e-123">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="33c4e-123">Application configuration</span></span>

<span data-ttu-id="33c4e-124">ASP.NET Core 2.0 이상에서 다음 NuGet 패키지는 Azure App Service에 배포된 앱에 대한 자동 로깅 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-124">In ASP.NET Core 2.0 or later, the following NuGet packages provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="33c4e-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 강화 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) to provide ASP.NET Core light-up integration with Azure App Service.</span></span> <span data-ttu-id="33c4e-126">추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-126">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="33c4e-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="33c4e-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

<span data-ttu-id="33c4e-129">.NET Core를 대상으로 지정하고 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)를 참조하는 경우 패키지가 이미 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-129">If targeting .NET Core and referencing the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage), the packages are already included.</span></span> <span data-ttu-id="33c4e-130">패키지는 최신 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-130">The packages are absent from the newer [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="33c4e-131">.NET Framework를 대상으로 지정하거나 `Microsoft.AspNetCore.App` 메타패키지를 참조하는 경우 개별 로깅 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-131">If targeting .NET Framework or referencing the `Microsoft.AspNetCore.App` metapackage, reference the individual logging packages.</span></span>

::: moniker-end

## <a name="override-app-configuration-using-the-azure-portal"></a><span data-ttu-id="33c4e-132">Azure Portal을 사용하여 앱 구성 재정의</span><span class="sxs-lookup"><span data-stu-id="33c4e-132">Override app configuration using the Azure Portal</span></span>

<span data-ttu-id="33c4e-133">**응용 프로그램 설정** 블레이드의 **앱 설정** 영역에서는 앱의 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-133">The **App Settings** area of the **Application settings** blade permits you to set environment variables for the app.</span></span> <span data-ttu-id="33c4e-134">환경 변수는 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-134">Environment variables can be consumed by the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="33c4e-135">앱이 [웹 호스트](xref:fundamentals/host/web-host)를 사용하고 [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 사용하여 호스트를 빌드하는 경우 호스트를 구성하는 환경 변수는 `ASPNETCORE_` 접두사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-135">When an app uses the [Web Host](xref:fundamentals/host/web-host) and builds the host using [WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), environment variables that configure the host use the `ASPNETCORE_` prefix.</span></span> <span data-ttu-id="33c4e-136">자세한 내용은 <xref:fundamentals/host/web-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33c4e-136">For more information, see <xref:fundamentals/host/web-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

<span data-ttu-id="33c4e-137">앱이 [일반 호스트](xref:fundamentals/host/generic-host)를 사용하는 경우에는 기본적으로 환경 변수가 앱 구성으로 로드되지 않으며 개발자가 구성 공급자를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-137">When an app uses the [Generic Host](xref:fundamentals/host/generic-host), environment variables aren't loaded into an app's configuration by default and the configuration provider must be added by the developer.</span></span> <span data-ttu-id="33c4e-138">개발자가 구성 공급자를 추가할 때 환경 변수 접두사를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-138">The developer determines the environment variable prefix when the configuration provider is added.</span></span> <span data-ttu-id="33c4e-139">자세한 내용은 <xref:fundamentals/host/generic-host> 및 [환경 변수 구성 공급자](xref:fundamentals/configuration/index#environment-variables-configuration-provider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33c4e-139">For more information, see <xref:fundamentals/host/generic-host> and the [Environment Variables Configuration Provider](xref:fundamentals/configuration/index#environment-variables-configuration-provider).</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="33c4e-140">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="33c4e-140">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="33c4e-141">체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-141">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="33c4e-142">추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-142">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="33c4e-143">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33c4e-143">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="33c4e-144">모니터링 및 로깅</span><span class="sxs-lookup"><span data-stu-id="33c4e-144">Monitoring and logging</span></span>

<span data-ttu-id="33c4e-145">모니터링, 로깅 및 문제 해결에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33c4e-145">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="33c4e-146">방법: Azure App Service에서 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="33c4e-146">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="33c4e-147">앱 및 App Service 계획의 할당량 및 메트릭을 검토하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-147">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="33c4e-148">Azure App Service에서 웹앱에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="33c4e-148">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="33c4e-149">HTTP 상태 코드, 실패한 요청 및 웹 서버 활동에 대한 진단 로깅을 활성화하고 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-149">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="33c4e-150">ASP.NET Core의 오류 처리 소개</span><span class="sxs-lookup"><span data-stu-id="33c4e-150">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="33c4e-151">ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-151">Understand common approaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="33c4e-152">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="33c4e-152">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="33c4e-153">ASP.NET Core 앱을 사용하는 Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-153">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="33c4e-154">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="33c4e-154">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="33c4e-155">Azure App Service/IIS에서 호스트하는 앱의 일반적인 배포 구성 오류와 문제 해결에 대한 조언을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33c4e-155">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="33c4e-156">데이터 보호 키 링 및 배포 슬롯</span><span class="sxs-lookup"><span data-stu-id="33c4e-156">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="33c4e-157">[데이터 보호 키](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-157">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="33c4e-158">이 폴더는 네트워크 저장소에서 지원하고, 앱을 호스트하는 모든 컴퓨터에서 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-158">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="33c4e-159">저장된 키는 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-159">Keys aren't protected at rest.</span></span> <span data-ttu-id="33c4e-160">이 폴더는 단일 배포 슬롯에 앱의 모든 인스턴스에 대한 키 링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-160">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="33c4e-161">준비 및 프로덕션과 같은 별도의 배포 슬롯은 키 링을 공유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-161">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="33c4e-162">배포 슬롯을 바꿀 경우 데이터 보호를 사용하는 모든 시스템은 이전 슬롯 내에 있는 키 링을 사용하여 저장된 데이터의 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-162">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="33c4e-163">ASP.NET 쿠키 미들웨어는 데이터 보호를 사용하여 쿠키를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-163">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="33c4e-164">이로 인해 표준 ASP.NET 쿠키 미들웨어를 사용하는 앱에서 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-164">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="33c4e-165">슬롯에 관계없는 키 링 솔루션의 경우 다음과 같은 외부 키 링 공급자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="33c4e-165">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="33c4e-166">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="33c4e-166">Azure Blob Storage</span></span>
* <span data-ttu-id="33c4e-167">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="33c4e-167">Azure Key Vault</span></span>
* <span data-ttu-id="33c4e-168">SQL 저장소</span><span class="sxs-lookup"><span data-stu-id="33c4e-168">SQL store</span></span>
* <span data-ttu-id="33c4e-169">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="33c4e-169">Redis cache</span></span>

<span data-ttu-id="33c4e-170">자세한 내용은 [키 저장소 공급자](xref:security/data-protection/implementation/key-storage-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33c4e-170">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="33c4e-171">Azure App Service에 ASP.NET Core 미리 보기 릴리스 배포</span><span class="sxs-lookup"><span data-stu-id="33c4e-171">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="33c4e-172">다음과 같은 방법으로 Azure App Service에 ASP.NET Core 미리 보기 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-172">ASP.NET Core preview apps can be deployed to Azure App Service with the following approaches:</span></span>

* <span data-ttu-id="33c4e-173">[미리 보기 사이트 확장 설치](#install-the-preview-site-extension)
<!-- * [Deploy the app self-contained](#deploy-the-app-self-contained) --></span><span class="sxs-lookup"><span data-stu-id="33c4e-173">[Install the preview site extension](#install-the-preview-site-extension)
<!-- * [Deploy the app self-contained](#deploy-the-app-self-contained) --></span></span>
* [<span data-ttu-id="33c4e-174">Web Apps for Containers에서 Docker 사용</span><span class="sxs-lookup"><span data-stu-id="33c4e-174">Use Docker with Web Apps for containers</span></span>](#use-docker-with-web-apps-for-containers)

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="33c4e-175">미리 보기 사이트 확장 설치</span><span class="sxs-lookup"><span data-stu-id="33c4e-175">Install the preview site extension</span></span>

<span data-ttu-id="33c4e-176">미리 보기 사이트 확장을 사용하는 데 문제가 발생하는 경우 [GitHub](https://github.com/aspnet/azureintegration/issues/new)에서 문제를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-176">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

1. <span data-ttu-id="33c4e-177">Azure Portal에서 App Service 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-177">From the Azure portal, navigate to the App Service blade.</span></span>
1. <span data-ttu-id="33c4e-178">웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-178">Select the web app.</span></span>
1. <span data-ttu-id="33c4e-179">검색 상자에 "ex"를 입력하거나 관리 섹션 목록을 **개발 도구** 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-179">Type "ex" in the search box or scroll down the list of management sections to **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="33c4e-180">**개발 도구** > **확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-180">Select **DEVELOPMENT TOOLS** > **Extensions**.</span></span>
1. <span data-ttu-id="33c4e-181">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-181">Select **Add**.</span></span>
1. <span data-ttu-id="33c4e-182">목록에서 **ASP.NET Core &lt;x.y&gt;(x86) 런타임** 확장을 선택합니다. 여기서 `<x.y>`는 ASP.NET Core 미리 보기 버전입니다(예: **ASP.NET Core 2.2(x86) 런타임**).</span><span class="sxs-lookup"><span data-stu-id="33c4e-182">Select the **ASP.NET Core &lt;x.y&gt; (x86) Runtime** extension from the list, where `<x.y>` is the ASP.NET Core preview version (for example, **ASP.NET Core 2.2 (x86) Runtime**).</span></span> <span data-ttu-id="33c4e-183">x86 런타임은ASP.NET Core 모듈에 의해 호스트되는 out-of-process를 사용하는 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-183">The x86 runtime is appropriate for [framework-dependent deployments](/dotnet/core/deploying/#framework-dependent-deployments-fdd) that rely on out-of-process hosting by the ASP.NET Core Module.</span></span>
1. <span data-ttu-id="33c4e-184">**확인**을 선택하여 적합한 조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-184">Select **OK** to accept the legal terms.</span></span>
1. <span data-ttu-id="33c4e-185">확장을 설치하려면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-185">Select **OK** to install the extension.</span></span>

<span data-ttu-id="33c4e-186">작업이 완료되면 최신.NET Core 미리 보기가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-186">When the operation completes, the latest .NET Core preview is installed.</span></span> <span data-ttu-id="33c4e-187">설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-187">Verify the installation:</span></span>

1. <span data-ttu-id="33c4e-188">**개발 도구** 아래에서 **고급 도구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-188">Select **Advanced Tools** under **DEVELOPMENT TOOLS**.</span></span>
1. <span data-ttu-id="33c4e-189">**고급 도구** 블레이드에서 **이동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-189">Select **Go** on the **Advanced Tools** blade.</span></span>
1. <span data-ttu-id="33c4e-190">**디버그 콘솔** > **PowerShell** 메뉴 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-190">Select the **Debug console** > **PowerShell** menu item.</span></span>
1. <span data-ttu-id="33c4e-191">PowerShell 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-191">At the PowerShell prompt, execute the following command.</span></span> <span data-ttu-id="33c4e-192">명령에서 `<x.y>`에 대한 ASP.NET Core 런타임 버전을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-192">Substitute the ASP.NET Core runtime version for `<x.y>` in the command:</span></span>

   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x86\
   ```
   <span data-ttu-id="33c4e-193">설치된 미리 보기 런타임이 ASP.NET Core 2.2용인 경우 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-193">If the installed preview runtime is for ASP.NET Core 2.2, the command is:</span></span>
   ```powershell
   Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x86\
   ```
   <span data-ttu-id="33c4e-194">x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-194">The command returns `True` when the x64 preview runtime is installed.</span></span>

::: moniker range=">= aspnetcore-2.2"

> [!NOTE]
> <span data-ttu-id="33c4e-195">App Services 앱의 플랫폼 아키텍처(x86/x64)를 A 시리즈 계산 또는 더 나은 호스트 계층에서 호스트되는 앱에 대한 **일반 설정** 아래의 **응용 프로그램 설정** 블레이드에서 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-195">The platform architecture (x86/x64) of an App Services app is set in the **Application Settings** blade under **General Settings** for apps that are hosted on an A-series compute or better hosting tier.</span></span> <span data-ttu-id="33c4e-196">앱이 in-process 모드에서 실행되고 플랫폼 아키텍처가 64비트(x64)에 대해 구성되는 경우 ASP.NET Core 모듈은 64비트 미리 보기 런타임을 사용합니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="33c4e-196">If the app is run in in-process mode and the platform architecture is configured for 64-bit (x64), the ASP.NET Core Module uses the 64-bit preview runtime, if present.</span></span> <span data-ttu-id="33c4e-197">**ASP.NET Core &lt;x.y&gt;(x64) 런타임** 확장을 설치합니다(예: **ASP.NET Core 2.2(x64) 런타임**).</span><span class="sxs-lookup"><span data-stu-id="33c4e-197">Install the **ASP.NET Core &lt;x.y&gt; (x64) Runtime** extension (for example, **ASP.NET Core 2.2 (x64) Runtime**).</span></span>
>
> <span data-ttu-id="33c4e-198">x64 미리 보기 런타임을 설치한 후에 Kudu PowerShell 명령 창에서 다음 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-198">After installing the x64 preview runtime, run the following command in the Kudu PowerShell command window to verify the installation.</span></span> <span data-ttu-id="33c4e-199">명령에서 `<x.y>`에 대한 ASP.NET Core 런타임 버전을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-199">Substitute the ASP.NET Core runtime version for `<x.y>` in the command:</span></span>
>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.<x.y>.x64\
> ```
> <span data-ttu-id="33c4e-200">설치된 미리 보기 런타임이 ASP.NET Core 2.2용인 경우 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-200">If the installed preview runtime is for ASP.NET Core 2.2, the command is:</span></span>
> ```powershell
> Test-Path D:\home\SiteExtensions\AspNetCoreRuntime.2.2.x64\
> ```
> <span data-ttu-id="33c4e-201">x64 미리 보기 런타임이 설치된 경우 명령이 `True`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-201">The command returns `True` when the x64 preview runtime is installed.</span></span>

::: moniker-end

> [!NOTE]
> <span data-ttu-id="33c4e-202">**ASP.NET Core 확장**을 사용하면 Azure 로깅을 사용하는 등 Azure App Services에서 ASP.NET Core에 대한 추가 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-202">**ASP.NET Core Extensions** enables additional functionality for ASP.NET Core on Azure App Services, such as enabling Azure logging.</span></span> <span data-ttu-id="33c4e-203">Visual Studio에서 배포할 경우 확장은 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-203">The extension is installed automatically when deploying from Visual Studio.</span></span> <span data-ttu-id="33c4e-204">확장이 설치되지 않은 경우 앱에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-204">If the extension isn't installed, install it for the app.</span></span>

<span data-ttu-id="33c4e-205">**ARM 템플릿에서 미리 보기 사이트 확장 사용**</span><span class="sxs-lookup"><span data-stu-id="33c4e-205">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="33c4e-206">ARM 템플릿을 사용하여 앱을 만들고 배포하는 경우 `siteextensions` 리소스 형식을 사용하여 웹앱에 사이트 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-206">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="33c4e-207">예:</span><span class="sxs-lookup"><span data-stu-id="33c4e-207">For example:</span></span>

[!code-json[Main](index/sample/arm.json?highlight=2)]

<!--
### Deploy the app self-contained

A [self-contained app](/dotnet/core/deploying/#self-contained-deployments-scd) can be deployed that carries the preview runtime in the deployment. When deploying a self-contained app:

* The site doesn't need to be prepared.
* The app must be published differently than when publishing for a framework-dependent deployment with the shared runtime and host on the server.

Self-contained apps are an option for all ASP.NET Core apps.
-->

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="33c4e-208">Web Apps for Containers에서 Docker 사용</span><span class="sxs-lookup"><span data-stu-id="33c4e-208">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="33c4e-209">[Docker 허브](https://hub.docker.com/r/microsoft/aspnetcore/)에는 최신 미리 보기 Docker 이미지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-209">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest preview Docker images.</span></span> <span data-ttu-id="33c4e-210">이미지는 기본 이미지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-210">The images can be used as a base image.</span></span> <span data-ttu-id="33c4e-211">이미지를 사용하고 일반적으로 Web App for Containers에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-211">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="33c4e-212">추가 자료</span><span class="sxs-lookup"><span data-stu-id="33c4e-212">Additional resources</span></span>

* [<span data-ttu-id="33c4e-213">Web Apps 개요(5분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="33c4e-213">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="33c4e-214">Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="33c4e-214">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="33c4e-215">Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 비디오)</span><span class="sxs-lookup"><span data-stu-id="33c4e-215">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="33c4e-216">Azure App Service 진단 개요</span><span class="sxs-lookup"><span data-stu-id="33c4e-216">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)
* <xref:host-and-deploy/web-farm>

<span data-ttu-id="33c4e-217">Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-217">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="33c4e-218">다음 항목은 기본 IIS 기술과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33c4e-218">The following topics pertain to the underlying IIS technology:</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/modules>
* [<span data-ttu-id="33c4e-219">Microsoft TechNet 라이브러리: Windows Server</span><span class="sxs-lookup"><span data-stu-id="33c4e-219">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
