---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 만들고 컬렉션의 서버에서 웹 서버 팜을 구성 하는 팜 프레임 워크 WFF (웹) 2.0을 사용 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: ad557306cb4d3c62932c640b598f82d692bc74cf
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388295"
---
<a name="creating-a-server-farm-with-the-web-farm-framework"></a><span data-ttu-id="f8004-103">웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기</span><span class="sxs-lookup"><span data-stu-id="f8004-103">Creating a Server Farm with the Web Farm Framework</span></span>
====================
<span data-ttu-id="f8004-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="f8004-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="f8004-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="f8004-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="f8004-106">이 항목에서는 만들고 컬렉션의 서버에서 웹 서버 팜을 구성 하는 팜 프레임 워크 WFF (웹) 2.0을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-106">This topic describes how to use the Web Farm Framework (WFF) 2.0 to create and configure a web server farm from a collection of servers.</span></span>


<span data-ttu-id="f8004-107">WFF를 사용 하면 여러 부하 분산 된 웹 서버에서 웹 플랫폼 제품 및 구성 요소, 웹 응용 프로그램, 웹 사이트 및 구성 설정을 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-107">WFF lets you synchronize web platform products and components, web applications, websites, and configuration settings across multiple load-balanced web servers.</span></span> <span data-ttu-id="f8004-108">스테이징 및 프로덕션 환경에서 같은 둘 이상의 웹 서버를 해야 하는 시나리오에서 배포 및 구성 프로세스를 크게 간소화할 수 있습니다이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-108">In scenarios where you need more than one web server, like staging and production environments, this can vastly simplify your deployment and configuration process.</span></span> <span data-ttu-id="f8004-109">단일 서버에 웹 응용 프로그램을 배포할 수 있습니다&#x2014;는 *주 서버*&#x2014;및 WFF 서버 팜의 모든 다른 웹 서버에서 해당 웹 응용 프로그램에 자동으로 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-109">You can deploy a web application to a single server&#x2014;the *primary server*&#x2014;and WFF will automatically replicate that web application on all the other web servers in the server farm.</span></span>

## <a name="understanding-the-web-farm-framework"></a><span data-ttu-id="f8004-110">웹 팜 프레임 워크 이해</span><span class="sxs-lookup"><span data-stu-id="f8004-110">Understanding the Web Farm Framework</span></span>

<span data-ttu-id="f8004-111">프로 비전, 관리 및 웹 서버 그룹에 콘텐츠를 배포 하려면 WFF 2.0을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-111">You can use WFF 2.0 to provision, manage, and deploy content to a group of web servers.</span></span> <span data-ttu-id="f8004-112">세 가지 주요 서버 역할의 WFF 배포 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-112">A WFF deployment consists of three key server roles:</span></span>

- <span data-ttu-id="f8004-113">합니다 *컨트롤러 서버*합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-113">The *controller server*.</span></span> <span data-ttu-id="f8004-114">이 서버를 사용 하 여 만들고 WFF 서버 팜을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-114">You use this server to create and configure WFF server farms.</span></span> <span data-ttu-id="f8004-115">Controller 서버를 웹 플랫폼 구성 요소, 구성 설정 및 서버 팜의 웹 서버 사이 응용 프로그램의 동기화를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-115">The controller server manages the synchronization of web platform components, configuration settings, and applications between the web servers in a server farm.</span></span> <span data-ttu-id="f8004-116">컨트롤러 서버의 WFF 2.0을 설치 하 고 컨트롤러 서버는 각 서버 팜의 서버에 WFF 에이전트를 설치에 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-116">You install WFF 2.0 on the controller server, and the controller server will in turn install the WFF agent on each of the servers in a server farm.</span></span> <span data-ttu-id="f8004-117">WFF 서버 팜에, controller 서버를 개념적으로 속하지 및 단일 컨트롤러 서버에는 여러 서버 팜을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-117">The controller server does not conceptually belong to any WFF server farm, and a single controller server can manage multiple server farms.</span></span> <span data-ttu-id="f8004-118">이 시나리오에서는 준비 서버 팜 및 프로덕션 서버 팜 만들기 및 관리를 단일 WFF 컨트롤러 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-118">In this scenario, you use a single WFF controller server to create and manage the staging server farm and the production server farm.</span></span>
- <span data-ttu-id="f8004-119">합니다 *주 서버*합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-119">The *primary server*.</span></span> <span data-ttu-id="f8004-120">각 WFF 서버 팜에 단일 주 서버를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-120">Each WFF server farm includes a single primary server.</span></span> <span data-ttu-id="f8004-121">웹 플랫폼 구성 요소를 설치 하거나 주 서버에 응용 프로그램을 배포할 때의 WFF 서버 팜의 다른 모든 서버에 변경 내용을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-121">When you install web platform components or deploy applications to the primary server, the WFF synchronizes your changes to all the other servers in the server farm.</span></span>
- <span data-ttu-id="f8004-122">합니다 *보조 서버*합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-122">The *secondary server*.</span></span> <span data-ttu-id="f8004-123">각 WFF 서버 팜에서 하나 이상의 보조 서버가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-123">Each WFF server farm includes one or more secondary servers.</span></span> <span data-ttu-id="f8004-124">서버 팜 내에서 모든 보조 서버를 주 서버로 변경 내용이 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-124">Any changes you make to the primary server are replicated to every secondary server within the server farm.</span></span>

