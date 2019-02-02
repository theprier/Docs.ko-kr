---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 배포 게시용 웹에 대 한 웹 서버 구성 (웹 배포 처리기) | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 게시 및 IIS 웹 배포 Han를 사용 하 여 배포를 지원 하기 위해 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: cf18a8860d34daa23f61e3dde13c2c79c6c0d4a5
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667325"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a><span data-ttu-id="5e6c7-103">웹 배포 게시용 웹 서버 구성(웹 배포 처리기)</span><span class="sxs-lookup"><span data-stu-id="5e6c7-103">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>

[<span data-ttu-id="5e6c7-104">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="5e6c7-104">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="5e6c7-105">이 항목에서는 웹 게시 및 IIS 웹 배포 처리기를 사용 하 여 배포를 지원 하기 위해 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-105">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deploy Handler.</span></span>
> 
> <span data-ttu-id="5e6c7-106">웹 배포 2.0 이상으로 작업할 때 세 가지 기본 방법을 응용 프로그램 또는 웹 서버에 사이트를 가져오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-106">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="5e6c7-107">다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-107">You can:</span></span>
> 
> - <span data-ttu-id="5e6c7-108">사용 된 *원격 에이전트 서비스를 배포 하는 웹*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-108">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="5e6c7-109">이 접근 방식에서는 웹 서버의 구성이 줄어들기 하지만 아무 것도 서버에 배포 하기 위해 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-109">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="5e6c7-110">사용 된 *웹 배포 처리기*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-110">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="5e6c7-111">이 방법은 훨씬 더 복잡 한 이며 웹 서버를 설정 하려면 초기 더 많은 노력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-111">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="5e6c7-112">그러나이 방법을 사용 하는 경우에 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-112">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="5e6c7-113">웹 배포 처리기만 IIS 7 이상 버전에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-113">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="5e6c7-114">사용 하 여 *오프 라인 배포*합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-114">Use *offline deployment*.</span></span> <span data-ttu-id="5e6c7-115">이 방법은 웹 서버에 최소 구성이 필요 하지만 서버 관리자가 수동으로 서버로 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-115">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="5e6c7-116">주요 기능, 이점 및 이러한 접근 방식의 단점에 대 한 자세한 내용은 참조 하세요. [웹 배포에 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-116">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>


<span data-ttu-id="5e6c7-117">예, 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 콘텐츠를 배포 하도록 허용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-117">Yes, if you want to allow non-administrator users to deploy content to specific IIS websites.</span></span> <span data-ttu-id="5e6c7-118">이 방법은 이러한 종류의 시나리오에서 바람직한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-118">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="5e6c7-119">스테이징 또는 프로덕션 환경에서 원격 배포를 트리거하는 사용자 또는 서비스 계정이 서버 관리자의 자격 증명에 대 한 액세스를 갖고 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-119">Staging or production environments, where the person or service account that triggers the remote deployment is unlikely to have access to the credentials of a server administrator.</span></span>
- <span data-ttu-id="5e6c7-120">원격 사용자가 웹 서버 (또는 다른 사람의 웹 사이트에 대 한 액세스)의 모든 권한을 부여 하지 않고 웹 사이트를 업데이트 하는 기능을 제공 하려는 호스팅된 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-120">Hosted environments, where you want to give remote users the ability to update their websites without giving them full control of your web servers (or access to anyone else's websites).</span></span>

<span data-ttu-id="5e6c7-121">개발 또는 테스트 시나리오 또는 소규모 조직에서 서버 관리자 자격 증명을 사용 하 여 콘텐츠 배포 작습니다 종종 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-121">In development or test scenarios, or in smaller organizations, deploying content using server administrator credentials is often less contentious.</span></span> <span data-ttu-id="5e6c7-122">이러한 시나리오에서 사용 하 여 배포를 지원 하도록 웹 서버를 구성 합니다 [웹 배포 된 원격 에이전트 서비스가](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 더 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-122">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Remote Agent Service](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) offers a more straightforward approach.</span></span>

## <a name="task-overview"></a><span data-ttu-id="5e6c7-123">작업 개요</span><span class="sxs-lookup"><span data-stu-id="5e6c7-123">Task Overview</span></span>

<span data-ttu-id="5e6c7-124">허용 및 웹 배포 처리기 방식을 사용 하 여 원격 컴퓨터에서 웹 패키지를 배포 하려면 웹 서버를 구성 하려면를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-124">To configure the web server to accept and deploy web packages from a remote computer using the Web Deploy Handler approach, you'll need to:</span></span>

- <span data-ttu-id="5e6c7-125">만들기 또는 도메인 사용자 계정 ("비관리자 사용자") 배포를 수행 하는 데 사용할 자격 증명을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-125">Create, or choose, a domain user account (the "non-administrator user") whose credentials you'll use to perform deployments.</span></span>
- <span data-ttu-id="5e6c7-126">웹 관리 서비스 및 기본 인증 모듈을 포함 하 여 IIS 7.5를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-126">Install IIS 7.5, including the Web Management Service and the Basic Authentication module.</span></span>
- <span data-ttu-id="5e6c7-127">웹 배포 2.1 이상을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-127">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="5e6c7-128">원격 연결을 허용 하도록 웹 관리 서비스를 구성 하 고 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-128">Configure the Web Management Service to allow remote connections, and start the service.</span></span>
- <span data-ttu-id="5e6c7-129">배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-129">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="5e6c7-130">IIS 관리자에서 웹 사이트에 관리자가 아닌 사용자 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-130">Grant your non-administrator user permissions on your website in IIS Manager.</span></span>
- <span data-ttu-id="5e6c7-131">웹 관리 서비스 위임 규칙을 추가 하 고 관리자가 아닌 사용자 계정의 사용 하 여 웹 사이트 콘텐츠를 변경 하는 서비스를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-131">Ensure that the Web Management Service delegation rules permit the service to add and change website content using your non-administrator user account.</span></span>
- <span data-ttu-id="5e6c7-132">8172 포트에서 들어오는 연결을 허용 하도록 방화벽을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-132">Configure any firewalls to allow incoming connections on port 8172.</span></span>

<span data-ttu-id="5e6c7-133">ContactManager 샘플 솔루션, 특히 호스트도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-133">To host the ContactManager sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="5e6c7-134">.NET Framework 4.0을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-134">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="5e6c7-135">ASP.NET MVC 3을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-135">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="5e6c7-136">이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-136">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="5e6c7-137">작업은이 항목의 연습에서는 Windows Server 2016을 실행 하는 새로운 서버 빌드를 사용 하 여 시작 하 고 있음을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-137">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2016.</span></span> <span data-ttu-id="5e6c7-138">계속 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-138">Before you continue, ensure that:</span></span>

- <span data-ttu-id="5e6c7-139">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5e6c7-139">Windows Server 2016</span></span>
- <span data-ttu-id="5e6c7-140">서버가는 도메인에 가입 된입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-140">The server is domain-joined.</span></span>
- <span data-ttu-id="5e6c7-141">서버에 고정 IP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-141">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="5e6c7-142">참조 컴퓨터를 도메인에 가입 하는 방법은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-142">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="5e6c7-143">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [정적 IP 주소를 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-143">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>


## <a name="install-products-and-components"></a><span data-ttu-id="5e6c7-144">제품 및 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-144">Install Products and Components</span></span>

<span data-ttu-id="5e6c7-145">이 섹션에서는 웹 서버에서 필요한 제품 및 구성 요소를 설치 하는 과정 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-145">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="5e6c7-146">시작 하기 전에 서버에 최신 인지 확인 하려면 Windows Update를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-146">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="5e6c7-147">이 경우 이러한 작업을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-147">In this case, you need to install these things:</span></span>

- <span data-ttu-id="5e6c7-148">**IIS 7 권장 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-148">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="5e6c7-149">이 통해는 **웹 서버 (IIS)** 웹 서버의 역할 IIS 모듈 및 ASP.NET 응용 프로그램을 호스트 하기 위해 필요한 구성 요소 집합을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-149">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="5e6c7-150">**IIS: 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-150">**IIS: Management Service**.</span></span> <span data-ttu-id="5e6c7-151">이 IIS에서 웹 관리 서비스 (WMSvc)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-151">This installs the Web Management Service (WMSvc) in IIS.</span></span> <span data-ttu-id="5e6c7-152">이 서비스는 IIS 웹 사이트의 원격 관리를 사용 하도록 설정 하 고 클라이언트에 웹 배포 처리기 끝점을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-152">This service enables remote management of IIS websites and exposes the Web Deploy Handler endpoint to clients.</span></span>
- <span data-ttu-id="5e6c7-153">**IIS: 기본 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-153">**IIS: Basic Authentication**.</span></span> <span data-ttu-id="5e6c7-154">IIS 기본 인증 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-154">This installs the IIS Basic Authentication module.</span></span> <span data-ttu-id="5e6c7-155">이 그러면 웹 관리 서비스 (WMSvc) 제공한 자격 증명을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-155">This lets the Web Management Service (WMSvc) authenticate the credentials you provide.</span></span>
- <span data-ttu-id="5e6c7-156">**웹 배포 도구 2.1 이상**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-156">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="5e6c7-157">서버에 웹 배포 (및 해당 기본 실행 파일, MSDeploy.exe)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-157">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="5e6c7-158">이 프로세스의 일환으로, 웹 배포 처리기를 설치 하 고 웹 관리 서비스와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-158">As part of this process, it installs the Web Deploy Handler and integrates it with the Web Management Service.</span></span>
- <span data-ttu-id="5e6c7-159">**.NET Framework 4.0**.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-159">**.NET Framework 4.0**.</span></span> <span data-ttu-id="5e6c7-160">이 버전의.NET Framework에서 빌드된 응용 프로그램을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-160">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="5e6c7-161">**ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-161">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="5e6c7-162">MVC 3 응용 프로그램을 실행 해야 하는 어셈블리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-162">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="5e6c7-163">이 연습에서는 웹 플랫폼 설치 관리자를 설치 하 여 다양 한 구성 요소 사용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-163">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="5e6c7-164">웹 플랫폼 설치 관리자를 사용 하 여 필요가 있지만 자동으로 종속성을 검색 하 고 제품을 최신 버전 항상 얻을 수를 확인 하 여 설치 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-164">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="5e6c7-165">자세한 내용은 [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-165">For more information, see [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>


<span data-ttu-id="5e6c7-166">**필요한 제품 및 구성 요소를 설치 하려면**</span><span class="sxs-lookup"><span data-stu-id="5e6c7-166">**To install the required products and components**</span></span>

1. <span data-ttu-id="5e6c7-167">다운로드 및 설치 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-167">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="5e6c7-168">설치가 완료 되 면 웹 플랫폼 설치 관리자를 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-168">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e6c7-169">웹 플랫폼 설치 관리자에서 언제 든 지 시작할 수 있습니다 합니다 **시작** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-169">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="5e6c7-170">이 작업을 수행 하는 **시작** 메뉴에서 클릭 **모든 프로그램**를 클릭 하 고 **Microsoft Web Platform Installer**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-170">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="5e6c7-171">맨 위에 있는 합니다 **웹 플랫폼 설치 관리자** 창에서 클릭 **제품**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-171">At the top of the **Web Platform Installer** window, click **Products**.</span></span>
4. <span data-ttu-id="5e6c7-172">왼쪽 탐색 창에서 창에서 클릭 **프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-172">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="5e6c7-173">에 **Microsoft.NET Framework 4** 행을.NET Framework가 이미 설치 되어 있지 않으면 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-173">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e6c7-174">이미 설치한 Windows Update를 통해.NET Framework 4.0입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-174">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="5e6c7-175">제품 또는 구성 요소를 이미 설치 되어 웹 플랫폼 설치 관리자는이 표시할 대체 하 여 합니다 **추가** 텍스트가 있는 단추 **설치 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-175">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. <span data-ttu-id="5e6c7-176">에 **ASP.NET MVC 3 (Visual Studio 2010)** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-176">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="5e6c7-177">탐색 창에서 클릭 **Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-177">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="5e6c7-178">에 **IIS 7 권장 구성** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-178">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="5e6c7-179">에 **웹 배포 도구 2.1** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-179">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="5e6c7-180">에 **IIS: 기본 인증** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-180">In the **IIS: Basic Authentication** row, click **Add**.</span></span>
11. <span data-ttu-id="5e6c7-181">에 **IIS: 관리 서비스** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-181">In the **IIS: Management Service** row, click **Add**.</span></span>
12. <span data-ttu-id="5e6c7-182">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-182">Click **Install**.</span></span> <span data-ttu-id="5e6c7-183">웹 플랫폼 설치 관리자 제품의 목록이 표시 됩니다&#x2014;연결 된 종속성을와 함께&#x2014;를 설치 및 사용 조건에 동의 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-183">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. <span data-ttu-id="5e6c7-184">사용 조건을 검토 하 고 사용자가 약관에 동의 하면 클릭 **동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-184">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
14. <span data-ttu-id="5e6c7-185">설치가 완료 되 면 클릭 **완료**를 닫은 다음 합니다 **웹 플랫폼 설치 관리자** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-185">When the installation is complete, click **Finish**, and then close the **Web Platform Installer** window.</span></span>

<span data-ttu-id="5e6c7-186">실행 해야 IIS를 설치 하기 전에.NET Framework 4.0을 설치한 경우 합니다 [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) IIS를 사용 하 여 최신 버전의 ASP.NET 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-186">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="5e6c7-187">이렇게 하지 않으면, 문제 없이 IIS 정적 콘텐츠 (예: HTML 파일)에서 처리를 찾을 수 있지만 반환 **찾을 수 없음 HTTP 오류 404.0 –** ASP.NET 콘텐츠를 검색 하려고 할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-187">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="5e6c7-188">ASP.NET 4.0이 등록 되었는지 확인 하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-188">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="5e6c7-189">**IIS를 사용 하 여 ASP.NET 4.0을 등록 하려면**</span><span class="sxs-lookup"><span data-stu-id="5e6c7-189">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="5e6c7-190">클릭 **시작**를 차례로 **명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-190">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="5e6c7-191">검색 결과에서 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 클릭 하 고 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-191">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="5e6c7-192">명령 프롬프트 창에서로 이동 합니다 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-192">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="5e6c7-193">이 명령을 입력 한 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-193">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. <span data-ttu-id="5e6c7-194">언제 든 지 64 비트 웹 응용 프로그램을 호스트 하려는 경우 IIS를 사용 하 여 64 비트 버전의 ASP.NET도 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-194">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="5e6c7-195">이렇게 하려면 명령 프롬프트 창에서로 이동 합니다 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-195">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="5e6c7-196">이 명령을 입력 한 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-196">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

<span data-ttu-id="5e6c7-197">좋은 방법은, Windows 업데이트 다시 사용이 시점에서 다운로드 하 고 새 제품 및 설치한 구성 요소에 대 한 사용 가능한 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-197">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-web-management-service"></a><span data-ttu-id="5e6c7-198">웹 관리 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-198">Configure the Web Management Service</span></span>

<span data-ttu-id="5e6c7-199">이제 필요한 모든 것을 설치한 다음 단계는 IIS에서 웹 관리 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-199">Now that you've installed everything you need, the next step is to configure the Web Management Service in IIS.</span></span> <span data-ttu-id="5e6c7-200">높은 수준에서 이러한 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-200">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="5e6c7-201">서버 수준에서 기본 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-201">Enable basic authentication at the server level.</span></span>
- <span data-ttu-id="5e6c7-202">원격 연결을 허용 하도록 웹 관리 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-202">Configure the Web Management Service to accept remote connections.</span></span>
- <span data-ttu-id="5e6c7-203">웹 관리 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-203">Start the Web Management Service.</span></span>
- <span data-ttu-id="5e6c7-204">필요한 웹 관리 서비스 위임 규칙 충족 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-204">Check that the required Web Management Service delegation rules are in place.</span></span>

<span data-ttu-id="5e6c7-205">**웹 관리 서비스를 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="5e6c7-205">**To configure the Web Management Service**</span></span>

1. <span data-ttu-id="5e6c7-206">에 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-206">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="5e6c7-207">IIS 관리자에서에서 **연결** 창에서 서버 노드를 클릭 (예를 들어 **STAGEWEB1**).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-207">In IIS Manager, in the **Connections** pane, click the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. <span data-ttu-id="5e6c7-208">가운데 창에서 아래 **IIS**를 두 번 클릭 **인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-208">In the center pane, under **IIS**, double-click **Authentication**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. <span data-ttu-id="5e6c7-209">마우스 오른쪽 단추로 클릭 **기본 인증**를 클릭 하 고 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-209">Right-click **Basic Authentication**, and then click **Enable**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. <span data-ttu-id="5e6c7-210">에 **연결** 창 다시 돌아가려면 최상위 수준 설정을 서버 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-210">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
6. <span data-ttu-id="5e6c7-211">가운데 창에서 아래 **Management**를 두 번 클릭 **관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-211">In the center pane, under **Management**, double-click **Management Service**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. <span data-ttu-id="5e6c7-212">가운데 창에서 선택 **원격 연결을 사용 하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-212">In the center pane, select **Enable remote connections**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e6c7-213">웹 관리 서비스를 이미 실행 중이면 먼저 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-213">If the Web Management Service is already running, you'll need to stop it first.</span></span>
8. <span data-ttu-id="5e6c7-214">에 **동작** 창 클릭 **시작** 웹 관리 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-214">In the **Actions** pane, click **Start** to start the Web Management Service.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. <span data-ttu-id="5e6c7-215">클릭 설정을 저장할지 묻는 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-215">If you're prompted to save your settings, click **Yes**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e6c7-216">자동으로 시작 되도록 서비스를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-216">You may also want to configure the service to start automatically.</span></span> <span data-ttu-id="5e6c7-217">이렇게 하려면 서비스 콘솔을 열고 마우스 오른쪽 단추로 클릭 **Web Management Service**를 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-217">To do this, open the Services console, right-click **Web Management Service**, and then click **Properties**.</span></span> <span data-ttu-id="5e6c7-218">에 **시작 유형** 드롭다운 목록에서 **자동**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-218">In the **Startup type** dropdown list, select **Automatic**, and then click **OK**.</span></span>
10. <span data-ttu-id="5e6c7-219">에 **연결** 창 다시 돌아가려면 최상위 수준 설정을 서버 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-219">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
11. <span data-ttu-id="5e6c7-220">가운데 창에서 아래 **관리**를 두 번 클릭 **관리 서비스 위임**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-220">In the center pane, under **Management**, double-click **Management Service Delegation**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. <span data-ttu-id="5e6c7-221">가운데 창 규칙 집합이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-221">Verify that the center pane contains a set of rules.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    <span data-ttu-id="5e6c7-222">이러한 규칙에는 권한 있는 웹 관리 서비스 사용자가 다양 한 웹 배포 공급자를 사용 하도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-222">These rules allow authorized Web Management Service users to use various Web Deploy providers.</span></span> <span data-ttu-id="5e6c7-223">예를 들어, 웹 배포 처리기를 통해 IIS에 웹 응용 프로그램 및 콘텐츠 배포에 있어야 모든 인증 된 웹 관리 서비스 사용자가 사용 하도록 허용 하는 위임 규칙을 **contentPath** 고 **iisApp**  공급자 (스크린샷에서 볼 수 있는 마지막 규칙).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-223">For example, to deploy web applications and content to IIS through the Web Deploy Handler, there must be a delegation rule that allows all authenticated Web Management Service users to use the **contentPath** and **iisApp** providers (the last rule that you can see in the screenshot).</span></span>

    <span data-ttu-id="5e6c7-224">이 항목에서 설명 하는 순서로 제품 및 구성 요소를 설치한 경우 최신 버전의 웹 배포는 웹 관리 서비스에 필요한 위임 규칙을 모두 자동으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-224">If you installed products and components in the order described in this topic, the latest version of Web Deploy should automatically add all the required delegation rules to the Web Management Service.</span></span> <span data-ttu-id="5e6c7-225">관리 서비스 위임 페이지에는 모든 규칙 표시 되지 않으면, 직접 만들 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-225">If the Management Service Delegation page does not show any rules, you'll need to create them yourself.</span></span> <span data-ttu-id="5e6c7-226">이 작업을 수행 하는 방법에 지침은 [웹 배포 처리기 구성](https://go.microsoft.com/?linkid=9805124)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-226">For instructions on how to do this, see [Configure the Web Deployment Handler](https://go.microsoft.com/?linkid=9805124).</span></span>
13. <span data-ttu-id="5e6c7-227">에 **연결** 창 다시 돌아가려면 최상위 수준 설정을 서버 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-227">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>

## <a name="create-and-configure-an-iis-website"></a><span data-ttu-id="5e6c7-228">만들기 및 IIS 웹 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-228">Create and Configure an IIS Website</span></span>

<span data-ttu-id="5e6c7-229">웹 콘텐츠 서버를 배포 하기 전에 만들고 콘텐츠를 호스팅하는 IIS 웹 사이트를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-229">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="5e6c7-230">웹 배포는 기존 IIS 웹 사이트에 웹 패키지를 배포만 웹 사이트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-230">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="5e6c7-231">관리자가 아닌 계정의 콘텐츠를 원격으로 배포할 수 있도록 약간 추가 구성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-231">You also need to do a little extra configuration to allow your non-administrator account to deploy content remotely.</span></span> <span data-ttu-id="5e6c7-232">높은 수준에서 이러한 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-232">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="5e6c7-233">따라서 콘텐츠 호스트 파일 시스템에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-233">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="5e6c7-234">콘텐츠를 제공 하는 IIS 웹 사이트를 만들고 로컬 폴더를 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-234">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="5e6c7-235">로컬 폴더에 응용 프로그램 풀 id에 대 한 읽기 권한 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-235">Grant read permissions to the application pool identity on the local folder.</span></span>
- <span data-ttu-id="5e6c7-236">웹 응용 프로그램을 배포 하는 도메인 계정에 필요한 IIS 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-236">Grant the necessary IIS permissions to the domain account that will deploy your web application.</span></span>

<span data-ttu-id="5e6c7-237">없지만 해도 전혀 IIS에서 기본 웹 사이트에 콘텐츠를 배포, 테스트 또는 데모 시나리오 외에이 방법은 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-237">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="5e6c7-238">프로덕션 환경을 시뮬레이트하기 위해 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 새 IIS 웹 사이트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-238">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="5e6c7-239">**IIS 웹 사이트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="5e6c7-239">**To create an IIS website**</span></span>

1. <span data-ttu-id="5e6c7-240">로컬 파일 시스템에 콘텐츠를 저장할 폴더를 만듭니다 (예를 들어 **C:\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-240">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="5e6c7-241">에 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-241">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="5e6c7-242">IIS 관리자에서에서 **연결** 창에서 서버 노드를 확장 (예를 들어 **STAGEWEB1**).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-242">In IIS Manager, in the **Connections** pane, expand the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. <span data-ttu-id="5e6c7-243">마우스 오른쪽 단추로 클릭 합니다 **사이트** 노드를 차례로 클릭 한 다음 **웹 사이트 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-243">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="5e6c7-244">에 **사이트 이름** 상자에 IIS 웹 사이트에 대 한 이름을 입력 (예를 들어 **DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-244">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="5e6c7-245">에 **실제 경로** 상자, 형식 (또는 이동) 로컬 폴더에 경로 (예를 들어 **C:\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-245">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="5e6c7-246">에 **포트** 상자는 웹 사이트를 호스트 하려면 포트 번호를 입력 합니다 (예를 들어 **85**).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-246">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e6c7-247">표준 포트 번호로 HTTP 80 및 443 https 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-247">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="5e6c7-248">그러나 포트 80에서이 웹 사이트를 호스트 하는 경우에 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-248">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="5e6c7-249">유지 된 **호스트 이름** 빈 웹 사이트에 대 한 도메인 이름 시스템 (DNS) 레코드를 구성 하 고 클릭 하려는 경우가 아니면 상자 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-249">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > <span data-ttu-id="5e6c7-250">프로덕션 환경에서는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성 하 해야 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-250">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="5e6c7-251">IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [웹 사이트 (IIS 7)에 대 한 호스트 헤더 구성](https://technet.microsoft.com/library/cc753195(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-251">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="5e6c7-252">Windows Server에서 DNS 서버 역할에 대 한 자세한 내용은 참조 하세요. [DNS 서버 개요](https://technet.microsoft.com/en-gb/library/cc770392.aspx) 하 고 [DNS 서버](https://technet.microsoft.com/windowsserver/dd448607)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-252">For more information on the DNS Server role in Windows Server, see [DNS Server Overview](https://technet.microsoft.com/en-gb/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="5e6c7-253">**작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-253">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="5e6c7-254">에 **사이트 바인딩을** 대화 상자, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-254">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. <span data-ttu-id="5e6c7-255">에 **사이트 바인딩 추가** 대화 상자에서를 **IP 주소** 하 고 **포트** 기존 사이트 구성과 일치 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-255">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="5e6c7-256">에 **호스트 이름** 상자 웹 서버의 이름을 입력 합니다 (예를 들어 **STAGEWEB1**)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-256">In the **Host name** box, type the name of your web server (for example, **STAGEWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > <span data-ttu-id="5e6c7-257">첫 번째 사이트 바인딩을 사용 하면 IP 주소 및 포트를 사용 하 여 로컬 사이트에 액세스할 수 있습니다 또는 `http://localhost:85`합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-257">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="5e6c7-258">두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름을 사용 하 여 도메인의 다른 컴퓨터에서 사이트에 액세스할 수 있습니다 (예를 들어 http://stageweb1:85)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-258">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://stageweb1:85).</span></span>
13. <span data-ttu-id="5e6c7-259">에 **사이트 바인딩을** 대화 상자, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-259">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="5e6c7-260">에 **연결** 창 클릭 **응용 프로그램 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-260">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="5e6c7-261">에 **응용 프로그램 풀** 창에 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 **기본 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-261">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="5e6c7-262">기본적으로 응용 프로그램 풀의 이름에는 웹 사이트의 이름과 일치 합니다 (예를 들어 **DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-262">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="5e6c7-263">에 **.NET CLR 버전** 목록에서 **.NET CLR v4.0.30319**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-263">In the **.NET CLR version** list, select **.NET CLR v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > <span data-ttu-id="5e6c7-264">샘플 솔루션에는.NET Framework 4.0에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-264">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="5e6c7-265">이 요구 사항은 아닙니다 웹 배포에 대 한 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-265">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="5e6c7-266">콘텐츠를 제공 하도록 웹 사이트에 대 한 순서 대로 응용 프로그램 풀 id를 콘텐츠를 저장 하는 로컬 폴더에 대 한 권한이 읽기 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-266">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="5e6c7-267">IIS 7.5에서 응용 프로그램 풀을 고유한 응용 프로그램 풀 id를 사용 하 여 (이전 버전의 IIS에 응용 프로그램 풀은 일반적으로 실행할 네트워크 서비스 계정 사용)는 달리 기본적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-267">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="5e6c7-268">응용 프로그램 풀 id는 실제 사용자 계정이 아니며 사용자 또는 그룹의 모든 목록에 표시 되지 않습니다&#x2014;대신 만들어집니다 동적으로 응용 프로그램 풀 시작 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-268">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="5e6c7-269">각 응용 프로그램 풀 id는 로컬에 추가할 **IIS\_IUSRS** 숨겨진된 항목으로 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-269">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="5e6c7-270">파일 또는 폴더에 응용 프로그램 풀 id에 대 한 사용 권한을 부여 하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-270">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="5e6c7-271">사용 권한을 할당 하 고 응용 프로그램 풀 id를 직접 형식을 사용 하 여 <strong>IIS AppPool\</s o n ><em>[응용 프로그램 풀 이름]</em>(예를 들어 <strong>IIS AppPool\DemoSite</strong>).</span><span class="sxs-lookup"><span data-stu-id="5e6c7-271">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="5e6c7-272">사용 권한을 할당 합니다 **IIS\_IUSRS** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-272">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="5e6c7-273">로컬에 사용 권한을 할당 하는 가장 일반적인 방법입니다 **IIS\_IUSRS** 그룹에 있으므로이 방법을 사용 하면 파일 시스템 사용 권한 다시 구성 하지 않고 응용 프로그램 풀을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-273">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="5e6c7-274">다음 절차에는이 그룹 기반 접근 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-274">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="5e6c7-275">IIS 7.5에서 응용 프로그램 풀 id에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-275">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="5e6c7-276">**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="5e6c7-276">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="5e6c7-277">Windows 탐색기에서 로컬 폴더의 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-277">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="5e6c7-278">폴더를 마우스 오른쪽 단추로 누른 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-278">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="5e6c7-279">에 **보안** 탭을 클릭 **편집**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-279">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="5e6c7-280">클릭 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-280">Click **Locations**.</span></span> <span data-ttu-id="5e6c7-281">에 **위치** 대화 상자에서 로컬 서버를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-281">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. <span data-ttu-id="5e6c7-282">에 **사용자 또는 그룹 선택** 대화 상자에서 **IIS\_IUSRS**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-282">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="5e6c7-283">에 <strong>에 대 한 권한을</strong><em>[폴더 이름]</em> 대화 상자, 새 그룹에 할당 된 합니다 <strong>읽기 &amp; 실행</strong>, <strong>폴더 나열 내용을</strong>, 및 <strong>읽기</strong> 기본적으로 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-283">In the <strong>Permissions for</strong><em>[folder name]</em> dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="5e6c7-284">이 변경 되지 않은 상태로 두고 클릭 <strong>확인</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-284">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="5e6c7-285">클릭 <strong>확인</strong> 닫으려면 합니다 <em>[폴더 이름]</em><strong>속성</strong> 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-285">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

<span data-ttu-id="5e6c7-286">작업을 마지막으로 콘텐츠를 배포 하는 데 사용할 자격 증명 관리자가 아닌 사용자에 게 적절 한 권한의 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-286">As a final task, you must grant the appropriate permissions to the non-administrator user whose credentials you'll use to deploy content.</span></span> <span data-ttu-id="5e6c7-287">이 사용자는 웹 사이트에 콘텐츠를 원격으로 배포 하는 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-287">This user requires the permissions to deploy content remotely to your website.</span></span>

<span data-ttu-id="5e6c7-288">**관리자가 아닌 도메인 사용자에 대 한 IIS 웹 사이트 사용 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="5e6c7-288">**To configure IIS website permissions for a non-administrator domain user**</span></span>

1. <span data-ttu-id="5e6c7-289">IIS 관리자에서에 **연결** 창 웹 사이트 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **DemoSite**)를 가리키도록 **배포**, 클릭 하 고 **웹 구성 배포 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-289">In IIS Manager, in the **Connections** pane, right-click your website node (for example, **DemoSite**), point to **Deploy**, and then click **Configure Web Deploy Publishing**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. <span data-ttu-id="5e6c7-290">에 **구성 웹 배포 게시** 대화 상자에서 오른쪽에는 **게시 권한을 부여 하려면 사용자를 선택** 목록에서 줄임표 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-290">In the **Configure Web Deploy Publishing** dialog box, to the right of the **Select a user to give publishing permissions** list, click the ellipsis button.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. <span data-ttu-id="5e6c7-291">에 **허용 사용자** 대화 상자를 사용 하 여 콘텐츠를 배포 하 고 클릭 하려는 계정의 도메인 및 사용자 이름을 입력 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-291">In the **Allow User** dialog box, type the domain and user name of the account you want to use to deploy content, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. <span data-ttu-id="5e6c7-292">에 **구성할 웹 배포 게시** 대화 상자, 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-292">In the **Configure Web Deploy Publishing** dialog box, click **Setup**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > <span data-ttu-id="5e6c7-293">이 작업을 한 번에 두 가지 주요 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-293">This operation performs two key functions in one step.</span></span> <span data-ttu-id="5e6c7-294">먼저 이전 섹션에서 검사 위임 규칙에 따라 웹 관리 서비스를 통해 원격으로 웹 사이트를 수정할 수 있는 사용자 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-294">First, it grants the user permission to modify the website remotely through the Web Management Service, according to the delegation rules you examined in the previous section.</span></span> <span data-ttu-id="5e6c7-295">둘째, 웹 사이트를 추가, 수정 및 웹 사이트 콘텐츠에 대해 사용 권한을 설정할 수 있는 원본 폴더의 전체 사용자 정의 컨트롤을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-295">Second, it grants the user full control of the source folder for the website, which allows the user to add, modify, and set permissions on the website content.</span></span>
5. <span data-ttu-id="5e6c7-296">에 **구성할 웹 배포 게시** 대화 상자, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-296">In the **Configure Web Deploy Publishing** dialog box, click **Close**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="5e6c7-297">방화벽 예외 구성</span><span class="sxs-lookup"><span data-stu-id="5e6c7-297">Configure Firewall Exceptions</span></span>

<span data-ttu-id="5e6c7-298">기본적으로 IIS 웹 관리 서비스 8172 TCP 포트에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-298">By default, the IIS Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="5e6c7-299">웹 서버에서 Windows 방화벽이 사용 되는 경우 새 인바운드 규칙을 하려면 8172 포트의 TCP 트래픽을 허용 (Windows 방화벽에서 기본적으로 모든 아웃 바운드 트래픽은 허용 됨)을 만들려고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-299">If Windows Firewall is enabled on your web server, you'll need to create a new inbound rule to allow TCP traffic on port 8172 (all outbound traffic is permitted by default in Windows Firewall).</span></span> <span data-ttu-id="5e6c7-300">타사 방화벽을 사용 하는 경우 트래픽을 허용 하도록 규칙을 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-300">If you use a third-party firewall, you'll need to create rules to allow traffic.</span></span>

| <span data-ttu-id="5e6c7-301">방향</span><span class="sxs-lookup"><span data-stu-id="5e6c7-301">Direction</span></span> | <span data-ttu-id="5e6c7-302">포트에서</span><span class="sxs-lookup"><span data-stu-id="5e6c7-302">From Port</span></span> | <span data-ttu-id="5e6c7-303">포트</span><span class="sxs-lookup"><span data-stu-id="5e6c7-303">To Port</span></span> | <span data-ttu-id="5e6c7-304">포트 유형</span><span class="sxs-lookup"><span data-stu-id="5e6c7-304">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e6c7-305">인바운드</span><span class="sxs-lookup"><span data-stu-id="5e6c7-305">Inbound</span></span> | <span data-ttu-id="5e6c7-306">임의의 값</span><span class="sxs-lookup"><span data-stu-id="5e6c7-306">Any</span></span> | <span data-ttu-id="5e6c7-307">8172</span><span class="sxs-lookup"><span data-stu-id="5e6c7-307">8172</span></span> | <span data-ttu-id="5e6c7-308">TCP</span><span class="sxs-lookup"><span data-stu-id="5e6c7-308">TCP</span></span> |
| <span data-ttu-id="5e6c7-309">아웃바운드</span><span class="sxs-lookup"><span data-stu-id="5e6c7-309">Outbound</span></span> | <span data-ttu-id="5e6c7-310">8172</span><span class="sxs-lookup"><span data-stu-id="5e6c7-310">8172</span></span> | <span data-ttu-id="5e6c7-311">임의의 값</span><span class="sxs-lookup"><span data-stu-id="5e6c7-311">Any</span></span> | <span data-ttu-id="5e6c7-312">TCP</span><span class="sxs-lookup"><span data-stu-id="5e6c7-312">TCP</span></span> |
  

<span data-ttu-id="5e6c7-313">Windows 방화벽에서 규칙 구성에 대 한 자세한 내용은 참조 하세요. [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-313">For more information on configuring rules in Windows Firewall, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="5e6c7-314">타사 방화벽 제품 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-314">For third-party firewalls, please consult your product documentation.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5e6c7-315">결론</span><span class="sxs-lookup"><span data-stu-id="5e6c7-315">Conclusion</span></span>

<span data-ttu-id="5e6c7-316">이제 웹 서버에 웹 배포 처리기 웹 관리 서비스를 통해 원격 배포를 받을 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-316">Your web server should now be ready to accept remote deployments to the Web Deploy Handler through the Web Management Service.</span></span> <span data-ttu-id="5e6c7-317">서버에 웹 응용 프로그램을 배포 하기 전에 이러한 요점을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-317">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="5e6c7-318">IIS에서 서버 수준에서 기본 인증 하도록 설정 했습니까?</span><span class="sxs-lookup"><span data-stu-id="5e6c7-318">Have you enabled basic authentication at the server level in IIS?</span></span>
- <span data-ttu-id="5e6c7-319">웹 관리 서비스에 대 한 원격 연결 하도록 설정 했습니까?</span><span class="sxs-lookup"><span data-stu-id="5e6c7-319">Have you enabled remote connections to the Web Management Service?</span></span>
- <span data-ttu-id="5e6c7-320">웹 관리 서비스 시작 하셨나요?</span><span class="sxs-lookup"><span data-stu-id="5e6c7-320">Have you started the Web Management Service?</span></span>
- <span data-ttu-id="5e6c7-321">사항이 관리 위임 규칙을 서비스 위치에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="5e6c7-321">Are there management service delegation rules in place?</span></span>
- <span data-ttu-id="5e6c7-322">응용 프로그램 풀 id를 웹 사이트의 소스 폴더에 읽기 액세스할을 수?</span><span class="sxs-lookup"><span data-stu-id="5e6c7-322">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="5e6c7-323">관리자가 아닌 사용자 계정의 권한이 사이트 수준에서 IIS?</span><span class="sxs-lookup"><span data-stu-id="5e6c7-323">Does the non-administrator user account have site-level permissions in IIS?</span></span>
- <span data-ttu-id="5e6c7-324">에 방화벽이 TCP 포트 8172 서버에 대 한 들어오는 연결 허용 합니까?</span><span class="sxs-lookup"><span data-stu-id="5e6c7-324">Does your firewall allow incoming connections to the server on TCP port 8172?</span></span>

## <a name="further-reading"></a><span data-ttu-id="5e6c7-325">추가 정보</span><span class="sxs-lookup"><span data-stu-id="5e6c7-325">Further Reading</span></span>

<span data-ttu-id="5e6c7-326">웹 배포 처리기에 웹 패키지를 배포 하기 위해 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 구성 하는 방법에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6c7-326">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Web Deploy Handler, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5e6c7-327">[이전](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [다음](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="5e6c7-327">[Previous](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span></span>
