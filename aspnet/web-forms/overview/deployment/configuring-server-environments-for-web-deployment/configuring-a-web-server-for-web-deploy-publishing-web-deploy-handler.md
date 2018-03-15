---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: "배포 게시를 웹에 대 한 웹 서버 구성 (웹 처리기를 배포 하는 데 사용) | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 웹 게시 및 IIS 웹 배포 한자를 사용 하 여 배포를 지원 하기 위해 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법을 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: 81848c683fb9ddaa8942f030a520847a3c89fde0
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
<a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a><span data-ttu-id="c9595-103">배포 게시를 웹에 대 한 웹 서버 구성 (웹 처리기를 배포 하는 데 사용)</span><span class="sxs-lookup"><span data-stu-id="c9595-103">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>
====================
<span data-ttu-id="c9595-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c9595-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c9595-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="c9595-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c9595-106">이 항목에서는 웹 게시 및 IIS 웹 배포 처리기를 사용 하 여 배포를 지원 하기 위해 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-106">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deploy Handler.</span></span>
> 
> <span data-ttu-id="c9595-107">웹 배포 2.0 이상으로 작업할 때 다음 3 가지 주요 방법 응용 프로그램이 나 웹 서버에 사이트를 가져오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-107">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="c9595-108">다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-108">You can:</span></span>
> 
> - <span data-ttu-id="c9595-109">사용 하 여는 *원격 에이전트 서비스를 배포 하는 웹*합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-109">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="c9595-110">이 방법은 웹 서버의 적게 구성 해야 하지만 아무 것도 서버에 배포 하기 위해 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-110">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="c9595-111">사용 하 여는 *웹 배포 처리기*합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-111">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="c9595-112">이 방법은 훨씬 더 복잡 한 고 웹 서버를 설정 하려면 초기 더 많은 노력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-112">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="c9595-113">그러나이 방법을 사용 하면 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-113">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="c9595-114">웹 배포 처리기가 IIS 7 이상 버전에서에서 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-114">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="c9595-115">사용 하 여 *오프 라인 배포*합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-115">Use *offline deployment*.</span></span> <span data-ttu-id="c9595-116">이 방법은 웹 서버의 최소 구성 하는데 수동으로 서버에 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져올 해야 서버 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-116">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="c9595-117">주요 기능, 이점 및 이러한 방법의 단점에 대 한 자세한 내용은 참조 하십시오. [웹 배포에 대 한 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-117">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>


<span data-ttu-id="c9595-118">예, 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 콘텐츠를 배포 하도록 허용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="c9595-118">Yes, if you want to allow non-administrator users to deploy content to specific IIS websites.</span></span> <span data-ttu-id="c9595-119">이 방법은 이러한 유형의 시나리오에서는 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-119">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="c9595-120">스테이징 또는 프로덕션 환경, 원격 배포를 트리거하는 사람 또는 서비스 계정이 서버 관리자의 자격 증명에 대 한 액세스를 갖고 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-120">Staging or production environments, where the person or service account that triggers the remote deployment is unlikely to have access to the credentials of a server administrator.</span></span>
- <span data-ttu-id="c9595-121">원격 사용자가 웹 서버 (또는 다른 사용자의 웹 사이트에 대 한 액세스)의 모든 권한을 제공 하지 않고도 자신의 웹 사이트를 업데이트 하는 기능을 제공 하려면 호스팅된 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-121">Hosted environments, where you want to give remote users the ability to update their websites without giving them full control of your web servers (or access to anyone else's websites).</span></span>

<span data-ttu-id="c9595-122">개발 또는 테스트 시나리오에서 또는 소규모 조직에서 서버 관리자 자격 증명을 사용 하 여 배포 콘텐츠 작으면 종종 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-122">In development or test scenarios, or in smaller organizations, deploying content using server administrator credentials is often less contentious.</span></span> <span data-ttu-id="c9595-123">이러한 시나리오에서 사용 하 여 배포를 지원 하도록 웹 서버 구성에서 [웹 배포 된 원격 에이전트 서비스가](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 더 간단한 접근 방식을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-123">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Remote Agent Service](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) offers a more straightforward approach.</span></span>

## <a name="task-overview"></a><span data-ttu-id="c9595-124">작업 개요</span><span class="sxs-lookup"><span data-stu-id="c9595-124">Task Overview</span></span>

<span data-ttu-id="c9595-125">허용 및 웹 배포 처리기 방식을 사용 하 여 원격 컴퓨터에서 웹 패키지를 배포 하도록 웹 서버를 구성 하려면 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-125">To configure the web server to accept and deploy web packages from a remote computer using the Web Deploy Handler approach, you'll need to:</span></span>