<span data-ttu-id="f8004-125">이러한 서버 역할 Fabrikam, Inc. 스테이징 및 프로덕션 환경에 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-125">This shows how these server roles relate to the Fabrikam, Inc. staging and production environments:</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

<span data-ttu-id="f8004-126">이 시나리오에서는 프로덕션 환경과 스테이징 환경 둘 다로 구성 됩니다 WFF 서버 팜.</span><span class="sxs-lookup"><span data-stu-id="f8004-126">In this scenario, the staging environment and the production environment are both configured as WFF server farms.</span></span> <span data-ttu-id="f8004-127">단일 WFF 컨트롤러 서버 팜 모두 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-127">A single WFF controller server manages both farms.</span></span> <span data-ttu-id="f8004-128">각 서버 팜 내에서 주 서버로 변경 내용을 모든 보조 서버에 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-128">Within each server farm, any changes to the primary server are replicated to every secondary server.</span></span>

<span data-ttu-id="f8004-129">스테이징 및 프로덕션 환경을 구성 하려면 먼저 WFF 2.0의 주요 개념을 숙지 하려면 다음이 문서를 읽는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-129">Before you start to configure your staging and production environments, we recommend that you read these articles to familiarize yourself with the key concepts of WFF 2.0:</span></span>

- [<span data-ttu-id="f8004-130">IIS 7에 대 한 Web Farm Framework 2.0의 개요</span><span class="sxs-lookup"><span data-stu-id="f8004-130">Overview of the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805126)
- [<span data-ttu-id="f8004-131">IIS 7에 대 한 Web Farm Framework 2.0을 사용 하 여 서버 팜을 설정</span><span class="sxs-lookup"><span data-stu-id="f8004-131">Setting up a Server Farm with the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805127)
- [<span data-ttu-id="f8004-132">시스템 및 IIS 7에 대 한 Web Farm Framework 2.0에 대 한 플랫폼 요구 사항</span><span class="sxs-lookup"><span data-stu-id="f8004-132">System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a><span data-ttu-id="f8004-133">작업 개요</span><span class="sxs-lookup"><span data-stu-id="f8004-133">Task Overview</span></span>

<span data-ttu-id="f8004-134">작업은이 항목의 연습을 완료 하려면 3 개 이상의 서버가 해야&#x2014;하나의 WFF 컨트롤러, 서버 팜에 대 한 하나의 기본 웹 서버 및 서버 팜에 대 한 하나 이상의 보조 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-134">To complete the tasks and walkthroughs in this topic, you'll need at least three servers&#x2014;one WFF controller, one primary web server for the server farm, and one or more secondary web servers for the server farm.</span></span> <span data-ttu-id="f8004-135">언제 든 지 WFF 서버 팜에 보조 서버를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-135">You can add more secondary servers to a WFF server farm at any time.</span></span> <span data-ttu-id="f8004-136">높은 수준, 만들기 및 구성 해야 하는 스테이징 또는 프로덕션의 환경의 WFF 서버 팜:</span><span class="sxs-lookup"><span data-stu-id="f8004-136">At a high level, to create and configure a WFF server farm for your staging or production environment you'll need to:</span></span>

- <span data-ttu-id="f8004-137">인터넷 정보 서비스 (IIS) 7.5 및 WFF 2.0을 설치 하 여 컨트롤러 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-137">Create a controller server by installing Internet Information Services (IIS) 7.5 and WFF 2.0.</span></span>
- <span data-ttu-id="f8004-138">일반적인 관리자 계정을 만들고 방화벽 예외를 구성 하 여 기본 및 보조 서버를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-138">Prepare primary and secondary servers by creating a common administrator account and configuring firewall exceptions.</span></span>
- <span data-ttu-id="f8004-139">컨트롤러 서버의 IIS 관리자를 사용 하 여 서버 팜을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-139">Configure the server farm by using IIS Manager on the controller server.</span></span>
- <span data-ttu-id="f8004-140">부하 분산 IIS 응용 프로그램 요청 라우팅 (ARR) 또는 대체는 부하 분산 기술을 사용 하 여 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-140">Configure load balancing using IIS Application Request Routing (ARR) or an alternative load-balancing technology.</span></span>

<span data-ttu-id="f8004-141">작업은이 항목의 연습에서는 Windows Server 2008 R2를 실행 하는 새로운 서버 빌드를 사용 하 여 시작 하 고 있음을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-141">The tasks and walkthroughs in this topic assume that you're starting with clean server builds running Windows Server 2008 R2.</span></span> <span data-ttu-id="f8004-142">를 시작 하기 전에 각 서버에 대 한을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-142">Before you begin, for each server, ensure that:</span></span>

- <span data-ttu-id="f8004-143">Windows Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-143">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="f8004-144">서버가는 도메인에 가입 된입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-144">The server is domain-joined.</span></span>
- <span data-ttu-id="f8004-145">서버에 고정 IP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-145">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="f8004-146">참조 컴퓨터를 도메인에 가입 하는 방법은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-146">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="f8004-147">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [정적 IP 주소를 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-147">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>


## <a name="create-the-wff-controller-server"></a><span data-ttu-id="f8004-148">WFF 컨트롤러 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="f8004-148">Create the WFF Controller Server</span></span>

<span data-ttu-id="f8004-149">WFF 컨트롤러 서버를 만들려면 IIS 7 이상 및 WFF 2.0 이상을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-149">To create a WFF controller server, you'll need to install both IIS 7 or later and WFF 2.0 or later.</span></span> <span data-ttu-id="f8004-150">내부적으로 WFF (웹 배포)는 IIS 웹 배포 도구를 사용 2.x 팜에 서버를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-150">Under the covers, WFF uses the IIS Web Deployment Tool (Web Deploy) 2.x to synchronize the servers in your farm.</span></span> <span data-ttu-id="f8004-151">WFF를 설치 하려면 웹 플랫폼 설치 관리자를 사용 하는 경우 설치 관리자를 자동으로 다운로드를 Web Deploy를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-151">If you use the Web Platform Installer to install WFF, the installer will automatically download and install Web Deploy for you.</span></span>

<span data-ttu-id="f8004-152">**WFF 컨트롤러 서버를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="f8004-152">**To create the WFF controller server**</span></span>

1. <span data-ttu-id="f8004-153">다운로드 및 설치 합니다 [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9739157)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-153">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9739157).</span></span>
2. <span data-ttu-id="f8004-154">맨 위에 있는 합니다 **웹 플랫폼 설치 관리자 3.0** 창에서 클릭 **제품**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-154">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="f8004-155">왼쪽 탐색 창에서 창에서 클릭 **Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-155">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="f8004-156">에 **IIS 7 권장 구성** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-156">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
5. <span data-ttu-id="f8004-157">에 <strong>웹 팜 프레임 워크 2.</strong> <em>x</em> 행을 클릭 <strong>추가</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-157">In the <strong>Web Farm Framework 2.</strong><em>x</em> row, click <strong>Add</strong>.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. <span data-ttu-id="f8004-158">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-158">Click **Install**.</span></span> <span data-ttu-id="f8004-159">웹 플랫폼 설치 관리자가 목록에 추가할 다른 다양 한 종속성과 함께 웹 배포 도구를 설치 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-159">Notice that the Web Platform Installer has added the Web Deployment Tool, along with various other dependencies, to the installation list.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. <span data-ttu-id="f8004-160">사용 조건을 검토 하 고 사용자가 약관에 동의 하면 클릭 **동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-160">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
8. <span data-ttu-id="f8004-161">설치가 완료 되 면 클릭 **완료**를 닫은 다음 합니다 **웹 플랫폼 설치 관리자 3.0** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-161">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

## <a name="configure-the-primary-and-secondary-servers"></a><span data-ttu-id="f8004-162">기본 및 보조 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-162">Configure the Primary and Secondary Servers</span></span>

<span data-ttu-id="f8004-163">WFF 서버 팜을 만들려면 팜의 구성 하는 웹 서버에서 몇 가지 준비 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-163">Before you create a WFF server farm, you should complete some preparation tasks on the web servers that will make up the farm:</span></span>

- <span data-ttu-id="f8004-164">수 있도록 방화벽 예외를 추가 합니다 **Core Networking**, **원격 관리**, 및 **파일 및 프린터 공유** WFF 컨트롤러 서버와 통신 하는 기능 .</span><span class="sxs-lookup"><span data-stu-id="f8004-164">Add firewall exceptions to allow the **Core Networking**, **Remote Administration**, and **File and Printer Sharing** features to communicate with the WFF controller server.</span></span>
- <span data-ttu-id="f8004-165">도메인 계정을 만듭니다 (예를 들어 **FABRIKAM\stagingfarm**) Active Directory에서 각 서버의 로컬 관리자 그룹에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-165">Create a domain account (for example, **FABRIKAM\stagingfarm**) in Active Directory and add it to the local administrators group on each server.</span></span> <span data-ttu-id="f8004-166">서버 팜 관리자 계정으로이 계정은 사용 하 여 서버 팜을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-166">You'll use this account as the server farm administrator account when you create the server farm.</span></span>

<span data-ttu-id="f8004-167">Windows 방화벽에서 이러한 방화벽 예외를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [시스템 및 IIS 7에 대 한 Web Farm Framework 2.0에 대 한 플랫폼 요구 사항](https://go.microsoft.com/?linkid=9805128)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-167">For more information on how to configure these firewall exceptions in Windows Firewall, see [System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805128).</span></span> <span data-ttu-id="f8004-168">다른 방화벽 시스템, 제품 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8004-168">For other firewall systems, consult your product documentation.</span></span>

<span data-ttu-id="f8004-169">Windows Server 2008 R2의 로컬 관리자 그룹에 도메인 계정을 추가 하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-169">You can use the next procedure to add a domain account to the local administrators group in Windows Server 2008 R2.</span></span> <span data-ttu-id="f8004-170">서버 팜에 추가 하려는 모든 서버에서이 절차를 수행 해야 하면&#x2014;즉, 각 보조 서버 및 주 서버에서 로컬 관리자 그룹에 동일한 도메인 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-170">You should perform this procedure on every server that you want to add to the server farm&#x2014;in other words, add the same domain account to the local administrators group on the primary server and on each secondary server.</span></span>

<span data-ttu-id="f8004-171">**로컬 관리자 그룹에 도메인 계정을 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="f8004-171">**To add a domain account to the local administrators group**</span></span>

1. <span data-ttu-id="f8004-172">에 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **서버 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-172">On the **Start** menu, point to **Administrative Tools**, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="f8004-173">에 **서버 관리자** 창의 트리 뷰 창에서 확장 **구성**를 확장 **로컬 사용자 및 그룹**를 클릭 하 고 **그룹**.</span><span class="sxs-lookup"><span data-stu-id="f8004-173">In the **Server Manager** window, in the tree view pane, expand **Configuration**, expand **Local Users and Groups**, and then click **Groups**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. <span data-ttu-id="f8004-174">에 **그룹** 창에 두 번 클릭 **관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-174">In the **Groups** pane, double-click **Administrators**.</span></span>
4. <span data-ttu-id="f8004-175">에 **관리자 속성** 대화 상자, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-175">In the **Administrators Properties** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="f8004-176">에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자, 형식 (또는 찾아보기) 도메인 계정에 (예를 들어 **FABRIKAM\stagingfarm**)를 클릭 하 고 **확인**.</span><span class="sxs-lookup"><span data-stu-id="f8004-176">In the **Select Users, Computers, Service Accounts, or Groups** dialog box, type (or browse) to your domain account (for example, **FABRIKAM\stagingfarm**), and then click **OK**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. <span data-ttu-id="f8004-177">에 **관리자 속성** 대화 상자, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-177">In the **Administrators Properties** dialog box, click **OK**.</span></span>

<span data-ttu-id="f8004-178">서버를 서버 팜에 추가할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-178">Your servers are now ready to be added to a server farm.</span></span> <span data-ttu-id="f8004-179">주 서버에서의 경우 전 서버 팜을 만든 후 또는 응용 프로그램 요구 사항에 맞게 서버를 구성할 수 있습니다&#x2014;두 경우 모두는 WFF는 동기화 서버 제품, 구성 요소에 같거나 구성 배포 하 여 보조 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-179">In the case of the primary server, you can configure the server to meet your application requirements before or after you create the server farm&#x2014;in both cases, the WFF will synchronize the servers by deploying the same products, components, or configuration to your secondary servers.</span></span> <span data-ttu-id="f8004-180">편의상이 자습서에서는 서버 팜 만들기를 마쳤으면 주 서버를 구성 하겠습니다을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-180">For the sake of simplicity, this tutorial assumes that you'll configure the primary server when you've finished creating the server farm.</span></span>

## <a name="create-the-wff-server-farm"></a><span data-ttu-id="f8004-181">WFF 서버 팜 만들기</span><span class="sxs-lookup"><span data-stu-id="f8004-181">Create the WFF Server Farm</span></span>

<span data-ttu-id="f8004-182">이 시점에서 모든 서버 준비가 WFF 서버 팜에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-182">At this point, all your servers are ready to be added to a WFF server farm:</span></span>

- <span data-ttu-id="f8004-183">WFF 컨트롤러 서버에 설치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-183">You've installed WFF on the controller server.</span></span>
- <span data-ttu-id="f8004-184">기본 및 보조 웹 서버에서 방화벽 예외를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-184">You've configured firewall exceptions on your primary and secondary web servers.</span></span>
- <span data-ttu-id="f8004-185">기본 및 보조 웹 서버에서 로컬 관리자 그룹에 도메인 계정을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-185">You've added a domain account to the local administrators group on your primary and secondary web servers.</span></span>

<span data-ttu-id="f8004-186">다음 단계 WFF에서 서버 팜을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-186">The next step is to create the server farm in WFF.</span></span> <span data-ttu-id="f8004-187">WFF 컨트롤러 서버의 IIS 관리자에서이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-187">You can do this from IIS Manager on the WFF controller server.</span></span>

<span data-ttu-id="f8004-188">**WFF 서버 팜을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="f8004-188">**To create a WFF server farm**</span></span>

1. <span data-ttu-id="f8004-189">WFF 컨트롤러 서버의는 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **인터넷 정보 서비스 (IIS) 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-189">On the WFF controller server, on the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="f8004-190">에 **연결** 창, 로컬 서버 노드를 마우스 오른쪽 단추로 클릭 **서버 팜**를 클릭 하 고 **서버 팜 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-190">In the **Connections** pane, expand the local server node, right-click **Server Farms**, and then click **Create Server Farm**.</span></span>
3. <span data-ttu-id="f8004-191">에 **서버 팜 만들기** 대화 상자 서버 팜에 대 한 의미 있는 이름을 입력 합니다 (예를 들어 **스테이징 팜**), 선택한 후 **서버 팜 프로 비전**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-191">In the **Create Server Farm** dialog box, type a meaningful name for the server farm (for example, **Staging Farm**), and then select **Provision server farm**.</span></span>
4. <span data-ttu-id="f8004-192">사용자 이름 및 각 서버의 로컬 관리자 그룹에 추가한 도메인 계정의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-192">Type the user name and password of the domain account that you added to the local administrators group on each server.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. <span data-ttu-id="f8004-193">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-193">Click **Next**.</span></span>
6. <span data-ttu-id="f8004-194">에 **서버 추가** 페이지 선택 주 서버의 정규화 된 도메인 이름 (FQDN)을 입력 **주 서버**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-194">On the **Add Servers** page, type the fully qualified domain name (FQDN) of the primary server, select **Primary Server**, and then click **Add**.</span></span>
7. <span data-ttu-id="f8004-195">이 시점에서 WFF 제공한 자격 증명을 사용 하 여 주 서버에 연결 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-195">At this point, WFF will attempt to contact the primary server using the credentials you provided.</span></span> <span data-ttu-id="f8004-196">연결에 성공 하는 경우 주 서버를 추가할 테이블에는 **서버 추가** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-196">If the connection succeeds, the primary server will be added to the table on the **Add Servers** page.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="f8004-197">보았을 것입니다 **부하 분산에 사용할 수 있는** 기본적으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-197">You might have noticed that **Server is available for Load Balancing** is selected by default.</span></span> <span data-ttu-id="f8004-198">WFF 부하 분산을 구현 하 여 여러 서버 팜에 웹 서버 요청을 분산 함으로써 IIS ARR 모듈을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-198">WFF uses the IIS ARR module to implement load balancing and thereby distribute requests across the web servers in your server farm.</span></span> <span data-ttu-id="f8004-199">대부분의 경우에만 선택을 취소 합니다 **부하 분산에 사용할 수 있는** 타사 부하 분산 솔루션을 대신 사용 하려는 경우 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-199">In most scenarios, you'd only clear the **Server is available for Load Balancing** option if you wanted to use a third-party load balancing solution instead.</span></span>
8. <span data-ttu-id="f8004-200">에 **서버 추가** 페이지에서 첫 번째 보조 서버의 FQDN을 입력 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-200">On the **Add Servers** page, type the FQDN of your first secondary server, and then click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. <span data-ttu-id="f8004-201">팜에 추가 보조 서버에 대해 7 단계를 반복 하 고 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-201">Repeat step 7 for any additional secondary servers in your farm, and then click **Finish**.</span></span>

<span data-ttu-id="f8004-202">WFF 서버 팜 작동 되 고 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-202">Your WFF server farm is now up and running.</span></span> <span data-ttu-id="f8004-203">모든 웹 플랫폼 제품 또는 주 서버에서 모든 웹 응용 프로그램 또는 주 서버에 배포 하는 콘텐츠를 설치 하는 구성 요소 자동으로 프로 비전 할 모든 보조 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-203">Any web platform products or components that you install on the primary server, and any web applications or content that you deploy to the primary server, will be automatically provisioned on all your secondary servers.</span></span>

<span data-ttu-id="f8004-204">WFF 광범위 하 고 복잡 한 항목은 및에서 자세히 알아보십시오 합니다 [IIS 7 용 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-204">WFF is a broad and complex topic, and you can learn more about it on the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span> <span data-ttu-id="f8004-205">그러나 당분간, 가지 주의 해야 하는 두 가지 기능 영역</span><span class="sxs-lookup"><span data-stu-id="f8004-205">For the time being, however, there are two features areas that you need to be aware of:</span></span>

- <span data-ttu-id="f8004-206">*응용 프로그램 프로 비전* 서버 팜의 모든 보조 서버에서 웹 응용 프로그램 및 구성 설정과 같은 기본 서버에서 콘텐츠를 복제 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-206">*Application provisioning* is the process that replicates content from the primary server, like web applications and configuration settings, across all the secondary servers in the server farm.</span></span> <span data-ttu-id="f8004-207">예를 들어, 기본 스테이징 서버로 Contact Manager 샘플 솔루션을 배포 하는 경우 WFF 응용 프로그램 프로 비전 프로세스는 모든 보조 준비 서버에이 솔루션을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-207">For example, if you deploy the Contact Manager sample solution to your primary staging server, the WFF application provisioning process will deploy this solution to all your secondary staging servers.</span></span> <span data-ttu-id="f8004-208">응용 프로그램 프로 비전 프로세스는 기본적으로 30 초 마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-208">By default, the application provisioning process runs every 30 seconds.</span></span>
- <span data-ttu-id="f8004-209">*플랫폼 프로 비전* 웹 플랫폼 제품 및 주 서버에서 구성 요소 서버 팜의 모든 보조 서버를 동기화 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-209">*Platform provisioning* is the process that synchronizes web platform products and components from the primary server to all the secondary servers in the server farm.</span></span> <span data-ttu-id="f8004-210">예를 들어, 기본 스테이징 서버에서 ASP.NET MVC 3을 설치 하는 경우 플랫폼 프로 비전 프로세스는 웹 플랫폼 설치 관리자를 모든 보조 준비 서버에서 ASP.NET MVC 3을 설치 하려면 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-210">For example, if you install ASP.NET MVC 3 on your primary staging server, the platform provisioning process will use the Web Platform Installer to install ASP.NET MVC 3 on all your secondary staging servers.</span></span> <span data-ttu-id="f8004-211">플랫폼 프로 비전 프로세스는 기본적으로 5 분 마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-211">By default, the platform provisioning process runs every five minutes.</span></span>

<span data-ttu-id="f8004-212">관리할 수 있습니다 기본 응용 프로그램 및 플랫폼 프로 비전 설정 IIS 관리자에서 WFF 컨트롤러 서버.</span><span class="sxs-lookup"><span data-stu-id="f8004-212">You can manage basic application and platform provisioning settings from IIS Manager on your WFF controller server.</span></span>

<span data-ttu-id="f8004-213">**응용 프로그램 및 설정을 프로 비전 하는 플랫폼 탐색**</span><span class="sxs-lookup"><span data-stu-id="f8004-213">**Explore application and platform provisioning settings**</span></span>

1. <span data-ttu-id="f8004-214">IIS 관리자에서에 **연결** 창의 서버 팜을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-214">In IIS Manager, in the **Connections** pane, select your server farm.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. <span data-ttu-id="f8004-215">에 **팜을** 창 두 번 클릭 **응용 프로그램 프로 비전**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-215">In the **Server Farm** pane, double-click **Application Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. <span data-ttu-id="f8004-216">알 수 있듯이 서버 팜의 주 서버와 보조 서버 간의 웹 콘텐츠 및 구성 설정을 30 초 마다 동기화를 현재 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-216">As you can see, the server farm is currently configured to synchronize web content and configuration settings between the primary server and the secondary servers every 30 seconds.</span></span>
4. <span data-ttu-id="f8004-217">클릭 **다시**를 차례로 클릭 한 다음 **플랫폼 프로 비전**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-217">Click **Back**, and then double-click **Platform Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. <span data-ttu-id="f8004-218">알 수 있듯이 서버 팜의 현재 웹 플랫폼 제품 및 구성 요소는 주 서버와 보조 서버 간에 5 분 마다 동기화 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-218">As you can see, the server farm is currently configured to synchronize web platform products and components between the primary server and the secondary servers every five minutes.</span></span>
6. <span data-ttu-id="f8004-219">클릭 **다시**입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-219">Click **Back**.</span></span>
7. <span data-ttu-id="f8004-220">서버 팜의 웹 플랫폼 제품을 즉시 동기화를 강제로는 **동작** 창 클릭 **프로 비전 플랫폼**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-220">To force the server farm to synchronize web platform products immediately, in the **Actions** pane, click **Provision Platform**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > <span data-ttu-id="f8004-221">플랫폼 프로 비전 하는 데 시간이 소요 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-221">Platform provisioning may take some time.</span></span> <span data-ttu-id="f8004-222">설치 관리자 프로세스 서버 팜의 보조 서버의 백그라운드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-222">The installer process runs in the background on the secondary servers in your server farm.</span></span>
8. <span data-ttu-id="f8004-223">프로 비전 프로세스를 완료 하려면 충분 한 시간을 허용한 후에 제품 및 주 서버에 추가한 구성 요소는 보조 서버에서 복제 이제 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-223">Once you've allowed sufficient time for the provisioning process to complete, you can verify that the products and components that you added to the primary server have now been replicated on the secondary servers.</span></span> <span data-ttu-id="f8004-224">보조 서버에 로그온을 사용 하는 예를 들어 합니다 **서버 관리자** 창 웹 서버 역할 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-224">For example, you can log on to a secondary server and use the **Server Manager** window to verify that the web server role has been installed.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. <span data-ttu-id="f8004-225">또한 다양 한 웹 플랫폼 구성 요소를 추가한 적이 있는지를 확인 하려면 설치 된 프로그램 목록을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-225">You can also check the installed programs list to verify that various web platform components have been added.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a><span data-ttu-id="f8004-226">부하 분산 구성</span><span class="sxs-lookup"><span data-stu-id="f8004-226">Configure Load Balancing</span></span>

<span data-ttu-id="f8004-227">웹 팜을 만들면 일종의 로드 균형 조정 웹 서버 간에 HTTP 요청을 분산로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-227">When you create a web farm, you need to set up some form of load balancing to distribute HTTP requests between your web servers.</span></span> <span data-ttu-id="f8004-228">Windows Server 2008 네트워크 부하 분산, IIS ARR 또는 타사 소프트웨어 또는 하드웨어 기반 부하 분산 솔루션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-228">This could be Windows Server 2008 network load balancing, IIS ARR, or a third-party software-based or hardware-based load balancing solution.</span></span>

<span data-ttu-id="f8004-229">WFF는 IIS arr.와 밀접 하 게 통합 되도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-229">WFF is designed to integrate closely with IIS ARR.</span></span> <span data-ttu-id="f8004-230">이 통합을 활용 하려면 WFF 컨트롤러 서버에 ARR 모듈을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-230">To take advantage of this integration, you need to install the ARR module on the WFF controller server.</span></span> <span data-ttu-id="f8004-231">하 한 다음 직접 컨트롤러 서버에 모든 웹 트래픽을 일반적으로 도메인 이름 시스템 (DNS) 레코드를 구성 하 여.</span><span class="sxs-lookup"><span data-stu-id="f8004-231">You then direct all your web traffic to the controller server, typically by configuring Domain Name System (DNS) records.</span></span> <span data-ttu-id="f8004-232">Controller 서버를 서버 가용성 및 기타 다양 한 조건에 따라 팜에 서버 사이에서 들어오는 요청을 분산 한 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-232">The controller server will then distribute incoming requests among the servers in your farm, based on server availability and various other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="f8004-233">WFF;를 사용 하 여 ARR을 사용할 필요가 없습니다. WFF 타사 부하 분산 솔루션을 사용 하 여 작동 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-233">You don't have to use ARR with WFF; you can configure WFF to work with third-party load balancing solutions.</span></span> <span data-ttu-id="f8004-234">자세한 내용은 [IIS 7에 대 한 Web Farm Framework 2.0의 개요](https://go.microsoft.com/?linkid=9805126)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-234">For more information, see [Overview of the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805126).</span></span>


<span data-ttu-id="f8004-235">ARR을 사용 하 여 부하 분산는 복잡 한 주제를 가장는이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-235">Load balancing using ARR is a complex topic, most of which is beyond the scope of this tutorial.</span></span> <span data-ttu-id="f8004-236">그러나 ARR 모듈을 설치 하 고 로드 균형 조정을 시작 하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-236">However, you can use the next procedure to install the ARR module and get started with load balancing.</span></span>

<span data-ttu-id="f8004-237">**WFF 컨트롤러 서버에 부하 분산을 설정 하려면**</span><span class="sxs-lookup"><span data-stu-id="f8004-237">**To set up load balancing on the WFF controller server**</span></span>

1. <span data-ttu-id="f8004-238">WFF 컨트롤러 서버에서 웹 플랫폼 설치 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-238">On the WFF controller server, launch the Web Platform Installer.</span></span>
2. <span data-ttu-id="f8004-239">맨 위에 있는 합니다 **웹 플랫폼 설치 관리자 3.0** 창에서 클릭 **제품**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-239">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="f8004-240">왼쪽 탐색 창에서 창에서 클릭 **Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-240">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="f8004-241">에 **응용 프로그램 요청 라우팅 2.5** 행을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-241">In the **Application Request Routing 2.5** row, click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. <span data-ttu-id="f8004-242">클릭 **설치**에 대 한 지침을 따릅니다 합니다 **웹 플랫폼 설치** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-242">Click **Install**, and then follow the instructions in the **Web Platform Installation** window.</span></span>
6. <span data-ttu-id="f8004-243">설치가 완료 되 면 IIS 관리자를 시작 및 합니다 **연결** 창 서버 팜에 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-243">When the installation is complete, launch IIS Manager, and in the **Connections** pane, click your server farm node.</span></span> <span data-ttu-id="f8004-244">여러 새 아이콘에 추가 된 합니다 **팜을** 창.</span><span class="sxs-lookup"><span data-stu-id="f8004-244">Notice that several new icons have been added to the **Server Farm** pane.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. <span data-ttu-id="f8004-245">에 **팜을** 창 두 번 클릭 **부하 분산**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-245">In the **Server Farm** pane, double-click **Load Balance**.</span></span>
8. <span data-ttu-id="f8004-246">에 **부하 분산** 창의 선택 부하 분산 알고리즘 (예를 들어 **요청과 이상**).</span><span class="sxs-lookup"><span data-stu-id="f8004-246">In the **Load Balance** pane, select a load balance algorithm (for example, **Least current request**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="f8004-247">부하 분산 알고리즘 및 기타 구성 설정에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 요청 라우팅 모듈이](https://go.microsoft.com/?linkid=9805130)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-247">For more information on load balancing algorithms and other configuration settings, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. <span data-ttu-id="f8004-248">에 **동작** 창 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-248">In the **Actions** pane, click **Apply**.</span></span>

<span data-ttu-id="f8004-249">이제 기본 서버 팜의 서버에 대 한 분산을 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-249">You have now configured basic load balancing for the servers in your server farm.</span></span> <span data-ttu-id="f8004-250">하 여 웹 팜 컨트롤러 서버에 모든 트래픽을 직접, 하는 경우 요청 선택한 부하 분산 알고리즘 및 가용성에 따라 팜에 서버 간에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-250">If you direct all your web farm traffic to the controller server, the requests will be distributed between the servers in your farm according to availability and the load balancing algorithm you selected.</span></span>

<span data-ttu-id="f8004-251">ARR을 사용 하 여 분산을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 요청 라우팅 모듈이](https://go.microsoft.com/?linkid=9805130)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-251">For more information on how to configure load balancing with ARR, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

## <a name="monitor-the-server-farm"></a><span data-ttu-id="f8004-252">모니터 서버 팜</span><span class="sxs-lookup"><span data-stu-id="f8004-252">Monitor the Server Farm</span></span>

<span data-ttu-id="f8004-253">언제 든 지 IIS 관리자를 통해 컨트롤러 서버에서 서버 팜의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-253">You can monitor the health of your server farm at any time through IIS Manager on the controller server.</span></span> <span data-ttu-id="f8004-254">에 **연결** 창에 서버 팜의 확장 한 다음 클릭 **서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-254">In the **Connections** pane, expand your server farm, and then click **Servers**.</span></span> <span data-ttu-id="f8004-255">가운데 창에는 최근 활동의 추적 로그와 함께 팜의 각 서버의 요약이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-255">The center pane will show a summary of each server in the farm together with a trace log of recent activity.</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a><span data-ttu-id="f8004-256">결론</span><span class="sxs-lookup"><span data-stu-id="f8004-256">Conclusion</span></span>

<span data-ttu-id="f8004-257">WFF 서버 팜을 시작 및 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-257">Your WFF server farm should now be up and running.</span></span> <span data-ttu-id="f8004-258">원하는 어떤 배포 방법을 지원 하려면 주 서버를 구성할 수 있습니다&#x2014;세부 정보에 대 한 추가 정보 섹션을 참조 하세요&#x2014;되 고 구성 서버 팜의 각 보조 서버에서 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-258">You can configure the primary server to support whichever deployment approach you prefer&#x2014;see the Further Reading section for details&#x2014;and your configuration will be replicated on each secondary server in the server farm.</span></span>

## <a name="further-reading"></a><span data-ttu-id="f8004-259">추가 정보</span><span class="sxs-lookup"><span data-stu-id="f8004-259">Further Reading</span></span>

<span data-ttu-id="f8004-260">모든 측면을 구성 하 고는 WFF를 사용 하 여에 대 한 자세한 지침을 참조 하세요. 합니다 [IIS 7 용 Microsoft Web Farm Framework 2.0](https://go.microsoft.com/?linkid=9805129) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f8004-260">For more guidance on all aspects of configuring and using the WFF, see the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f8004-261">[이전](configuring-a-database-server-for-web-deploy-publishing.md)
> [다음](configuring-deployment-properties-for-a-target-environment.md)</span><span class="sxs-lookup"><span data-stu-id="f8004-261">[Previous](configuring-a-database-server-for-web-deploy-publishing.md)
[Next](configuring-deployment-properties-for-a-target-environment.md)</span></span>
