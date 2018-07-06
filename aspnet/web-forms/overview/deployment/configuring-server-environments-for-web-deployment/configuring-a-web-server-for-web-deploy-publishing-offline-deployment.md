---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 게시 (오프 라인 배포) 배포 웹에 대 한 웹 서버 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 오프 라인 웹 게시 및 배포를 지원 하기 위해 IIS 웹 서버를 구성 하는 방법을 설명 합니다. 인터넷 정보 서비스를 사용 하 여 작업할 때 (I....
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: 048cd1855e3f03a6f348521c00acb03ddee8c630
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824676"
---
<a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a><span data-ttu-id="d68b6-104">웹 배포 게시용 (오프 라인 배포) 웹 서버 구성</span><span class="sxs-lookup"><span data-stu-id="d68b6-104">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>
====================
<span data-ttu-id="d68b6-105">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="d68b6-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="d68b6-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="d68b6-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="d68b6-107">이 항목에서는 오프 라인 웹 게시 및 배포를 지원 하기 위해 IIS 웹 서버를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-107">This topic describes how to configure an IIS web server to support offline web publishing and deployment.</span></span>
> 
> <span data-ttu-id="d68b6-108">인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상을 사용 하 여 작업할 때 세 가지 기본 방법을 응용 프로그램 또는 웹 서버에 사이트를 가져오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-108">When you work with Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="d68b6-109">다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-109">You can:</span></span>
> 
> - <span data-ttu-id="d68b6-110">사용 된 *원격 에이전트 서비스를 배포 하는 웹*합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-110">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="d68b6-111">이 접근 방식에서는 웹 서버의 구성이 줄어들기 하지만 아무 것도 서버에 배포 하기 위해 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-111">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="d68b6-112">사용 된 *웹 배포 처리기*합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-112">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="d68b6-113">이 방법은 훨씬 더 복잡 한 이며 웹 서버를 설정 하려면 초기 더 많은 노력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-113">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="d68b6-114">그러나이 방법을 사용 하는 경우에 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-114">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="d68b6-115">웹 배포 처리기만 IIS 7 이상 버전에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-115">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="d68b6-116">사용 하 여 *오프 라인 배포*합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-116">Use *offline deployment*.</span></span> <span data-ttu-id="d68b6-117">이 방법은 웹 서버에 최소 구성이 필요 하지만 서버 관리자가 수동으로 서버로 웹 패키지를 복사 하 고 IIS 관리자를 통해 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-117">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="d68b6-118">주요 기능, 이점 및 이러한 접근 방식의 단점에 대 한 자세한 내용은 참조 하세요. [웹 배포에 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-118">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>


<span data-ttu-id="d68b6-119">예, 네트워크 인프라 또는 보안 제한 사항에 원격 배포가 진행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-119">Yes, if your network infrastructure or security restrictions prevent remote deployment.</span></span> <span data-ttu-id="d68b6-120">이 웹 서버가 격리 되 인터넷 프로덕션 환경의 경우 일 가능성이 가장 큰&#x2014;하거나 물리적으로 또는 하 여 방화벽 및 서브넷&#x2014;서버 인프라의 나머지 부분에서.</span><span class="sxs-lookup"><span data-stu-id="d68b6-120">This is most likely to be the case in Internet-facing production environments, where the web servers are isolated&#x2014;either physically or by firewalls and subnets&#x2014;from the rest of your server infrastructure.</span></span>

<span data-ttu-id="d68b6-121">물론이 방법은 그다지 웹 응용 프로그램을 정기적으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-121">Obviously, this approach becomes less desirable if your web applications are updated on a regular basis.</span></span> <span data-ttu-id="d68b6-122">인프라에서 허용 하는 경우 하려는 원격 배포를 사용 하도록 설정 하는 것이 좋습니다. 웹 배포 처리기 또는 웹 배포 원격 에이전트 서비스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-122">If your infrastructure allows it, you may want to consider enabling remote deployment, using either the Web Deploy Handler or the Web Deploy Remote Agent Service.</span></span>

## <a name="task-overview"></a><span data-ttu-id="d68b6-123">작업 개요</span><span class="sxs-lookup"><span data-stu-id="d68b6-123">Task Overview</span></span>

<span data-ttu-id="d68b6-124">오프 라인 가져오기 및 웹 패키지 배포를 지원 하도록 웹 서버를 구성 하려면를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-124">To configure the web server to support offline import and deployment of web packages, you'll need to:</span></span>

- <span data-ttu-id="d68b6-125">IIS 7.5 및 IIS 7 권장 구성에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-125">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="d68b6-126">웹 배포 2.1 이상을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-126">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="d68b6-127">배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-127">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="d68b6-128">웹 배포 에이전트 서비스를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-128">Disable the Web Deployment Agent Service.</span></span>

<span data-ttu-id="d68b6-129">샘플 솔루션, 특히 호스트도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-129">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="d68b6-130">.NET Framework 4.0을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-130">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="d68b6-131">ASP.NET MVC 3을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-131">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="d68b6-132">이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-132">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="d68b6-133">작업은이 항목의 연습에서는 Windows Server 2008 R2를 실행 하는 새로운 서버 빌드를 사용 하 여 시작 하 고 있음을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-133">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="d68b6-134">계속 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-134">Before you continue, ensure that:</span></span>

- <span data-ttu-id="d68b6-135">Windows Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-135">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="d68b6-136">서버가는 도메인에 가입 된입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-136">The server is domain-joined.</span></span>
- <span data-ttu-id="d68b6-137">서버에 고정 IP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-137">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="d68b6-138">참조 컴퓨터를 도메인에 가입 하는 방법은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-138">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="d68b6-139">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [정적 IP 주소를 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-139">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>


## <a name="install-products-and-components"></a><span data-ttu-id="d68b6-140">제품 및 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-140">Install Products and Components</span></span>

<span data-ttu-id="d68b6-141">이 섹션에서는 웹 서버에서 필요한 제품 및 구성 요소를 설치 하는 과정 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-141">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="d68b6-142">시작 하기 전에 서버에 최신 인지 확인 하려면 Windows Update를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-142">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="d68b6-143">이 경우 이러한 작업을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-143">In this case, you need to install these things:</span></span>

- <span data-ttu-id="d68b6-144">**IIS 7 권장 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-144">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="d68b6-145">이 통해는 **웹 서버 (IIS)** 웹 서버의 역할 IIS 모듈 및 ASP.NET 응용 프로그램을 호스트 하기 위해 필요한 구성 요소 집합을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-145">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="d68b6-146">**.NET Framework 4.0**.</span><span class="sxs-lookup"><span data-stu-id="d68b6-146">**.NET Framework 4.0**.</span></span> <span data-ttu-id="d68b6-147">이 버전의.NET Framework에서 빌드된 응용 프로그램을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-147">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="d68b6-148">**웹 배포 도구 2.1 이상**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-148">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="d68b6-149">서버에 웹 배포 (및 해당 기본 실행 파일, MSDeploy.exe)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-149">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="d68b6-150">웹 배포는 IIS를 통합 하 고 웹 패키지 가져오기 및 내보내기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-150">Web Deploy integrates with IIS and lets you import and export web packages.</span></span>
- <span data-ttu-id="d68b6-151">**ASP.NET MVC 3**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-151">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="d68b6-152">MVC 3 응용 프로그램을 실행 해야 하는 어셈블리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-152">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="d68b6-153">이 연습에서는 웹 플랫폼 설치 관리자를 설치 하 여 다양 한 구성 요소 사용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-153">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="d68b6-154">웹 플랫폼 설치 관리자를 사용 하 여 필요가 있지만 자동으로 종속성을 검색 하 고 제품을 최신 버전 항상 얻을 수를 확인 하 여 설치 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-154">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="d68b6-155">자세한 내용은 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/?linkid=9805118)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-155">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>


<span data-ttu-id="d68b6-156">**필요한 제품 및 구성 요소를 설치 하려면**</span><span class="sxs-lookup"><span data-stu-id="d68b6-156">**To install the required products and components**</span></span>

1. <span data-ttu-id="d68b6-157">다운로드 및 설치 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-157">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="d68b6-158">설치가 완료 되 면 웹 플랫폼 설치 관리자를 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-158">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d68b6-159">웹 플랫폼 설치 관리자에서 언제 든 지 시작할 수 있습니다 합니다 **시작** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="d68b6-159">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="d68b6-160">이 작업을 수행 하는 **시작** 메뉴에서 클릭 **모든 프로그램**를 클릭 하 고 **Microsoft Web Platform Installer**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-160">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="d68b6-161">맨 위에 있는 합니다 **웹 플랫폼 설치 관리자 3.0** 창에서 클릭 **제품**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-161">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="d68b6-162">왼쪽 탐색 창에서 창에서 클릭 **프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-162">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="d68b6-163">에 **Microsoft.NET Framework 4** 행을.NET Framework가 이미 설치 되어 있지 않으면 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-163">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d68b6-164">이미 설치한 Windows Update를 통해.NET Framework 4.0입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-164">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="d68b6-165">제품 또는 구성 요소를 이미 설치 되어 웹 플랫폼 설치 관리자는이 표시할 대체 하 여 합니다 **추가** 텍스트가 있는 단추 **설치 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-165">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. <span data-ttu-id="d68b6-166">에 **ASP.NET MVC 3 (Visual Studio 2010)** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-166">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="d68b6-167">탐색 창에서 클릭 **Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-167">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="d68b6-168">에 **IIS 7 권장 구성** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-168">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="d68b6-169">에 **웹 배포 도구 2.1** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-169">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="d68b6-170">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-170">Click **Install**.</span></span> <span data-ttu-id="d68b6-171">웹 플랫폼 설치 관리자 제품의 목록이 표시 됩니다&#x2014;연결 된 종속성을와 함께&#x2014;를 설치 및 사용 조건에 동의 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-171">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. <span data-ttu-id="d68b6-172">사용 조건을 검토 하 고 사용자가 약관에 동의 하면 클릭 **동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-172">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="d68b6-173">설치가 완료 되 면 클릭 **완료**를 닫은 다음 합니다 **웹 플랫폼 설치 관리자 3.0** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-173">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="d68b6-174">실행 해야 IIS를 설치 하기 전에.NET Framework 4.0을 설치한 경우 합니다 [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) IIS를 사용 하 여 최신 버전의 ASP.NET 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-174">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="d68b6-175">이렇게 하지 않으면, 문제 없이 IIS 정적 콘텐츠 (예: HTML 파일)에서 처리를 찾을 수 있지만 반환 **찾을 수 없음 HTTP 오류 404.0 –** ASP.NET 콘텐츠를 검색 하려고 할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-175">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="d68b6-176">ASP.NET 4.0이 등록 되었는지 확인 하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-176">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="d68b6-177">**IIS를 사용 하 여 ASP.NET 4.0을 등록 하려면**</span><span class="sxs-lookup"><span data-stu-id="d68b6-177">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="d68b6-178">클릭 **시작**를 차례로 **명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-178">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="d68b6-179">검색 결과에서 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 클릭 하 고 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-179">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="d68b6-180">명령 프롬프트 창에서로 이동 합니다 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-180">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="d68b6-181">이 명령을 입력 한 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-181">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. <span data-ttu-id="d68b6-182">언제 든 지 64 비트 웹 응용 프로그램을 호스트 하려는 경우 IIS를 사용 하 여 64 비트 버전의 ASP.NET도 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-182">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="d68b6-183">이렇게 하려면 명령 프롬프트 창에서로 이동 합니다 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-183">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="d68b6-184">이 명령을 입력 한 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-184">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

<span data-ttu-id="d68b6-185">좋은 방법은, Windows 업데이트 다시 사용이 시점에서 다운로드 하 고 새 제품 및 설치한 구성 요소에 대 한 사용 가능한 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-185">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="d68b6-186">IIS 웹 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-186">Configure the IIS Website</span></span>

<span data-ttu-id="d68b6-187">웹 콘텐츠 서버를 배포 하기 전에 만들고 콘텐츠를 호스팅하는 IIS 웹 사이트를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-187">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="d68b6-188">웹 배포는 기존 IIS 웹 사이트에 웹 패키지를 배포만 웹 사이트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-188">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="d68b6-189">높은 수준에서 이러한 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-189">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="d68b6-190">따라서 콘텐츠 호스트 파일 시스템에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-190">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="d68b6-191">콘텐츠를 제공 하는 IIS 웹 사이트를 만들고 로컬 폴더를 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-191">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="d68b6-192">로컬 폴더에 응용 프로그램 풀 id에 대 한 읽기 권한 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-192">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="d68b6-193">없지만 해도 전혀 IIS에서 기본 웹 사이트에 콘텐츠를 배포, 테스트 또는 데모 시나리오 외에이 방법은 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-193">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="d68b6-194">프로덕션 환경을 시뮬레이트하기 위해 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 새 IIS 웹 사이트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-194">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="d68b6-195">**만들기 및 IIS 웹 사이트를 구성 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d68b6-195">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="d68b6-196">로컬 파일 시스템에 콘텐츠를 저장할 폴더를 만듭니다 (예를 들어 **C:\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="d68b6-196">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="d68b6-197">에 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-197">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="d68b6-198">IIS 관리자에서에서 **연결** 창에서 서버 노드를 확장 (예를 들어 **PROWEB1**).</span><span class="sxs-lookup"><span data-stu-id="d68b6-198">In IIS Manager, in the **Connections** pane, expand the server node (for example, **PROWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. <span data-ttu-id="d68b6-199">마우스 오른쪽 단추로 클릭 합니다 **사이트** 노드를 차례로 클릭 한 다음 **웹 사이트 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-199">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="d68b6-200">에 **사이트 이름** 상자에 IIS 웹 사이트에 대 한 이름을 입력 (예를 들어 **DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="d68b6-200">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="d68b6-201">에 **실제 경로** 상자, 형식 (또는 이동) 로컬 폴더에 경로 (예를 들어 **C:\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="d68b6-201">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="d68b6-202">에 **포트** 상자는 웹 사이트를 호스트 하려면 포트 번호를 입력 합니다 (예를 들어 **85**).</span><span class="sxs-lookup"><span data-stu-id="d68b6-202">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d68b6-203">표준 포트 번호로 HTTP 80 및 443 https 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-203">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="d68b6-204">그러나 포트 80에서이 웹 사이트를 호스트 하는 경우에 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-204">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="d68b6-205">유지 된 **호스트 이름** 빈 웹 사이트에 대 한 도메인 이름 시스템 (DNS) 레코드를 구성 하 고 클릭 하려는 경우가 아니면 상자 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-205">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="d68b6-206">프로덕션 환경에서는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성 하 해야 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-206">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="d68b6-207">IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [웹 사이트 (IIS 7)에 대 한 호스트 헤더 구성](https://technet.microsoft.com/library/cc753195(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-207">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="d68b6-208">Windows Server 2008 R2에서 DNS 서버 역할에 대 한 자세한 내용은 참조 하세요. [DNS 서버 개요](https://technet.microsoft.com/en-gb/library/cc770392.aspx) 하 고 [DNS 서버](https://technet.microsoft.com/windowsserver/dd448607)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-208">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/en-gb/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="d68b6-209">**작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-209">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="d68b6-210">에 **사이트 바인딩을** 대화 상자, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-210">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. <span data-ttu-id="d68b6-211">에 **사이트 바인딩 추가** 대화 상자에서를 **IP 주소** 하 고 **포트** 기존 사이트 구성과 일치 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-211">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="d68b6-212">에 **호스트 이름** 상자 웹 서버의 이름을 입력 합니다 (예를 들어 **PROWEB1**)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-212">In the **Host name** box, type the name of your web server (for example, **PROWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="d68b6-213">첫 번째 사이트 바인딩을 사용 하면 IP 주소 및 포트를 사용 하 여 로컬 사이트에 액세스할 수 있습니다 또는 `http://localhost:85`합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-213">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="d68b6-214">두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름을 사용 하 여 도메인의 다른 컴퓨터에서 사이트에 액세스할 수 있습니다 (예를 들어 http://proweb1:85)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-214">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://proweb1:85).</span></span>
13. <span data-ttu-id="d68b6-215">에 **사이트 바인딩을** 대화 상자, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-215">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="d68b6-216">에 **연결** 창 클릭 **응용 프로그램 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-216">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="d68b6-217">에 **응용 프로그램 풀** 창에 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 **기본 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-217">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="d68b6-218">기본적으로 응용 프로그램 풀의 이름에는 웹 사이트의 이름과 일치 합니다 (예를 들어 **DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="d68b6-218">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="d68b6-219">에 **.NET Framework 버전** 목록에서 **.NET Framework v4.0.30319**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-219">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="d68b6-220">샘플 솔루션에는.NET Framework 4.0에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-220">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="d68b6-221">이 요구 사항은 아닙니다 웹 배포에 대 한 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-221">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="d68b6-222">콘텐츠를 제공 하도록 웹 사이트에 대 한 순서 대로 응용 프로그램 풀 id를 콘텐츠를 저장 하는 로컬 폴더에 대 한 권한이 읽기 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-222">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="d68b6-223">IIS 7.5에서 응용 프로그램 풀을 고유한 응용 프로그램 풀 id를 사용 하 여 (이전 버전의 IIS에 응용 프로그램 풀은 일반적으로 실행할 네트워크 서비스 계정 사용)는 달리 기본적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-223">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="d68b6-224">응용 프로그램 풀 id는 실제 사용자 계정이 아니며 사용자 또는 그룹의 모든 목록에 표시 되지 않습니다&#x2014;대신 만들어집니다 동적으로 응용 프로그램 풀 시작 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-224">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="d68b6-225">각 응용 프로그램 풀 id는 로컬에 추가할 **IIS\_IUSRS** 숨겨진된 항목으로 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-225">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="d68b6-226">파일 또는 폴더에 응용 프로그램 풀 id에 대 한 사용 권한을 부여 하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-226">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="d68b6-227">사용 권한을 할당 하 고 응용 프로그램 풀 id를 직접 형식을 사용 하 여 <strong>IIS AppPool\</s o n ><em>[응용 프로그램 풀 이름]</em>(예를 들어 <strong>IIS AppPool\DemoSite</strong>).</span><span class="sxs-lookup"><span data-stu-id="d68b6-227">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="d68b6-228">사용 권한을 할당 합니다 **IIS\_IUSRS** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-228">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="d68b6-229">로컬에 사용 권한을 할당 하는 가장 일반적인 방법입니다 **IIS\_IUSRS** 그룹에 있으므로이 방법을 사용 하면 파일 시스템 사용 권한 다시 구성 하지 않고 응용 프로그램 풀을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-229">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="d68b6-230">다음 절차에는이 그룹 기반 접근 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-230">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="d68b6-231">IIS 7.5에서 응용 프로그램 풀 id에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-231">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="d68b6-232">**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="d68b6-232">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="d68b6-233">Windows 탐색기에서 로컬 폴더의 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-233">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="d68b6-234">폴더를 마우스 오른쪽 단추로 누른 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-234">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="d68b6-235">에 **보안** 탭을 클릭 **편집**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-235">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="d68b6-236">클릭 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-236">Click **Locations**.</span></span> <span data-ttu-id="d68b6-237">에 **위치** 대화 상자에서 로컬 서버를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-237">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. <span data-ttu-id="d68b6-238">에 **사용자 또는 그룹 선택** 대화 상자에서 **IIS\_IUSRS**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-238">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="d68b6-239">에 <strong>에 대 한 권한을</strong><em>[폴더 이름]</em> 대화 상자, 새 그룹에 할당 된 합니다 <strong>읽기 &amp; 실행</strong>, <strong>폴더 나열 내용을</strong>, 및 <strong>읽기</strong> 기본적으로 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="d68b6-239">In the <strong>Permissions for</strong><em>[folder name]</em> dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="d68b6-240">이 변경 되지 않은 상태로 두고 클릭 <strong>확인</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-240">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="d68b6-241">클릭 <strong>확인</strong> 닫으려면 합니다 <em>[폴더 이름]</em><strong>속성</strong> 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d68b6-241">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

## <a name="disable-the-remote-agent-service"></a><span data-ttu-id="d68b6-242">원격 에이전트 서비스를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="d68b6-242">Disable the Remote Agent Service</span></span>

<span data-ttu-id="d68b6-243">웹 배포를 설치할 때 웹 배포 에이전트 서비스가 설치 되어 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-243">When you install Web Deploy, the Web Deployment Agent Service is installed and started automatically.</span></span> <span data-ttu-id="d68b6-244">이 서비스를 사용 하면 배포 하 고 원격 위치에서 웹 패키지를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-244">This service allows you to deploy and publish web packages from a remote location.</span></span> <span data-ttu-id="d68b6-245">중지 하 고 서비스를 사용 하지 않도록 설정 해야 하므로이 시나리오에서는 원격 배포 기능을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-245">You won't be using the remote deployment capability in this scenario, so you should stop and disable the service.</span></span>

> [!NOTE]
> <span data-ttu-id="d68b6-246">가져오기 및 웹 패키지를 수동으로 배포 하려면 원격 에이전트 서비스를 중지 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-246">You don't need to stop the remote agent service in order to import and deploy a web package manually.</span></span> <span data-ttu-id="d68b6-247">그러나 것을 중지 하 고 사용 하지 않으려는 경우 서비스를 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-247">However, it's a good practice to stop and disable the service if you don't plan to use it.</span></span>


<span data-ttu-id="d68b6-248">중지 하 고 다양 한 명령줄 유틸리티 또는 Windows PowerShell cmdlet을 사용 하 여 여러 가지 방법으로 서비스를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-248">You can stop and disable a service in multiple ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="d68b6-249">이 절차는 간단 하 게 UI 기반 접근 방식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-249">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="d68b6-250">**중지 하 고 원격 에이전트 서비스를 사용 하지 않도록 설정**</span><span class="sxs-lookup"><span data-stu-id="d68b6-250">**To stop and disable the remote agent service**</span></span>

1. <span data-ttu-id="d68b6-251">**시작** 메뉴에서 **관리 도구**를 가리킨 다음 **서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-251">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="d68b6-252">서비스 콘솔에서 찾습니다 합니다 **웹 배포 에이전트 서비스가** 행입니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-252">In the Services console, locate the **Web Deployment Agent Service** row.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. <span data-ttu-id="d68b6-253">마우스 오른쪽 단추로 클릭 **웹 배포 에이전트 서비스가**를 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-253">Right-click **Web Deployment Agent Service**, and then click **Properties**.</span></span>
4. <span data-ttu-id="d68b6-254">에 **웹 배포 에이전트 서비스 속성** 대화 상자, 클릭 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-254">In the **Web Deployment Agent Service Properties** dialog box, click **Stop**.</span></span>
5. <span data-ttu-id="d68b6-255">에 **시작 유형** 목록에서 **사용 안 함**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-255">In the **Startup type** list, select **Disabled**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a><span data-ttu-id="d68b6-256">결론</span><span class="sxs-lookup"><span data-stu-id="d68b6-256">Conclusion</span></span>

<span data-ttu-id="d68b6-257">이 시점에서 웹 서버는 오프 라인 웹 패키지 배포용으로 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-257">At this point, your web server is ready for offline web package deployment.</span></span> <span data-ttu-id="d68b6-258">IIS 웹 사이트 웹 패키지를 가져올 하려고 하기 전에 이러한 요점을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d68b6-258">Before you attempt to import web packages to an IIS website, you may want to check these key points:</span></span>

- <span data-ttu-id="d68b6-259">IIS를 사용 하 여 ASP.NET 4.0을 등록 한?</span><span class="sxs-lookup"><span data-stu-id="d68b6-259">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="d68b6-260">응용 프로그램 풀 id를 웹 사이트의 소스 폴더에 읽기 액세스할을 수?</span><span class="sxs-lookup"><span data-stu-id="d68b6-260">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="d68b6-261">웹 배포 에이전트 서비스를 중지 하면?</span><span class="sxs-lookup"><span data-stu-id="d68b6-261">Have you stopped the Web Deployment Agent Service?</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d68b6-262">[이전](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [다음](configuring-a-database-server-for-web-deploy-publishing.md)</span><span class="sxs-lookup"><span data-stu-id="d68b6-262">[Previous](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
[Next](configuring-a-database-server-for-web-deploy-publishing.md)</span></span>