- <span data-ttu-id="c9595-126">만들기, 또는 도메인 사용자 계정을 ("관리자 이외의 사용자")를 사용 하 여 배포를 수행 하는 자격 증명에 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-126">Create, or choose, a domain user account (the "non-administrator user") whose credentials you'll use to perform deployments.</span></span>
- <span data-ttu-id="c9595-127">웹 관리 서비스 및 기본 인증 모듈을 포함 하 여 IIS 7.5를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-127">Install IIS 7.5, including the Web Management Service and the Basic Authentication module.</span></span>
- <span data-ttu-id="c9595-128">2.1 이상에 웹 배포를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-128">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="c9595-129">원격 연결을 허용 하도록 웹 관리 서비스를 구성 하 고 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-129">Configure the Web Management Service to allow remote connections, and start the service.</span></span>
- <span data-ttu-id="c9595-130">배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-130">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="c9595-131">IIS 관리자에서 웹 사이트에 관리자가 아닌 사용자 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-131">Grant your non-administrator user permissions on your website in IIS Manager.</span></span>
- <span data-ttu-id="c9595-132">Web Management Service 위임 규칙을 추가 하 고 관리자가 아닌 사용자 계정을 사용 하 여 웹 사이트 콘텐츠를 변경 하는 서비스 허용 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-132">Ensure that the Web Management Service delegation rules permit the service to add and change website content using your non-administrator user account.</span></span>
- <span data-ttu-id="c9595-133">8172 포트에서 들어오는 연결을 허용 하도록 방화벽을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-133">Configure any firewalls to allow incoming connections on port 8172.</span></span>

<span data-ttu-id="c9595-134">ContactManager 샘플 솔루션을 구체적으로 호스트 하려면 또한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-134">To host the ContactManager sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="c9595-135">.NET Framework 4.0을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-135">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="c9595-136">ASP.NET MVC 3을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-136">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="c9595-137">이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-137">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="c9595-138">작업은이 항목의 연습에서는 Windows Server 2008 r 2를 실행 하는 새로운 서버 빌드도 시작 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-138">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="c9595-139">계속 하기 전에 다음 사항을 확인.</span><span class="sxs-lookup"><span data-stu-id="c9595-139">Before you continue, ensure that:</span></span>

- <span data-ttu-id="c9595-140">Windows Server 2008 R2 서비스 팩 1 및 가능한 모든 업데이트가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-140">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="c9595-141">서버가 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-141">The server is domain-joined.</span></span>
- <span data-ttu-id="c9595-142">서버에 고정 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-142">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="c9595-143">참조 컴퓨터는 도메인에 가입에 대 한 자세한 내용은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-143">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="c9595-144">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [고정 IP 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-144">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>


## <a name="install-products-and-components"></a><span data-ttu-id="c9595-145">제품 및 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="c9595-145">Install Products and Components</span></span>

<span data-ttu-id="c9595-146">이 섹션에서는 웹 서버에서 필요한 제품 및 구성 요소를 설치 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-146">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="c9595-147">시작 하기 전에 서버에 최신 인지 확인 하려면 Windows Update를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-147">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="c9595-148">이 경우 이러한 것 들을 설치 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-148">In this case, you need to install these things:</span></span>

- <span data-ttu-id="c9595-149">**IIS 7 권장 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-149">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="c9595-150">이 통해는 **웹 서버 (IIS)** 웹 서버에서 역할 및 IIS 모듈 및 ASP.NET 응용 프로그램을 호스트 하는 데 필요한 구성 요소 집합을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-150">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="c9595-151">**IIS: 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-151">**IIS: Management Service**.</span></span> <span data-ttu-id="c9595-152">IIS에서 웹 관리 서비스 (WMSvc)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-152">This installs the Web Management Service (WMSvc) in IIS.</span></span> <span data-ttu-id="c9595-153">이 서비스는 IIS 웹 사이트를 원격으로 관리할 수 있습니다 및 클라이언트에 웹 배포 처리기 끝점을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-153">This service enables remote management of IIS websites and exposes the Web Deploy Handler endpoint to clients.</span></span>
- <span data-ttu-id="c9595-154">**IIS: 기본 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-154">**IIS: Basic Authentication**.</span></span> <span data-ttu-id="c9595-155">IIS 기본 인증 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-155">This installs the IIS Basic Authentication module.</span></span> <span data-ttu-id="c9595-156">이 그러면 웹 관리 서비스 (WMSvc) 인증 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-156">This lets the Web Management Service (WMSvc) authenticate the credentials you provide.</span></span>
- <span data-ttu-id="c9595-157">**웹 배포 도구 2.1 이상**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-157">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="c9595-158">서버에 웹 배포 (및 해당 기본 실행 파일, MSDeploy.exe)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-158">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="c9595-159">이 과정의 일환으로,이 클래스는 웹 배포 처리기를 설치 및 관리 웹 서비스와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-159">As part of this process, it installs the Web Deploy Handler and integrates it with the Web Management Service.</span></span>
- <span data-ttu-id="c9595-160">**.NET Framework 4.0**.</span><span class="sxs-lookup"><span data-stu-id="c9595-160">**.NET Framework 4.0**.</span></span> <span data-ttu-id="c9595-161">이 버전의.NET Framework에 작성 된 응용 프로그램을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-161">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="c9595-162">**ASP.NET MVC 3**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-162">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="c9595-163">MVC 3 응용 프로그램을 실행 해야 하는 어셈블리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-163">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c9595-164">이 연습에는 웹 플랫폼 설치 관리자를 설치 하 여 다양 한 구성 요소를 사용 하 여를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-164">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="c9595-165">웹 플랫폼 설치 관리자를 사용할 필요가 없습니다, 있지만 자동으로 종속성을 검색 하 고 최신 제품 버전을 항상 얻을 수 있도록 설치 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-165">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="c9595-166">자세한 내용은 참조 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/?linkid=9805118)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-166">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>


