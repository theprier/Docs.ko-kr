---
title: "Azure App Service에서 ASP.NET Core 호스트"
author: guardrex
description: "유용한 리소스에 대한 링크를 통해 Azure App Service에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/index
ms.openlocfilehash: cefbc27c8091a2ed1441663e3779d67aae2c64dd
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="host-aspnet-core-on-azure-app-service"></a><span data-ttu-id="e54aa-103">Azure App Service에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="e54aa-103">Host ASP.NET Core on Azure App Service</span></span>

<span data-ttu-id="e54aa-104">[Azure App Service](https://azure.microsoft.com/services/app-service/)는 ASP.NET Core를 비롯한 웹앱을 호스트하기 위한 [Microsoft 클라우드 컴퓨팅 플랫폼 서비스](https://azure.microsoft.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-104">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span>

[!INCLUDE[Azure App Service Preview Notice](../../includes/azure-apps-preview-notice.md)]

## <a name="useful-resources"></a><span data-ttu-id="e54aa-105">유용한 리소스</span><span class="sxs-lookup"><span data-stu-id="e54aa-105">Useful resources</span></span>

<span data-ttu-id="e54aa-106">Azure [Web Apps 설명서](/azure/app-service/)는 Azure 앱 설명서, 샘플, 방법 가이드 및 기타 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-106">The Azure [Web Apps Documentation](/azure/app-service/) is the home for Azure Apps documentation, tutorials, samples, how-to guides, and other resources.</span></span> <span data-ttu-id="e54aa-107">ASP.NET Core 앱 호스트와 관련하여 두 가지 주목할 만한 자습서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-107">Two notable tutorials that pertain to hosting ASP.NET Core apps are:</span></span>

[<span data-ttu-id="e54aa-108">빠른 시작: Azure에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e54aa-108">Quickstart: Create an ASP.NET Core web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)  
<span data-ttu-id="e54aa-109">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 Windows의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-109">Use Visual Studio to create and deploy an ASP.NET Core web app to Azure App Service on Windows.</span></span>

[<span data-ttu-id="e54aa-110">빠른 시작: Linux의 App Service에서 .NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e54aa-110">Quickstart: Create a .NET Core web app in App Service on Linux</span></span>](/azure/app-service/containers/quickstart-dotnetcore)  
<span data-ttu-id="e54aa-111">명령줄을 사용하여 ASP.NET Core 웹앱을 만들고 Linux의 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-111">Use the command line to create and deploy an ASP.NET Core web app to Azure App Service on Linux.</span></span>

<span data-ttu-id="e54aa-112">다음 문서는 ASP.NET Core 설명서에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-112">The following articles are available in ASP.NET Core documentation:</span></span>

[<span data-ttu-id="e54aa-113">Visual Studio를 사용하여 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="e54aa-113">Publish to Azure with Visual Studio</span></span>](xref:tutorials/publish-to-azure-webapp-using-vs)  
<span data-ttu-id="e54aa-114">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-114">Learn how to publish an ASP.NET Core app to Azure App Service using Visual Studio.</span></span>

[<span data-ttu-id="e54aa-115">CLI 도구를 사용하여 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="e54aa-115">Publish to Azure with CLI tools</span></span>](xref:tutorials/publish-to-azure-webapp-using-cli)  
<span data-ttu-id="e54aa-116">Git 명령줄 클라이언트를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-116">Learn how to publish an ASP.NET Core app to Azure App Service using the Git command-line client.</span></span>

[<span data-ttu-id="e54aa-117">Visual Studio 및 Git을 사용하여 Azure에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="e54aa-117">Continuous deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)  
<span data-ttu-id="e54aa-118">Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-118">Learn how to create an ASP.NET Core web app using Visual Studio and deploy it to Azure App Service using Git for continuous deployment.</span></span>

<span data-ttu-id="e54aa-119">[Continuous deployment to Azure with VSTS](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)(VSTS를 사용하여 Azure에 연속 배포)</span><span class="sxs-lookup"><span data-stu-id="e54aa-119">[Continuous deployment to Azure with VSTS](https://www.visualstudio.com/docs/build/aspnet/core/quick-to-azure)</span></span>  
<span data-ttu-id="e54aa-120">ASP.NET Core 앱에 대한 CI 빌드를 설정하고 Azure App Service에 대한 연속 배포 릴리스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-120">Set up a CI build for an ASP.NET Core app, then create a continuous deployment release to Azure App Service.</span></span>

[<span data-ttu-id="e54aa-121">Azure Web App 샌드박스</span><span class="sxs-lookup"><span data-stu-id="e54aa-121">Azure Web App sandbox</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)  
<span data-ttu-id="e54aa-122">Azure 앱 플랫폼에서 적용하는 Azure App Service 런타임 실행 제한 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-122">Discover Azure App Service runtime execution limitations enforced by the Azure Apps platform.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="e54aa-123">응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="e54aa-123">Application configuration</span></span>

<span data-ttu-id="e54aa-124">ASP.NET Core 2.0 이상에서 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)의 세 패키지는 Azure App Service에 배포된 앱을 위한 자동 로깅 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-124">With ASP.NET Core 2.0 and later, three packages in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) provide automatic logging features for apps deployed to Azure App Service:</span></span>

* <span data-ttu-id="e54aa-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/)은 [IHostingStartup](xref:host-and-deploy/platform-specific-configuration)을 사용하여 Azure App Service와 ASP.NET Core의 라이트업 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-125">[Microsoft.AspNetCore.AzureAppServices.HostingStartup](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServices.HostingStartup/) uses [IHostingStartup](xref:host-and-deploy/platform-specific-configuration) to provide ASP.NET Core lightup integration with Azure App Service.</span></span> <span data-ttu-id="e54aa-126">추가된 로깅 기능은 `Microsoft.AspNetCore.AzureAppServicesIntegration` 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-126">The added logging features are provided by the `Microsoft.AspNetCore.AzureAppServicesIntegration` package.</span></span>
* <span data-ttu-id="e54aa-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/)은 [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics)를 실행하여 `Microsoft.Extensions.Logging.AzureAppServices` 패키지의 Azure App Service 진단 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-127">[Microsoft.AspNetCore.AzureAppServicesIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.AzureAppServicesIntegration/) executes [AddAzureWebAppDiagnostics](/dotnet/api/microsoft.extensions.logging.azureappservicesloggerfactoryextensions.addazurewebappdiagnostics) to add Azure App Service diagnostics logging providers in the `Microsoft.Extensions.Logging.AzureAppServices` package.</span></span>
* <span data-ttu-id="e54aa-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/)는 Azure App Service 진단 로그 및 로그 스트리밍 기능을 지원하는 로거 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-128">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices/) provides logger implementations to support Azure App Service diagnostics logs and log streaming features.</span></span>

## <a name="monitoring-and-logging"></a><span data-ttu-id="e54aa-129">모니터링 및 로깅</span><span class="sxs-lookup"><span data-stu-id="e54aa-129">Monitoring and logging</span></span>

<span data-ttu-id="e54aa-130">모니터링, 로깅 및 문제 해결에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54aa-130">For monitoring, logging, and troubleshooting information, see the following articles:</span></span>

[<span data-ttu-id="e54aa-131">방법: Azure App Service에서 앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="e54aa-131">How to: Monitor Apps in Azure App Service</span></span>](/azure/app-service/web-sites-monitor)  
<span data-ttu-id="e54aa-132">앱 및 App Service 계획의 할당량 및 메트릭을 검토하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-132">Learn how to review quotas and metrics for apps and App Service plans.</span></span>

[<span data-ttu-id="e54aa-133">Azure App Service에서 웹앱에 대한 진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="e54aa-133">Enable diagnostics logging for web apps in Azure App Service</span></span>](/azure/app-service/web-sites-enable-diagnostic-log)  
<span data-ttu-id="e54aa-134">HTTP 상태 코드, 실패한 요청 및 웹 서버 활동에 대한 진단 로깅을 활성화하고 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-134">Discover how to enable and access diagnostic logging for HTTP status codes, failed requests, and web server activity.</span></span>

[<span data-ttu-id="e54aa-135">ASP.NET Core의 오류 처리 소개</span><span class="sxs-lookup"><span data-stu-id="e54aa-135">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="e54aa-136">ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-136">Understand common appoaches to handling errors in ASP.NET Core apps.</span></span>

[<span data-ttu-id="e54aa-137">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e54aa-137">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="e54aa-138">ASP.NET Core 앱을 사용하는 Azure App Service 배포에 대한 문제 진단 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-138">Learn how to diagnose issues with Azure App Service deployments with ASP.NET Core apps.</span></span>

[<span data-ttu-id="e54aa-139">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="e54aa-139">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)  
<span data-ttu-id="e54aa-140">Azure App Service/IIS에서 호스트하는 앱의 일반적인 배포 구성 오류와 문제 해결에 대한 조언을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54aa-140">See the common deployment configuration errors for apps hosted by Azure App Service/IIS with troubleshooting advice.</span></span>

## <a name="data-protection-key-ring-and-deployment-slots"></a><span data-ttu-id="e54aa-141">데이터 보호 키 링 및 배포 슬롯</span><span class="sxs-lookup"><span data-stu-id="e54aa-141">Data Protection key ring and deployment slots</span></span>

<span data-ttu-id="e54aa-142">[데이터 보호 키](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)는 *%HOME%\ASP.NET\DataProtection-Keys* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-142">[Data Protection keys](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="e54aa-143">이 폴더는 네트워크 저장소에서 지원하고, 앱을 호스트하는 모든 컴퓨터에서 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-143">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span> <span data-ttu-id="e54aa-144">저장된 키는 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-144">Keys aren't protected at rest.</span></span> <span data-ttu-id="e54aa-145">이 폴더는 단일 배포 슬롯에 앱의 모든 인스턴스에 대한 키 링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-145">This folder supplies the key ring to all instances of an app in a single deployment slot.</span></span> <span data-ttu-id="e54aa-146">준비 및 프로덕션과 같은 별도의 배포 슬롯은 키 링을 공유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-146">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span>

<span data-ttu-id="e54aa-147">배포 슬롯을 바꿀 경우 데이터 보호를 사용하는 모든 시스템은 이전 슬롯 내에 있는 키 링을 사용하여 저장된 데이터의 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-147">When swapping between deployment slots, any system using data protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="e54aa-148">ASP.NET 쿠키 미들웨어는 데이터 보호를 사용하여 쿠키를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-148">ASP.NET Cookie Middleware uses data protection to protect its cookies.</span></span> <span data-ttu-id="e54aa-149">이로 인해 표준 ASP.NET 쿠키 미들웨어를 사용하는 앱에서 사용자가 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-149">This leads to users being signed out of an app that uses the standard ASP.NET Cookie Middleware.</span></span> <span data-ttu-id="e54aa-150">슬롯에 관계없는 키 링 솔루션의 경우 다음과 같은 외부 키 링 공급자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e54aa-150">For a slot-independent key ring solution, use an external key ring provider, such as:</span></span>

* <span data-ttu-id="e54aa-151">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="e54aa-151">Azure Blob Storage</span></span>
* <span data-ttu-id="e54aa-152">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e54aa-152">Azure Key Vault</span></span>
* <span data-ttu-id="e54aa-153">SQL 저장소</span><span class="sxs-lookup"><span data-stu-id="e54aa-153">SQL store</span></span>
* <span data-ttu-id="e54aa-154">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e54aa-154">Redis cache</span></span>

<span data-ttu-id="e54aa-155">자세한 내용은 [키 저장소 공급자](xref:security/data-protection/implementation/key-storage-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e54aa-155">For more information, see [Key storage providers](xref:security/data-protection/implementation/key-storage-providers).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e54aa-156">추가 자료</span><span class="sxs-lookup"><span data-stu-id="e54aa-156">Additional resources</span></span>

* [<span data-ttu-id="e54aa-157">Web Apps 개요(5분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="e54aa-157">Web Apps overview (5-minute overview video)</span></span>](/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="e54aa-158">Azure App Service: .NET 앱을 호스트하기에 가장 좋은 서비스(55분 개요 비디오)</span><span class="sxs-lookup"><span data-stu-id="e54aa-158">Azure App Service: The Best Place to Host your .NET Apps (55-minute overview video)</span></span>](https://channel9.msdn.com/events/dotnetConf/2017/T222)
* [<span data-ttu-id="e54aa-159">Azure Friday: Azure App Service 진단 및 문제 해결 환경(12분 비디오)</span><span class="sxs-lookup"><span data-stu-id="e54aa-159">Azure Friday: Azure App Service Diagnostic and Troubleshooting Experience (12-minute video)</span></span>](https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Diagnostic-and-Troubleshooting-Experience)
* [<span data-ttu-id="e54aa-160">Azure App Service 진단 개요</span><span class="sxs-lookup"><span data-stu-id="e54aa-160">Azure App Service diagnostics overview</span></span>](/azure/app-service/app-service-diagnostics)

<span data-ttu-id="e54aa-161">Windows Server의 Azure App Service는 [IIS(인터넷 정보 서비스)](https://www.iis.net/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-161">Azure App Service on Windows Server uses [Internet Information Services (IIS)](https://www.iis.net/).</span></span> <span data-ttu-id="e54aa-162">다음 항목은 기본 IIS 기술과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54aa-162">The following topics pertain to the underlying IIS technology:</span></span>

* [<span data-ttu-id="e54aa-163">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="e54aa-163">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="e54aa-164">ASP.NET Core 모듈 소개</span><span class="sxs-lookup"><span data-stu-id="e54aa-164">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="e54aa-165">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="e54aa-165">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="e54aa-166">ASP.NET Core와 함께 IIS 모듈 사용</span><span class="sxs-lookup"><span data-stu-id="e54aa-166">Using IIS Modules with ASP.NET Core</span></span>](xref:host-and-deploy/iis/modules)
* [<span data-ttu-id="e54aa-167">Microsoft TechNet 라이브러리: Windows Server</span><span class="sxs-lookup"><span data-stu-id="e54aa-167">Microsoft TechNet Library: Windows Server</span></span>](/windows-server/windows-server-versions)
