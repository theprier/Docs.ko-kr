---
title: Azure App Service에서 ASP.NET Core 호스트
author: guardrex
description: 유용한 리소스에 대한 링크를 통해 Azure App Service에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: 9e438cef9db61e725b5385da53e8aa2b407218c3
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="host-aspnet-core-on-azure-app-service"></a><span data-ttu-id="12c69-103">Azure App Service에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="12c69-103">Host ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="12c69-104">[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

## <a name="useful-resources"></a><span data-ttu-id="12c69-105">유용한 리소스</span><span class="sxs-lookup"><span data-stu-id="12c69-105">Useful resources</span></span>

<span data-ttu-id="12c69-106">Azure [Web Apps 설명서](/azure/app-service/)는 Azure 앱 설명서, 샘플, 방법 가이드 및 기타 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="12c69-107">ASP.NET Core 앱 호스트와 관련하여 두 가지 주목할 만한 자습서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="12c69-108">빠른 시작: Azure에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="12c69-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="12c69-109">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 Windows의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="12c69-110">빠른 시작: Linux의 App Service에서 .NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="12c69-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="12c69-111">명령줄을 사용하여 ASP.NET Core 웹앱을 만들고 Linux의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="12c69-112">다음 문서는 ASP.NET Core 설명서에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="12c69-113">Visual Studio를 사용하여 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="12c69-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="12c69-114">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="12c69-115">CLI 도구를 사용하여 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="12c69-115">Publish to Azure with CLI tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli)  
<span data-ttu-id="12c69-116">Git 명령줄 클라이언트를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-116">Learn how to publish an ASP.NET Core app to Azure App Service using the Git command-line client.</span></span>

[<span data-ttu-id="12c69-117">Visual Studio 및 Git을 사용하여 Azure에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="12c69-117">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="12c69-118">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-118">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

[<span data-ttu-id="12c69-119">VSTS를 사용하여 Azure에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="12c69-119">Continuous deployment to Azure with VSTS</span></span>](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)  
<span data-ttu-id="12c69-120">ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-120">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="12c69-121">Azure Web App 샌드박스</span><span class="sxs-lookup"><span data-stu-id="12c69-121">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="12c69-122">Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-122">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="12c69-123">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="12c69-123">Application configuration</span></span>

<span data-ttu-id="12c69-124">ASP.NET Core 2.0 이상에서 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)의 세 패키지는 Azure App Service에 배포된 앱을 위한 자동 로깅 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-124">With ASP.NET Core 2.0 and later, three packages in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="12c69-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 라이트업 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:fundamentals/configuration/platform-specific-configuration) to provide ASP.NET Core lightup integration with Azure App Service.</span></span> <span data-ttu-id="12c69-126">추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-126">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="12c69-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="12c69-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

## <a name="proxy-server-and-load-balancer-scenarios"></a><span data-ttu-id="12c69-129">프록시 서버 및 부하 분산 장치 시나리오</span><span class="sxs-lookup"><span data-stu-id="12c69-129">Proxy server and load balancer scenarios</span></span>

<span data-ttu-id="12c69-130">체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-130">The IIS Integration Middleware, which configures Forwarded Headers Middleware, and the ASP.NET Core Module are configured to forward the scheme (HTTP/HTTPS) and the remote IP address where the request originated.</span></span> <span data-ttu-id="12c69-131">추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-131">Additional configuration might be required for apps hosted behind additional proxy servers and load balancers.</span></span> <span data-ttu-id="12c69-132">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c69-132">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="12c69-133">모니터링 및 로깅</span><span class="sxs-lookup"><span data-stu-id="12c69-133">Monitoring and logging</span></span>