<span data-ttu-id="c9595-167">**필요한 제품 및 구성 요소를 설치 하려면**</span><span class="sxs-lookup"><span data-stu-id="c9595-167">**To install the required products and components**</span></span>

1. <span data-ttu-id="c9595-168">다운로드 및 설치는 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-168">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="c9595-169">설치가 완료 되 면 웹 플랫폼 설치 관리자는 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-169">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9595-170">웹 플랫폼 설치 관리자에서 언제 든 지 시작할 수 있습니다는 **시작** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="c9595-170">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="c9595-171">이 작업을 수행 하는 **시작** 메뉴를 클릭 **모든 프로그램**, 클릭 하 고 **Microsoft 웹 플랫폼 설치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-171">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="c9595-172">맨 위에 있는 **웹 플랫폼 설치 관리자 3.0** 창 클릭 **제품**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-172">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="c9595-173">왼쪽 탐색 창에서 창에서 클릭 **프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-173">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="c9595-174">에 **Microsoft.NET Framework 4** 행을.NET Framework가 이미 설치 되어 있지 않으면 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-174">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9595-175">이미 설치한 Windows Update를 통해.NET Framework 4.0입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-175">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="c9595-176">제품 또는 구성 요소가 이미 설치 되어 웹 플랫폼 설치 관리자는이 표시할 대체 하 여는 **추가** 단추 텍스트와 함께 **설치 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-176">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. <span data-ttu-id="c9595-177">에 **ASP.NET MVC 3 (Visual Studio 2010)** 행에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-177">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="c9595-178">탐색 창에서 클릭 **서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-178">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="c9595-179">에 **IIS 7 권장 구성** 행에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-179">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="c9595-180">에 **웹 배포 도구 2.1** 행에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-180">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="c9595-181">에 **IIS: 기본 인증** 행에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-181">In the **IIS: Basic Authentication** row, click **Add**.</span></span>
11. <span data-ttu-id="c9595-182">에 **IIS: 관리 서비스** 행에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-182">In the **IIS: Management Service** row, click **Add**.</span></span>
12. <span data-ttu-id="c9595-183">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-183">Click **Install**.</span></span> <span data-ttu-id="c9595-184">웹 플랫폼 설치 관리자를 설치할 모든 관련 된 종속성 & #x 2014; 함께; 제품 & #x 2014의 목록이 표시 됩니다 및 사용 조건에 동의 하 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-184">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. <span data-ttu-id="c9595-185">라이선스 조건을 검토 하 고 사용자가 약관에 동의 하는 경우 클릭 **동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-185">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
14. <span data-ttu-id="c9595-186">설치가 완료 되 면 클릭 **마침**, 한 다음 닫습니다는 **웹 플랫폼 설치 관리자 3.0** 창.</span><span class="sxs-lookup"><span data-stu-id="c9595-186">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="c9595-187">IIS를 설치 하기 전에.NET Framework 4.0을 설치한 경우 실행 해야 합니다는 [ASP.NET IIS 등록 도구](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe)를 IIS와 함께 최신 버전의 ASP.NET 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-187">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="c9595-188">이렇게 하지 않으면, 아무 문제 없이 IIS 정적 콘텐츠 (예: HTML 파일)에서 처리를 찾을 수 있지만 반환 됩니다 **찾을 수 없음 – HTTP 오류 404.0** ASP.NET 콘텐츠를 검색 하려고 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-188">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="c9595-189">ASP.NET 4.0이 등록 되었는지 확인 하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-189">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="c9595-190">**IIS와 ASP.NET 4.0을 등록 하려면**</span><span class="sxs-lookup"><span data-stu-id="c9595-190">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="c9595-191">클릭 **시작**, 한 다음 입력 **명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-191">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="c9595-192">검색 결과에서 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 클릭 하 고 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-192">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="c9595-193">명령 프롬프트 창에서 디렉터리로 이동 된 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-193">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="c9595-194">이 명령을 입력 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-194">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. <span data-ttu-id="c9595-195">언제 든 지 64 비트 웹 응용 프로그램을 호스트 하려는 경우 IIS와 함께 64 비트 버전의 ASP.NET도 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-195">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="c9595-196">명령 프롬프트 창에서이 작업을 수행 하려면 탐색 하 고 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-196">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="c9595-197">이 명령을 입력 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-197">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

<span data-ttu-id="c9595-198">것이 좋습니다도 다시 사용 하 여 Windows Update이 시점에서 다운로드 하 고 새로운 제품 및 이전에 설치한 구성 요소에 대 한 사용 가능한 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-198">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-web-management-service"></a><span data-ttu-id="c9595-199">웹 관리 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="c9595-199">Configure the Web Management Service</span></span>

<span data-ttu-id="c9595-200">필요한 모든 요소를 설치 했으므로 IIS에서 웹 관리 서비스를 구성 하는 다음 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-200">Now that you've installed everything you need, the next step is to configure the Web Management Service in IIS.</span></span> <span data-ttu-id="c9595-201">상위 수준에서 이러한 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-201">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="c9595-202">서버 수준에서 기본 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-202">Enable basic authentication at the server level.</span></span>
- <span data-ttu-id="c9595-203">원격 연결을 허용 하도록 웹 관리 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-203">Configure the Web Management Service to accept remote connections.</span></span>
- <span data-ttu-id="c9595-204">웹 관리 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-204">Start the Web Management Service.</span></span>
- <span data-ttu-id="c9595-205">필요한 웹 관리 서비스 위임 규칙 위치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-205">Check that the required Web Management Service delegation rules are in place.</span></span>

<span data-ttu-id="c9595-206">**웹 관리 서비스를 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="c9595-206">**To configure the Web Management Service**</span></span>

1. <span data-ttu-id="c9595-207">에 **시작** 메뉴에서 **관리 도구**, 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-207">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="c9595-208">IIS 관리자에서에서 **연결** 창에서 서버 노드를 클릭 (예를 들어 **STAGEWEB1**).</span><span class="sxs-lookup"><span data-stu-id="c9595-208">In IIS Manager, in the **Connections** pane, click the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. <span data-ttu-id="c9595-209">가운데 창에서 아래 **IIS**를 두 번 클릭 **인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-209">In the center pane, under **IIS**, double-click **Authentication**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image4.png)
4. <span data-ttu-id="c9595-210">마우스 오른쪽 단추로 클릭 **기본 인증**, 클릭 하 고 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-210">Right-click **Basic Authentication**, and then click **Enable**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. <span data-ttu-id="c9595-211">에 **연결** 창 다시 설정으로 되돌리려면는 최상위 서버 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-211">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
6. <span data-ttu-id="c9595-212">가운데 창에서 아래 **관리**를 두 번 클릭 **관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-212">In the center pane, under **Management**, double-click **Management Service**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. <span data-ttu-id="c9595-213">가운데 창에서 선택 **원격 연결을 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-213">In the center pane, select **Enable remote connections**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9595-214">Web Management Service가 이미 실행 중이면 먼저 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-214">If the Web Management Service is already running, you'll need to stop it first.</span></span>
8. <span data-ttu-id="c9595-215">에 **동작** 창에서 클릭 **시작** 웹 관리 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-215">In the **Actions** pane, click **Start** to start the Web Management Service.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. <span data-ttu-id="c9595-216">설정을 저장 하려면 메시지가 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-216">If you're prompted to save your settings, click **Yes**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9595-217">서비스가 자동으로 시작 되도록 구성 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-217">You may also want to configure the service to start automatically.</span></span> <span data-ttu-id="c9595-218">이 수행 하려면 서비스 콘솔을 열고 마우스 오른쪽 단추로 클릭 **웹 관리 서비스**, 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-218">To do this, open the Services console, right-click **Web Management Service**, and then click **Properties**.</span></span> <span data-ttu-id="c9595-219">에 **시작 유형** 드롭다운 목록에서 선택 **자동**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-219">In the **Startup type** dropdown list, select **Automatic**, and then click **OK**.</span></span>
10. <span data-ttu-id="c9595-220">에 **연결** 창 다시 설정으로 되돌리려면는 최상위 서버 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-220">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
11. <span data-ttu-id="c9595-221">가운데 창에서 아래 **관리**를 두 번 클릭 **관리 서비스 위임**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-221">In the center pane, under **Management**, double-click **Management Service Delegation**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. <span data-ttu-id="c9595-222">가운데 창에는 규칙 집합이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-222">Verify that the center pane contains a set of rules.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    <span data-ttu-id="c9595-223">이러한 규칙에 권한이 있는 웹 관리 서비스 사용자가 다양 한 웹 배포 공급자를 사용 하도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-223">These rules allow authorized Web Management Service users to use various Web Deploy providers.</span></span> <span data-ttu-id="c9595-224">예를 들어, 웹 배포 처리기를 통해 IIS를 웹 응용 프로그램 및 콘텐츠 배포 하려면 있어야 모든 인증 된 웹 관리 서비스 사용자가 사용 하도록 허용 하는 위임 규칙은 **contentPath** 및 **iisApp**  공급자 (스크린 샷에 표시 될 수 있는 마지막 규칙).</span><span class="sxs-lookup"><span data-stu-id="c9595-224">For example, to deploy web applications and content to IIS through the Web Deploy Handler, there must be a delegation rule that allows all authenticated Web Management Service users to use the **contentPath** and **iisApp** providers (the last rule that you can see in the screenshot).</span></span>

    <span data-ttu-id="c9595-225">이 항목에서 설명 하는 순서에 제품 및 구성 요소를 설치한 경우 최신 버전의 웹 배포는 웹 관리 서비스에 모든 필수 위임 규칙을 자동으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-225">If you installed products and components in the order described in this topic, the latest version of Web Deploy should automatically add all the required delegation rules to the Web Management Service.</span></span> <span data-ttu-id="c9595-226">관리 서비스 위임 페이지에는 규칙이 표시 되지 않으면, 사용자가 직접 만든 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-226">If the Management Service Delegation page does not show any rules, you'll need to create them yourself.</span></span> <span data-ttu-id="c9595-227">이 작업을 수행 하는 방법에 지침은 [웹 배포 처리기 구성](https://go.microsoft.com/?linkid=9805124)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-227">For instructions on how to do this, see [Configure the Web Deployment Handler](https://go.microsoft.com/?linkid=9805124).</span></span>