<span data-ttu-id="12c69-134">모니터링, 로깅 및 문제 해결에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c69-134">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="12c69-135">방법: Azure App Service에서 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="12c69-135">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="12c69-136">앱 및 App Service 계획의 할당량 및 메트릭을 검토하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-136">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="12c69-137">Azure App Service에서 웹앱에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="12c69-137">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="12c69-138">HTTP 상태 코드, 실패한 요청 및 웹 서버 활동에 대한 진단 로깅을 활성화하고 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-138">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="12c69-139">ASP.NET Core의 오류 처리 소개</span><span class="sxs-lookup"><span data-stu-id="12c69-139">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="12c69-140">ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-140">Understand common appoaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="12c69-141">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="12c69-141">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="12c69-142">ASP.NET Core 앱을 사용하는 Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-142">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="12c69-143">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="12c69-143">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="12c69-144">Azure App Service/IIS에서 호스트하는 앱의 일반적인 배포 구성 오류와 문제 해결에 대한 조언을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c69-144">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="12c69-145">데이터 보호 키 링 및 배포 슬롯</span><span class="sxs-lookup"><span data-stu-id="12c69-145">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="12c69-146">[데이터 보호 키](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-146">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="12c69-147">이 폴더는 네트워크 저장소에서 지원하고, 앱을 호스트하는 모든 컴퓨터에서 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-147">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="12c69-148">저장된 키는 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-148">Keys aren't protected at rest.</span></span> <span data-ttu-id="12c69-149">이 폴더는 단일 배포 슬롯에 앱의 모든 인스턴스에 대한 키 링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-149">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="12c69-150">준비 및 프로덕션과 같은 별도의 배포 슬롯은 키 링을 공유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-150">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="12c69-151">배포 슬롯을 바꿀 경우 데이터 보호를 사용하는 모든 시스템은 이전 슬롯 내에 있는 키 링을 사용하여 저장된 데이터의 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-151">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="12c69-152">ASP.NET 쿠키 미들웨어는 데이터 보호를 사용하여 쿠키를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-152">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="12c69-153">이로 인해 표준 ASP.NET 쿠키 미들웨어를 사용하는 앱에서 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-153">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="12c69-154">슬롯에 관계없는 키 링 솔루션의 경우 다음과 같은 외부 키 링 공급자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="12c69-154">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="12c69-155">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="12c69-155">Azure Blob Storage</span></span>
* <span data-ttu-id="12c69-156">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="12c69-156">Azure Key Vault</span></span>
* <span data-ttu-id="12c69-157">SQL 저장소</span><span class="sxs-lookup"><span data-stu-id="12c69-157">SQL store</span></span>
* <span data-ttu-id="12c69-158">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="12c69-158">Redis cache</span></span>

<span data-ttu-id="12c69-159">자세한 내용은 [키 저장소 공급자](xref:security/data-protection/implementation/key-storage-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c69-159">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="deploy-aspnet-core-preview-release-to-azure-app-service"></a><span data-ttu-id="12c69-160">Azure App Service에 ASP.NET Core 미리 보기 릴리스 배포</span><span class="sxs-lookup"><span data-stu-id="12c69-160">Deploy ASP.NET Core preview release to Azure App Service</span></span>

<span data-ttu-id="12c69-161">다음과 같은 방법으로 Azure App Service에 ASP.NET Core 미리 보기 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-161">ASP.NET Core preview apps can be deployed to Azure App Service with the following approaches:</span></span>

* [<span data-ttu-id="12c69-162">미리 보기 사이트 확장 설치</span><span class="sxs-lookup"><span data-stu-id="12c69-162">Install the preview site extension</span></span>](#install-the-preview-site-extension)
* [<span data-ttu-id="12c69-163">자체 포함된 앱 배포</span><span class="sxs-lookup"><span data-stu-id="12c69-163">Deploy the app self-contained</span></span>](#deploy-the-app-self-contained)
* [<span data-ttu-id="12c69-164">Web Apps for Containers에서 Docker 사용</span><span class="sxs-lookup"><span data-stu-id="12c69-164">Use Docker with Web Apps for containers</span></span>](#use-docker-with-web-apps-for-containers)

<span data-ttu-id="12c69-165">미리 보기 사이트 확장을 사용하는 데 문제가 발생하는 경우 [GitHub](https://github.com/aspnet/azureintegration/issues/new)에서 문제를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-165">If a problem occurs using the preview site extension, open an issue on [GitHub](https://github.com/aspnet/azureintegration/issues/new).</span></span>

### <a name="install-the-preview-site-extension"></a><span data-ttu-id="12c69-166">미리 보기 사이트 확장 설치</span><span class="sxs-lookup"><span data-stu-id="12c69-166">Install the preview site extension</span></span>

* <span data-ttu-id="12c69-167">Azure Portal에서 App Service 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-167">From the Azure portal, navigate to the App Service blade.</span></span>
* <span data-ttu-id="12c69-168">검색 상자에 "ex"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-168">Enter "ex" in the search box.</span></span>
* <span data-ttu-id="12c69-169">**확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-169">Select **Extensions**.</span></span>
* <span data-ttu-id="12c69-170">"추가"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-170">Select "Add".</span></span>

![이전 단계에서 Azure 앱 블레이드](index/_static/x1.png)

* <span data-ttu-id="12c69-172">**ASP.NET Core 2.1(x86) 런타임** 또는 **ASP.NET Core 2.1(x64) 런타임**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-172">Select **ASP.NET Core 2.1 (x86) Runtime** or **ASP.NET Core 2.1 (x64) Runtime**.</span></span>
* <span data-ttu-id="12c69-173">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-173">Select **OK**.</span></span> <span data-ttu-id="12c69-174">**확인**을 다시 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-174">Select **OK** again.</span></span>

<span data-ttu-id="12c69-175">추가 작업이 완료되면 최신.NET Core 2.1 미리 보기가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-175">When the add operations complete, the latest .NET Core 2.1 preview is installed.</span></span> <span data-ttu-id="12c69-176">콘솔에서 `dotnet --info`를 실행하여 설치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-176">Verify the installation by running `dotnet --info` in the console.</span></span> <span data-ttu-id="12c69-177">**App Service** 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="12c69-177">From the **App Service** blade:</span></span>

* <span data-ttu-id="12c69-178">검색 상자에 "con"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-178">Enter "con" in the search box.</span></span>
* <span data-ttu-id="12c69-179">**콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-179">Select **Console**.</span></span>
* <span data-ttu-id="12c69-180">콘솔에 `dotnet --info`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-180">Enter `dotnet --info` in the console.</span></span>

![이전 단계에서 Azure 앱 블레이드](index/_static/cons.png)

<span data-ttu-id="12c69-182">앞의 이미지는 이 내용이 작성된 현재 시간이었습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-182">The preceding image was current at the time this was written.</span></span> <span data-ttu-id="12c69-183">다른 버전으로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-183">You may see a different version.</span></span>

<span data-ttu-id="12c69-184">`dotnet --info`는 미리 보기가 설치되어 있는 사이트 확장에 대한 경로를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-184">The `dotnet --info` displays the the path to the site extension where the Preview has been installed.</span></span> <span data-ttu-id="12c69-185">기본 *ProgramFiles* 위치 대신 사이트 확장에서 앱이 실행된다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-185">It shows the app is running from the site extension instead of from the default *ProgramFiles* location.</span></span> <span data-ttu-id="12c69-186">*ProgramFiles*가 표시되면 사이트를 다시 시작하고 `dotnet --info`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-186">If you see *ProgramFiles*, restart the site and run `dotnet --info`.</span></span>

<span data-ttu-id="12c69-187">**ARM 템플릿에서 미리 보기 사이트 확장 사용**</span><span class="sxs-lookup"><span data-stu-id="12c69-187">**Use the preview site extension with an ARM template**</span></span>

<span data-ttu-id="12c69-188">ARM 템플릿을 사용하여 앱을 만들고 배포하는 경우 `siteextensions` 리소스 형식을 사용하여 웹앱에 사이트 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-188">If an ARM template is used to create and deploy apps, the `siteextensions` resource type can be used to add the site extension to a web app.</span></span> <span data-ttu-id="12c69-189">예:</span><span class="sxs-lookup"><span data-stu-id="12c69-189">For example:</span></span>

[!code-json[Main](index/sample/arm.json?highlight=2)]

### <a name="deploy-the-app-self-contained"></a><span data-ttu-id="12c69-190">자체 포함된 앱 배포</span><span class="sxs-lookup"><span data-stu-id="12c69-190">Deploy the app self-contained</span></span>

<span data-ttu-id="12c69-191">배포에 미리 보기 런타임을 전달하는 [자체 포함된 앱](/dotnet/core/deploying/#self-contained-deployments-scd)을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-191">A [self-contained app](/dotnet/core/deploying/#self-contained-deployments-scd) can be deployed that carries the preview runtime in the deployment.</span></span> <span data-ttu-id="12c69-192">자체 포함된 앱을 배포하는 경우:</span><span class="sxs-lookup"><span data-stu-id="12c69-192">When deploying a self-contained app:</span></span>

* <span data-ttu-id="12c69-193">사이트는 준비할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-193">The site doesn't need to be prepared.</span></span>
* <span data-ttu-id="12c69-194">공유 런타임 및 서버의 호스트를 사용하여 프레임워크 종속 배포를 위해 게시할 때와 다르게 앱을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-194">The app must be published differently than when publishing for a framework-dependent deployment with the shared runtime and host on the server.</span></span>

<span data-ttu-id="12c69-195">자체 포함된 앱은 모든 ASP.NET Core 앱에 대한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-195">Self-contained apps are an option for all ASP.NET Core apps.</span></span>

### <a name="use-docker-with-web-apps-for-containers"></a><span data-ttu-id="12c69-196">Web Apps for Containers에서 Docker 사용</span><span class="sxs-lookup"><span data-stu-id="12c69-196">Use Docker with Web Apps for containers</span></span>

<span data-ttu-id="12c69-197">[Docker 허브](https://hub.docker.com/r/microsoft/aspnetcore/)에는 최신 2.1 미리 보기 Docker 이미지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-197">The [Docker Hub](https://hub.docker.com/r/microsoft/aspnetcore/) contains the latest 2.1 preview Docker images.</span></span> <span data-ttu-id="12c69-198">이미지는 기본 이미지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-198">The images can be used as a base image.</span></span> <span data-ttu-id="12c69-199">이미지를 사용하고 일반적으로 Web App for Containers에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-199">Use the image and deploy to Web Apps for Containers normally.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12c69-200">추가 자료</span><span class="sxs-lookup"><span data-stu-id="12c69-200">Additional resources</span></span>

* [<span data-ttu-id="12c69-201">Web Apps 개요(5분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="12c69-201">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="12c69-202">Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="12c69-202">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="12c69-203">Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 비디오)</span><span class="sxs-lookup"><span data-stu-id="12c69-203">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="12c69-204">Azure App Service 진단 개요</span><span class="sxs-lookup"><span data-stu-id="12c69-204">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)

<span data-ttu-id="12c69-205">Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-205">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="12c69-206">다음 항목은 기본 IIS 기술과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c69-206">The following topics pertain to the underlying IIS technology:</span></span>

* [<span data-ttu-id="12c69-207">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="12c69-207">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="12c69-208">ASP.NET Core 모듈 소개</span><span class="sxs-lookup"><span data-stu-id="12c69-208">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="12c69-209">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="12c69-209">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="12c69-210">IIS 모듈 및 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="12c69-210">IIS Modules with ASP.NET Core</span></span>](xref:host-and-deploy/iis/modules)
* [<span data-ttu-id="12c69-211">Microsoft TechNet 라이브러리: Windows Server</span><span class="sxs-lookup"><span data-stu-id="12c69-211">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