13. <span data-ttu-id="c9595-228">에 **연결** 창 다시 설정으로 되돌리려면는 최상위 서버 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-228">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>

## <a name="create-and-configure-an-iis-website"></a><span data-ttu-id="c9595-229">만들기 및 IIS 웹 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-229">Create and Configure an IIS Website</span></span>

<span data-ttu-id="c9595-230">웹 콘텐츠 서버를 배포 하기 전에 만들고 콘텐츠를 호스팅하는 IIS 웹 사이트를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-230">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="c9595-231">웹 배포가 웹 패키지에서 기존 IIS 웹 사이트;에 배포할 수 있습니다. 웹 사이트를 만들 것 있습니다 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-231">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="c9595-232">관리자가 아닌 계정 콘텐츠를 원격으로 배포할 수 있도록 약간의 추가 구성 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-232">You also need to do a little extra configuration to allow your non-administrator account to deploy content remotely.</span></span> <span data-ttu-id="c9595-233">상위 수준에서 이러한 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-233">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="c9595-234">콘텐츠를 호스트 하는 파일 시스템에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-234">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="c9595-235">콘텐츠를 제공 하도록 IIS 웹 사이트를 만들고 로컬 폴더에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-235">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="c9595-236">로컬 폴더에 응용 프로그램 풀 id에 대 한 읽기 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-236">Grant read permissions to the application pool identity on the local folder.</span></span>
- <span data-ttu-id="c9595-237">웹 응용 프로그램을 배포 하는 도메인 계정에 필요한 IIS 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-237">Grant the necessary IIS permissions to the domain account that will deploy your web application.</span></span>

<span data-ttu-id="c9595-238">를 없지만 아무 IIS에서 기본 웹 사이트에 콘텐츠 배포에서 테스트 또는 데모 시나리오 외에이 방법은 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-238">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="c9595-239">프로덕션 환경을 시뮬레이트하기 위해 새 IIS 웹 사이트 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-239">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="c9595-240">**IIS 웹 사이트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="c9595-240">**To create an IIS website**</span></span>

1. <span data-ttu-id="c9595-241">로컬 파일 시스템에서 콘텐츠를 저장할 폴더를 만듭니다 (예를 들어 **C:\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="c9595-241">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="c9595-242">에 **시작** 메뉴에서 **관리 도구**, 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-242">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="c9595-243">IIS 관리자에서에서 **연결** 창에서 서버 노드를 확장 (예를 들어 **STAGEWEB1**).</span><span class="sxs-lookup"><span data-stu-id="c9595-243">In IIS Manager, in the **Connections** pane, expand the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. <span data-ttu-id="c9595-244">마우스 오른쪽 단추로 클릭는 **사이트** 노드를 차례로 클릭 한 다음 **웹 사이트 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-244">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="c9595-245">에 **사이트 이름** 상자에 IIS 웹 사이트에 대 한 이름을 입력 합니다 (예를 들어 **DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="c9595-245">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="c9595-246">에 **실제 경로** 상자, (찾거나 입력)의 경로를 로컬 폴더 (예를 들어 **C:\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="c9595-246">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="c9595-247">에 **포트** 상자에 웹 사이트를 호스트 하려는 포트 번호를 입력 합니다 (예를 들어 **85**).</span><span class="sxs-lookup"><span data-stu-id="c9595-247">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c9595-248">표준 포트 번호는 80 HTTP 및 HTTPS의 경우 443입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-248">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="c9595-249">그러나 포트 80에서이 웹 사이트를 호스트 하는 경우에 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-249">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="c9595-250">둡니다는 **호스트 이름** 상자를 비워는 웹 사이트에 대 한 도메인 이름 (DNS System) 레코드를 구성 하 고 클릭 하려는 경우가 아니면 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-250">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > <span data-ttu-id="c9595-251">프로덕션 환경에서 가능성이 싶어하는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-251">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="c9595-252">IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [웹 사이트 (IIS 7)에 대 한 호스트 헤더 구성](https://technet.microsoft.com/library/cc753195(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-252">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="c9595-253">Windows Server 2008 r 2에서 DNS 서버 역할에 대 한 자세한 내용은 참조 하십시오. [DNS 서버 개요](https://technet.microsoft.com/en-gb/library/cc770392.aspx) 및 [DNS 서버](https://technet.microsoft.com/windowsserver/dd448607)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-253">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/en-gb/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="c9595-254">**작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-254">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="c9595-255">에 **사이트 바인딩** 대화 상자를 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-255">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. <span data-ttu-id="c9595-256">에 **사이트 바인딩 추가** 대화 상자, 설정 된 **IP 주소** 및 **포트** 기존 사이트 구성과 일치 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-256">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="c9595-257">에 **호스트 이름** 웹 서버의 이름을 입력 합니다 (예를 들어 **STAGEWEB1**)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-257">In the **Host name** box, type the name of your web server (for example, **STAGEWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > <span data-ttu-id="c9595-258">첫 번째 사이트 바인딩을 사용 하면 IP 주소와 포트를 사용 하 여 로컬로 사이트에 액세스할 수 있습니다 또는 `http://localhost:85`합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-258">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="c9595-259">두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름 (예를 들어 http://stageweb1:85)를 사용 하 여 도메인의 다른 컴퓨터에서 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-259">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://stageweb1:85).</span></span>
13. <span data-ttu-id="c9595-260">에 **사이트 바인딩** 대화 상자를 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-260">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="c9595-261">에 **연결** 창에서 클릭 **응용 프로그램 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-261">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="c9595-262">에 **응용 프로그램 풀** 창, 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **기본 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-262">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="c9595-263">기본적으로 응용 프로그램 풀의 이름에는 웹 사이트의 이름과 일치 합니다 (예를 들어 **DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="c9595-263">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="c9595-264">에 **.NET Framework 버전** 목록에서 **.NET Framework v4.0.30319**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-264">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image14.png)

    > [!NOTE]
    > <span data-ttu-id="c9595-265">샘플 솔루션에는.NET Framework 4.0 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-265">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="c9595-266">이것이 웹 배포에 대 한 요구 사항은 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-266">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="c9595-267">콘텐츠를 제공 하도록 웹 사이트를 응용 프로그램 풀 id는 콘텐츠를 저장 하는 로컬 폴더에 대 한 권한이 읽기 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-267">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="c9595-268">IIS 7.5에서 응용 프로그램 풀은 일반적으로 실행 위치는 네트워크 서비스 계정을 사용 하 여 IIS의 이전 버전) (달리 기본적으로 응용 프로그램 풀 고유한 응용 프로그램 풀 id로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-268">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="c9595-269">응용 프로그램 풀 id가 실제 사용자 계정이 아닌 및 사용자 또는 그룹 & #x 2014의 모든 목록에 표시 되지 않습니다; 대신 만들어졌을 동적으로 응용 프로그램 풀을 시작할 때</span><span class="sxs-lookup"><span data-stu-id="c9595-269">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="c9595-270">각 응용 프로그램 풀 id는 로컬에 추가 됩니다 **IIS\_IUSRS** 숨겨진된 항목으로 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-270">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="c9595-271">를 파일이 나 폴더에 응용 프로그램 풀 id에 대 한 권한을 부여 하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-271">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="c9595-272">에 사용 권한을 할당 응용 프로그램 풀 id를 직접 형식을 사용 하 여 **IIS AppPool\***[응용 프로그램 풀 이름] * (예를 들어 **IIS AppPool\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="c9595-272">Assign permissions to the application pool identity directly, using the format **IIS AppPool\***[application pool name]*(for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="c9595-273">권한 할당의 **IIS\_IUSRS** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-273">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="c9595-274">로컬에 사용 권한을 할당 하는 가장 일반적인 방법입니다 **IIS\_IUSRS** 그룹화 하므로이 방법을 사용 하면 파일 시스템 사용 권한 다시 구성 하지 않고 응용 프로그램 풀을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-274">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="c9595-275">다음 절차에는이 그룹 기반 접근 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-275">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="c9595-276">IIS 7.5에서 응용 프로그램 풀 id에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-276">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="c9595-277">**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="c9595-277">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="c9595-278">Windows 탐색기에서 로컬 폴더의 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-278">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="c9595-279">폴더를 마우스 오른쪽 단추로 누른 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-279">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="c9595-280">에 **보안** 탭을 클릭 **편집**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-280">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="c9595-281">클릭 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-281">Click **Locations**.</span></span> <span data-ttu-id="c9595-282">에 **위치** 대화 상자에서 로컬 서버를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-282">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. <span data-ttu-id="c9595-283">에 **사용자 또는 그룹 선택** 대화 상자에서 **IIS\_IUSRS**, 클릭 **이름 확인**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-283">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="c9595-284">에 **에 대 한 권한을 * * * [폴더 이름]* 대화 상자, 새 그룹에 할당 된 통지는 **읽기 &amp; 실행**, **폴더 내용 보기**, 및 **읽기** 권한은 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-284">In the **Permissions for***[folder name]* dialog box, notice that the new group has been assigned the **Read &amp; execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="c9595-285">이 변경 되지 않은 상태로 두고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-285">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="c9595-286">클릭 **확인** 를 닫으려면는 *[폴더 이름] * * * 속성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="c9595-286">Click **OK** to close the *[folder name]***Properties** dialog box.</span></span>

<span data-ttu-id="c9595-287">마지막 작업으로 콘텐츠를 배포 하는 데 사용할 자격 증명에 관리자가 아닌 사용자에 게 적절 한 사용 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-287">As a final task, you must grant the appropriate permissions to the non-administrator user whose credentials you'll use to deploy content.</span></span> <span data-ttu-id="c9595-288">이 사용자는 웹 사이트에 콘텐츠를 원격으로 배포할 수 있는 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-288">This user requires the permissions to deploy content remotely to your website.</span></span>

<span data-ttu-id="c9595-289">**관리자가 아닌 도메인 사용자에 대 한 IIS 웹 사이트 사용 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="c9595-289">**To configure IIS website permissions for a non-administrator domain user**</span></span>

1. <span data-ttu-id="c9595-290">IIS 관리자에서에서 **연결** 창에서 웹 사이트 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **DemoSite**)를 가리키고 **배포**, 클릭 하 고 **웹 구성 배포 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-290">In IIS Manager, in the **Connections** pane, right-click your website node (for example, **DemoSite**), point to **Deploy**, and then click **Configure Web Deploy Publishing**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. <span data-ttu-id="c9595-291">에 **구성할 웹 배포 게시** 의 오른쪽에 대화 상자는 **게시 사용 권한을 부여 하려면 사용자를 선택** 목록에서 줄임표 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-291">In the **Configure Web Deploy Publishing** dialog box, to the right of the **Select a user to give publishing permissions** list, click the ellipsis button.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. <span data-ttu-id="c9595-292">에 **허용 사용자** 대화 상자에서 콘텐츠를 배포 하 고 클릭 한 다음 사용 하려는 계정의 도메인 및 사용자 이름을 입력 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-292">In the **Allow User** dialog box, type the domain and user name of the account you want to use to deploy content, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. <span data-ttu-id="c9595-293">에 **구성할 웹 배포 게시** 대화 상자를 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-293">In the **Configure Web Deploy Publishing** dialog box, click **Setup**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > <span data-ttu-id="c9595-294">이 작업을 한 번에 두 가지 주요 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-294">This operation performs two key functions in one step.</span></span> <span data-ttu-id="c9595-295">첫째, 이전 섹션의 검사 위임 규칙에 따라 웹 관리 서비스를 통해 원격으로 웹 사이트를 수정할 수 있는 사용자 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-295">First, it grants the user permission to modify the website remotely through the Web Management Service, according to the delegation rules you examined in the previous section.</span></span> <span data-ttu-id="c9595-296">둘째, 사용자를 추가, 수정 및 웹 사이트 콘텐츠에 사용 권한을 설정할 수 있는 웹 사이트에 대 한 원본 폴더의 사용자에 게 모든 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-296">Second, it grants the user full control of the source folder for the website, which allows the user to add, modify, and set permissions on the website content.</span></span>
5. <span data-ttu-id="c9595-297">에 **구성할 웹 배포 게시** 대화 상자를 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-297">In the **Configure Web Deploy Publishing** dialog box, click **Close**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="c9595-298">방화벽 예외 구성</span><span class="sxs-lookup"><span data-stu-id="c9595-298">Configure Firewall Exceptions</span></span>

<span data-ttu-id="c9595-299">기본적으로 IIS 웹 관리 서비스는 TCP 8172 포트에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-299">By default, the IIS Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="c9595-300">웹 서버에서 Windows 방화벽을 사용 하는 경우 새 인바운드 규칙을 만들어 8172 포트의 TCP 트래픽을 허용 (Windows 방화벽에서 기본적으로 모든 아웃 바운드 트래픽이 허용) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-300">If Windows Firewall is enabled on your web server, you'll need to create a new inbound rule to allow TCP traffic on port 8172 (all outbound traffic is permitted by default in Windows Firewall).</span></span> <span data-ttu-id="c9595-301">타사 방화벽을 사용 하는 경우 트래픽을 허용 하도록 규칙을 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-301">If you use a third-party firewall, you'll need to create rules to allow traffic.</span></span>

| <span data-ttu-id="c9595-302">방향</span><span class="sxs-lookup"><span data-stu-id="c9595-302">Direction</span></span> | <span data-ttu-id="c9595-303">포트에서</span><span class="sxs-lookup"><span data-stu-id="c9595-303">From Port</span></span> | <span data-ttu-id="c9595-304">이식 하려면</span><span class="sxs-lookup"><span data-stu-id="c9595-304">To Port</span></span> | <span data-ttu-id="c9595-305">포트 유형</span><span class="sxs-lookup"><span data-stu-id="c9595-305">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c9595-306">인바운드</span><span class="sxs-lookup"><span data-stu-id="c9595-306">Inbound</span></span> | <span data-ttu-id="c9595-307">임의의 값</span><span class="sxs-lookup"><span data-stu-id="c9595-307">Any</span></span> | <span data-ttu-id="c9595-308">8172</span><span class="sxs-lookup"><span data-stu-id="c9595-308">8172</span></span> | <span data-ttu-id="c9595-309">TCP</span><span class="sxs-lookup"><span data-stu-id="c9595-309">TCP</span></span> |
| <span data-ttu-id="c9595-310">아웃 바운드</span><span class="sxs-lookup"><span data-stu-id="c9595-310">Outbound</span></span> | <span data-ttu-id="c9595-311">8172</span><span class="sxs-lookup"><span data-stu-id="c9595-311">8172</span></span> | <span data-ttu-id="c9595-312">임의의 값</span><span class="sxs-lookup"><span data-stu-id="c9595-312">Any</span></span> | <span data-ttu-id="c9595-313">TCP</span><span class="sxs-lookup"><span data-stu-id="c9595-313">TCP</span></span> |
  

<span data-ttu-id="c9595-314">Windows 방화벽의 규칙 구성에 대 한 자세한 내용은 참조 하십시오. [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-314">For more information on configuring rules in Windows Firewall, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="c9595-315">타사 방화벽에 대 한 제품 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c9595-315">For third-party firewalls, please consult your product documentation.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c9595-316">결론</span><span class="sxs-lookup"><span data-stu-id="c9595-316">Conclusion</span></span>

<span data-ttu-id="c9595-317">이제 웹 서버 관리 웹 서비스를 통해 웹 배포 처리기에 대 한 원격 배포를 받을 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-317">Your web server should now be ready to accept remote deployments to the Web Deploy Handler through the Web Management Service.</span></span> <span data-ttu-id="c9595-318">서버에 웹 응용 프로그램을 배포 하려고 하기 전에 이러한 주요 사항을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-318">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="c9595-319">IIS에서 서버 수준에서 기본 인증 하도록 설정 했습니까?</span><span class="sxs-lookup"><span data-stu-id="c9595-319">Have you enabled basic authentication at the server level in IIS?</span></span>
- <span data-ttu-id="c9595-320">웹 관리 서비스에 대 한 원격 연결 하도록 설정 했습니까?</span><span class="sxs-lookup"><span data-stu-id="c9595-320">Have you enabled remote connections to the Web Management Service?</span></span>
- <span data-ttu-id="c9595-321">웹 관리 서비스를 시작 하면?</span><span class="sxs-lookup"><span data-stu-id="c9595-321">Have you started the Web Management Service?</span></span>
- <span data-ttu-id="c9595-322">사항이 관리 위임 규칙 서비스 위치에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c9595-322">Are there management service delegation rules in place?</span></span>
- <span data-ttu-id="c9595-323">응용 프로그램 풀 id가 읽기 권한을 웹 사이트에 대 한 원본 폴더에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="c9595-323">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="c9595-324">관리자가 아닌 사용자 계정이 있나요 사이트 수준 사용 권한을 IIS에서?</span><span class="sxs-lookup"><span data-stu-id="c9595-324">Does the non-administrator user account have site-level permissions in IIS?</span></span>
- <span data-ttu-id="c9595-325">프로그램 방화벽이 TCP 포트 8172에서 서버에 대 한 들어오는 연결을 허용 합니까?</span><span class="sxs-lookup"><span data-stu-id="c9595-325">Does your firewall allow incoming connections to the server on TCP port 8172?</span></span>

## <a name="further-reading"></a><span data-ttu-id="c9595-326">추가 정보</span><span class="sxs-lookup"><span data-stu-id="c9595-326">Further Reading</span></span>

<span data-ttu-id="c9595-327">웹 배포 처리기에 웹 패키지를 배포할 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 구성 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9595-327">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Web Deploy Handler, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c9595-328">[이전](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[다음](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="c9595-328">[Previous](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span></span>
