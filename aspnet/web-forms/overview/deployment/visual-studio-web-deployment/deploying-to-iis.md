---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트 환경에 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: d49dfad368ca4b81bb865103a99ec223a1cc66df
ms.sourcegitcommit: 184ba5b44d1c393076015510ac842b77bc9d4d93
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54396339"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a><span data-ttu-id="a7910-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 테스트 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="a7910-103">ASP.NET Web Deployment using Visual Studio: Deploying to Test</span></span>
====================
<span data-ttu-id="a7910-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a7910-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="a7910-105">이 자습서 시리즈에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 Visual Studio 2017을 사용 하 여 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-105">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider using Visual Studio 2017.</span></span> <span data-ttu-id="a7910-106">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-106">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="a7910-107">개요</span><span class="sxs-lookup"><span data-stu-id="a7910-107">Overview</span></span>

<span data-ttu-id="a7910-108">이 자습서에서는 로컬 컴퓨터에 인터넷 정보 서버 (IIS)에 ASP.NET 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-108">In this tutorial, you'll deploy an ASP.NET web application to Internet Information Server (IIS) on your local computer.</span></span>

<span data-ttu-id="a7910-109">일반적으로 응용 프로그램을 개발할 때 실행을 Visual Studio에서 테스트.</span><span class="sxs-lookup"><span data-stu-id="a7910-109">Generally when you develop an application, you run it and test it in Visual Studio.</span></span> <span data-ttu-id="a7910-110">Visual Studio 2017에서 웹 응용 프로그램 프로젝트 기본적으로 개발 웹 서버로 IIS Express를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-110">By default, web application projects in Visual Studio 2017 use IIS Express as the development web server.</span></span> <span data-ttu-id="a7910-111">IIS Express는 기본적으로 Visual Studio 2017에는 Visual Studio 개발 서버 (라고도: Cassini), 보다 전체 IIS 처럼 더 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-111">IIS Express behaves more like full IIS than the Visual Studio Development Server (also known as Cassini), which Visual Studio 2017 uses by default.</span></span> <span data-ttu-id="a7910-112">하지만 모두 개발 웹 서버 IIS 똑같이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-112">But neither development web server works exactly like IIS.</span></span> <span data-ttu-id="a7910-113">따라서 앱 수 실행 및 Visual Studio에서 정확 하 게 테스트 있지만 IIS에 배포 될 때 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-113">Consequently, an app could run and test correctly in Visual Studio but fail when it's deployed to IIS.</span></span>

<span data-ttu-id="a7910-114">두 가지 방법으로 응용 프로그램을 안정적으로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-114">You can reliably test your application in two ways:</span></span>

1. <span data-ttu-id="a7910-115">프로덕션 환경으로 배포 하려면 나중에 사용할 것과 동일한 프로세스를 사용 하 여 개발 컴퓨터에서 IIS에 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-115">Deploy your application to IIS on your development computer using the same process that you'll use later to deploy it to your production environment.</span></span>

   <span data-ttu-id="a7910-116">Visual Studio 웹 프로젝트를 실행할 때 배포 프로세스를 테스트 하지는 IIS를 사용 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-116">You can configure Visual Studio to use IIS when you run a web project, but that wouldn't test your deployment process.</span></span> <span data-ttu-id="a7910-117">이 메서드는 배포 프로세스를 확인 하 고 IIS에서 응용 프로그램이 올바르게 실행 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-117">This method validates your deployment process and that your application runs correctly under IIS.</span></span>

2. <span data-ttu-id="a7910-118">프로덕션 환경과 비슷한 테스트 환경에 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-118">Deploy your application to a test environment similar to your production environment.</span></span> 
 
   <span data-ttu-id="a7910-119">이 자습서에 대 한 프로덕션 환경은 Azure App Service에서 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-119">The production environment for these tutorials is Web Apps in Azure App Service.</span></span> <span data-ttu-id="a7910-120">이상적인 테스트 환경은 Azure 서비스에서 만든 추가 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-120">The ideal test environment is an additional web app created in the Azure Service.</span></span> <span data-ttu-id="a7910-121">프로덕션 웹 앱으로는 동일한 방식으로 설정할 수는, 있지만 테스트에 사용할 것 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-121">Though it would be set up the same way as a production web app, you would only use it for testing.</span></span>

<span data-ttu-id="a7910-122">옵션 2는 테스트에 대 한 가장 안정적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-122">Option 2 is the most reliable way to test.</span></span> <span data-ttu-id="a7910-123">옵션 2를 사용 하면 옵션 1을 사용 하 여 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-123">If you use option 2, you don't necessarily need to use option 1.</span></span> <span data-ttu-id="a7910-124">그러나 타사 배포 하는 경우 호스팅 공급자, 옵션 2 하지 못할 또는이 자습서 시리즈 방법을 모두 보여 줍니다. 하므로 비용이 많이 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-124">However if you're deploying to a third-party hosting provider, option 2 might not be feasible or might be expensive, so this tutorial series shows both methods.</span></span> <span data-ttu-id="a7910-125">옵션 2에 대 한 지침에 제공 되는 [프로덕션 환경에 배포](deploying-to-production.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-125">Guidance for option 2 is provided in the [Deploying to the Production Environment](deploying-to-production.md) tutorial.</span></span>

<span data-ttu-id="a7910-126">Visual Studio에서 웹 서버를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET 웹 프로젝트에 대 한 Visual Studio에서 웹 서버](https://msdn.microsoft.com/library/58wxa9w5.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-126">For more information about using web servers in Visual Studio, see [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>

<span data-ttu-id="a7910-127">미리 알림: 오류 메시지를 받거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-127">Reminder: If you receive an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="download-the-contoso-university-starter-project"></a><span data-ttu-id="a7910-128">Contoso University 시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="a7910-128">Download the Contoso University starter project</span></span>

<span data-ttu-id="a7910-129">다운로드 하 고 Contoso University Visual Studio 시작 솔루션 및 프로젝트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-129">Download and install the Contoso University Visual Studio starter solution and project.</span></span> <span data-ttu-id="a7910-130">이 솔루션은 완성된 된 자습서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-130">This solution contains the completed tutorial.</span></span> 

[<span data-ttu-id="a7910-131">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="a7910-131">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a><span data-ttu-id="a7910-132">IIS를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-132">Install IIS</span></span>

<span data-ttu-id="a7910-133">개발 컴퓨터에서 IIS에 배포, IIS 및 웹 배포 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-133">To deploy to IIS on your development computer, confirm that IIS and Web Deploy are installed.</span></span> <span data-ttu-id="a7910-134">기본적으로 Visual Studio 웹 배포 설치 되지만 IIS 기본 Windows 10, Windows 8 또는 Windows 7 구성에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-134">By default, Visual Studio installs Web Deploy, but IIS isn't included in the default Windows 10, Windows 8, or Windows 7 configuration.</span></span> <span data-ttu-id="a7910-135">IIS를 이미 설치한 경우 기본 응용 프로그램 풀.NET 4로 이미 설정 되어 건너뜁니다 [절로](#sqlexpress)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-135">If you've already installed IIS and the default application pool is already set to .NET 4, skip to [the next section](#sqlexpress).</span></span>

1. <span data-ttu-id="a7910-136">사용 하는 것이 좋습니다 합니다 [웹 플랫폼 설치 관리자 (WPI)](https://www.microsoft.com/web/downloads/platform.aspx) IIS 및 웹 배포를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-136">It's recommended you use the [Web Platform Installer (WPI)](https://www.microsoft.com/web/downloads/platform.aspx) to install IIS and Web Deploy.</span></span> <span data-ttu-id="a7910-137">WPI 필요한 경우 IIS 및 웹 배포 필수 구성 요소를 포함 하는 권장 되는 IIS 구성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-137">WPI installs a recommended IIS configuration that includes IIS and Web Deploy prerequisites if necessary.</span></span>

   <span data-ttu-id="a7910-138">IIS, 웹 배포 또는 관련 필수 구성 요소 중 하나를 설치한 경우 WPI 누락 된 것만 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-138">If you've already installed IIS, Web Deploy, or any of their required components, the WPI installs only what is missing.</span></span>

   * <span data-ttu-id="a7910-139">IIS 및 웹 배포를 설치 하려면 웹 플랫폼 설치 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-139">Use the Web Platform Installer to install IIS and Web Deploy:</span></span>
    
     ![WPI를 사용 하 여 IIS를 설치 합니다.](deploying-to-iis/_static/image30.png)

     ![WPI를 사용 하 여 웹 배포 설치](deploying-to-iis/_static/image31.png)

     <span data-ttu-id="a7910-142">IIS 7을 설치할지를 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-142">You'll see messages indicating that IIS 7 will be installed.</span></span> <span data-ttu-id="a7910-143">Windows 8;에서 IIS 8 사용할 수 있는 링크 하지만 Windows 8 이상에서는 ASP.NET 4.7이 설치 되어 있는지 확인 하려면 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-143">The link works for IIS 8 in Windows 8; but for Windows 8 and later, go through the following steps to make sure that ASP.NET 4.7 is installed:</span></span>

   * <span data-ttu-id="a7910-144">오픈 **Control Panel** > **프로그램** > **프로그램 및 기능** > **설정할 Windows 기능 사용 / 해제** .</span><span class="sxs-lookup"><span data-stu-id="a7910-144">Open **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off**.</span></span>

   * <span data-ttu-id="a7910-145">확장 **인터넷 정보 서비스**하십시오 **World Wide Web 서비스**, 및 **응용 프로그램 개발 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-145">Expand **Internet Information Services**, **World Wide Web Services**, and **Application Development Features**.</span></span>
   
   * <span data-ttu-id="a7910-146">확인 **ASP.NET 4.7** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-146">Confirm that **ASP.NET 4.7** is selected.</span></span>

     ![ASP.NET 4.7를 선택 합니다.](deploying-to-iis/_static/image1a.png)

   * <span data-ttu-id="a7910-148">확인 **World Wide Web 서비스** 하 고 **IIS 관리 콘솔** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-148">Confirm that **World Wide Web Services** and **IIS Management Console** is selected.</span></span> <span data-ttu-id="a7910-149">IIS 및 IIS 관리자가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-149">This installs IIS and IIS Manager.</span></span>
    
     ![World Wide Web 서비스를 선택 합니다.](deploying-to-iis/_static/image24.png)    
  
   * <span data-ttu-id="a7910-151">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-151">Select **OK**.</span></span> <span data-ttu-id="a7910-152">설치에 이루어지는 나타내는 대화 상자가 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-152">Dialog box messages indicating installation is taking place appear.</span></span>

<span data-ttu-id="a7910-153">IIS를 설치한 후 실행 **IIS 관리자** .NET Framework 버전 4에 기본 응용 프로그램 풀에 할당 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-153">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

1. <span data-ttu-id="a7910-154">WINDOWS + R 키를 눌러 엽니다는 **실행** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a7910-154">Press WINDOWS+R to open the **Run** dialog box.</span></span>

   <span data-ttu-id="a7910-155">(Windows 8 이상에서 "run"에 입력 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-155">(On Windows 8 or later, enter "run" on the **Start** page.</span></span> <span data-ttu-id="a7910-156">Windows 7에서 선택 **실행할** 에서 합니다 **시작** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="a7910-156">In Windows 7, select **Run** from the **Start** menu.</span></span> <span data-ttu-id="a7910-157">경우 **실행** 에 없는 **시작** 메뉴에서 작업 표시줄을 마우스 오른쪽 단추로 클릭을 선택 합니다 **속성**를 선택 합니다 **시작 메뉴** 탭 를선택합니다**사용자 지정**, 선택한 **명령을**.)</span><span class="sxs-lookup"><span data-stu-id="a7910-157">If **Run** isn't in the **Start** menu, right-click the taskbar, select **Properties**, select the **Start Menu** tab, select **Customize**, and select **Run command**.)</span></span>

2. <span data-ttu-id="a7910-158">"Inetmgr"을 입력 하 고 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-158">Enter "inetmgr" and select **OK**.</span></span>

3. <span data-ttu-id="a7910-159">에 **연결** 창에서 서버 노드를 확장 하 고 선택 **응용 프로그램 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-159">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="a7910-160">에 **응용 프로그램 풀** 창 경우 **DefaultAppPool** 는 다음 섹션으로 건너뛸.NET framework 버전 4 다음 그림과 같이 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-160">In the **Application Pools** pane if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

   ![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image5a.png)

4. <span data-ttu-id="a7910-162">두 개의 응용 프로그램 풀을 표시 하 고 모두.NET Framework 2.0으로 설정 됩니다, 경우 IIS에서 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-162">If you see only two application pools and both are set to .NET Framework 2.0, install ASP.NET 4 in IIS.</span></span>

   <span data-ttu-id="a7910-163">Windows 8 이상에 설치 되어 있도록 해당 ASP.NET 4.7에 대 한 이전 섹션의 지침을 참조 하세요. 또는 참조 [Windows 8 및 Windows Server 2012에 ASP.NET 4.5를 설치 하는 방법을](https://support.microsoft.com/kb/2736284)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-163">For Windows 8 or later, see the previous section's instructions for making sure that ASP.NET 4.7 is installed or see [How to install ASP.NET 4.5 on Windows 8 and Windows Server 2012](https://support.microsoft.com/kb/2736284).</span></span> <span data-ttu-id="a7910-164">Windows 7에 대 한 마우스 오른쪽 단추로 클릭 하 여 명령 프롬프트를 열고 **명령 프롬프트** 는 Windows에서 **시작** 메뉴에서 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-164">For Windows 7, open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="a7910-165">실행할 [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 다음 명령을 사용 하 여 IIS에서 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-165">Run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS using the following commands.</span></span> <span data-ttu-id="a7910-166">(32 비트 시스템에서 "프레임 워크"를 사용 하 여 "Framework64를"를 바꿉니다.)</span><span class="sxs-lookup"><span data-stu-id="a7910-166">(In 32-bit systems, replace "Framework64" with "Framework".)</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   <span data-ttu-id="a7910-167">이 명령은 새 응용 프로그램 풀.NET Framework 4에 대 한 하지만 기본 응용 프로그램 풀 남아 2.0로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-167">This command creates new application pools for the .NET Framework 4, but the default application pool will remain set to 2.0.</span></span> <span data-ttu-id="a7910-168">해당 응용 프로그램 풀에.NET 4를 대상.NET 4 응용 프로그램 풀을 변경 하므로 응용 프로그램을 배포 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-168">You're deploying an application that targets .NET 4 to that application pool, so change the application pool to .NET 4.</span></span>

5. <span data-ttu-id="a7910-169">닫았다면 **IIS 관리자**, 다시 실행, 해당 서버 노드를 확장 하 고 선택 **응용 프로그램 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-169">If you closed **IIS Manager**, run it again, expand the server node, and select **Application Pools**.</span></span>

6. <span data-ttu-id="a7910-170">에 **응용 프로그램 풀** 창 **DefaultAppPool**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-170">In the **Application Pools** pane, select **DefaultAppPool**.</span></span> <span data-ttu-id="a7910-171">에 **동작** 창 **기본 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-171">In the **Actions** pane, select **Basic Settings**.</span></span>

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. <span data-ttu-id="a7910-173">에 **응용 프로그램 풀 편집** 대화 상자에서 변경 합니다 **.NET CLR 버전** 에 **.NET CLR v4.0.30319**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-173">In the **Edit Application Pool** dialog box, change the **.NET CLR version** to **.NET CLR v4.0.30319**.</span></span> <span data-ttu-id="a7910-174">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-174">Select **OK**.</span></span>

   ![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

<span data-ttu-id="a7910-176">이제 IIS 웹 응용 프로그램을 게시할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-176">You're now ready to publish a web application to IIS.</span></span> <span data-ttu-id="a7910-177">그러나 먼저 테스트에 대 한 데이터베이스 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-177">First, however, create databases for testing.</span></span>

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a><span data-ttu-id="a7910-178">SQL Server Express 설치</span><span class="sxs-lookup"><span data-stu-id="a7910-178">Install SQL Server Express</span></span>

<span data-ttu-id="a7910-179">LocalDB는 테스트 환경에 SQL Server Express가 설치 되어 있어야 하므로 IIS에서 작동 하도록 설계 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-179">LocalDB isn't designed to work in IIS, so your test environment has to have SQL Server Express installed.</span></span> <span data-ttu-id="a7910-180">Visual Studio 2010 SQL Server Express를 사용 하는 경우 이미 기본적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-180">If you're using Visual Studio 2010 SQL Server Express, it's already installed by default.</span></span> <span data-ttu-id="a7910-181">Visual Studio 2012 이상 버전을 사용 하는 경우 SQL Server Express를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-181">If you're using Visual Studio 2012 or later, install SQL Server Express.</span></span>

<span data-ttu-id="a7910-182">SQL Server Express를 설치 하려면 다운로드 한 설치에서 [다운로드 센터: Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express).</span><span class="sxs-lookup"><span data-stu-id="a7910-182">To install SQL Server Express, download and install it from [Download Center: Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express).</span></span> 

<span data-ttu-id="a7910-183">SQL Server 설치 센터의 첫 번째 페이지에서 선택 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가** 기본 선택 항목을 수락 하는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-183">On the first page of the SQL Server Installation Center, select **New SQL Server stand-alone installation or add features to an existing installation** and follow the instructions accepting the default choices.</span></span> <span data-ttu-id="a7910-184">설치 마법사에서 기본 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-184">In the installation wizard, accept the default settings.</span></span> <span data-ttu-id="a7910-185">설치 옵션에 대 한 자세한 내용은 참조 하세요. [Install SQL Server 설치 마법사 (설치) from에서](https://msdn.microsoft.com/library/ms143219.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-185">For more information about installation options, see [Install SQL Server from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="create-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="a7910-186">테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a7910-186">Create SQL Server Express databases for the test environment</span></span>

<span data-ttu-id="a7910-187">Contoso University 응용 프로그램에는 두 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-187">The Contoso University application has two databases:</span></span> 

1. <span data-ttu-id="a7910-188">멤버 자격 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="a7910-188">Membership database</span></span> 
2. <span data-ttu-id="a7910-189">응용 프로그램 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="a7910-189">Application database</span></span> 

<span data-ttu-id="a7910-190">2 개의 개별 데이터베이스 또는 단일 데이터베이스에 이러한 데이터베이스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-190">You can deploy these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="a7910-191">쉽게 서로 데이터베이스 조인 하면 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-191">Combining them makes database joins between them easier.</span></span> 

<span data-ttu-id="a7910-192">타사 호스팅 공급자에 배포 하는 경우 호스팅 계획 수 또한를 통해 결합 하는 이유.</span><span class="sxs-lookup"><span data-stu-id="a7910-192">If you're deploying to a third-party hosting provider, your hosting plan might also give you a reason to combine them.</span></span> <span data-ttu-id="a7910-193">예를 들어 공급자는 여러 데이터베이스에 대 한 추가 요금을 청구할 수 또는 둘 이상의 데이터베이스도 허용 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-193">For example, the provider might charge more for multiple databases or might not even allow more than one database.</span></span>

<span data-ttu-id="a7910-194">이 자습서에서는 테스트 환경에서 두 개의 데이터베이스를 스테이징 및 프로덕션 환경에서 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-194">In this tutorial, you'll deploy to two databases in the test environment and to one database in the staging and production environments.</span></span>

<span data-ttu-id="a7910-195">**뷰** Visual Studio에서 메뉴 **서버 탐색기** (**데이터베이스 탐색기** Visual Web Developer에서).</span><span class="sxs-lookup"><span data-stu-id="a7910-195">From the **View** menu in Visual Studio, select **Server Explorer** (**Database Explorer** in Visual Web Developer).</span></span> <span data-ttu-id="a7910-196">마우스 오른쪽 단추로 클릭 **데이터 연결** 선택한 **새 SQL Server 데이터베이스 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-196">Right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

<span data-ttu-id="a7910-198">에 **새 SQL Server 데이터베이스 만들기** 대화 상자에 입력 합니다 ". \SQLExpress"에 **서버 이름** 상자와 "aspnet ContosoUniversity"에서 **새 데이터베이스 이름** 상자.</span><span class="sxs-lookup"><span data-stu-id="a7910-198">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-ContosoUniversity" in the **New database name** box.</span></span> <span data-ttu-id="a7910-199">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-199">Select **OK**.</span></span>

![Create aspnet-ContosoUniversity](deploying-to-iis/_static/image9.png)

<span data-ttu-id="a7910-201">라는 새 SQL Server Express School 데이터베이스를 만들려면 동일한 절차에 따라 `ContosoUniversity`합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-201">Follow the same procedure to create a new SQL Server Express School database named `ContosoUniversity`.</span></span>

<span data-ttu-id="a7910-202">**서버 탐색기** 두 새 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-202">**Server Explorer** shows the two new databases.</span></span>

![서버 탐색기에서 새 데이터베이스](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a><span data-ttu-id="a7910-204">새 데이터베이스에 대 한 권한 부여 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="a7910-204">Create a grant script for the new databases</span></span>

<span data-ttu-id="a7910-205">응용 프로그램 개발 컴퓨터에 IIS에서 실행 하는 경우 응용 프로그램 데이터베이스에 액세스할 기본 응용 프로그램 풀 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-205">When the application runs in IIS on your development computer, the application uses the default application pool's credentials to access the database.</span></span> <span data-ttu-id="a7910-206">그러나 기본적으로 응용 프로그램 풀의 데이터베이스를 열 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-206">However, by default, the application pool doesn't have permission to open the databases.</span></span> <span data-ttu-id="a7910-207">즉, 해당 권한을 부여 하는 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-207">This means you need to run a script to grant that permission.</span></span> <span data-ttu-id="a7910-208">이 섹션에서는 스크립트 만들고 IIS에서 실행 될 때 응용 프로그램에서 데이터베이스를 열 수 있도록 해야 하는 나중에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-208">In this section, you'll create that script and run it later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="a7910-209">텍스트 편집기에서 새 파일에 다음 SQL 명령을 복사 하 고으로 저장 *Grant.sql*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-209">In a text editor, copy the following SQL commands into a new file and save it as *Grant.sql*.</span></span> 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

<span data-ttu-id="a7910-210">Visual Studio에서 Contoso University 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-210">In Visual Studio, open the Contoso University solution.</span></span> <span data-ttu-id="a7910-211">(없습니다 프로젝트 중 하나), 솔루션을 마우스 오른쪽 단추로 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-211">Right-click the solution (not one of the projects), and select **Add**.</span></span> <span data-ttu-id="a7910-212">선택 **기존 항목**, 이동할 *Grant.sql*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-212">Select **Existing Item**, browse to *Grant.sql*, and open it.</span></span>

> [!NOTE]
> <span data-ttu-id="a7910-213">이 자습서에서는 지정 된 대로 SQL Server Express 2012를 사용 하 여 회사 이상 및 Windows 10, Windows 8 또는 Windows 7에서 IIS 설정을 사용 하 여이 스크립트는 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-213">This script is designed to work with SQL Server Express 2012 or later and with the IIS settings in Windows 10, Windows 8, or Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="a7910-214">다른 버전의 SQL Server 또는 Windows를 사용 하는 경우 또는 설정한 경우 IIS 컴퓨터에 다르게이 스크립트를 변경 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-214">If you're using a different version of SQL Server or Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="a7910-215">SQL Server 스크립트에 대 한 자세한 내용은 참조 하세요. [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-215">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> <span data-ttu-id="a7910-216">**보안 참고** 이 스크립트는 제공 `db_owner` 프로덕션 환경에 맞게 해야는 런타임 시 데이터베이스를 액세스 하는 사용자에 게 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="a7910-216">**Security Note** This script gives `db_owner` permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="a7910-217">일부 시나리오에서는 전체 데이터베이스 스키마 배포에 대 한 사용 권한을 업데이트 하 고 실행된 시간에 대 한 데이터 읽기 및 쓰기에 권한이 있는 다른 사용자 지정 된 사용자를 지정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-217">In some scenarios, you might want to specify a user that has full database schema update permissions only for deployment and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="a7910-218">자세한 내용은 [Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토](#reviewingmigrations) 이 자습서의 뒷부분에 나오는.</span><span class="sxs-lookup"><span data-stu-id="a7910-218">For more information, see [Reviewing the Automatic Web.config Changes for Code First Migrations](#reviewingmigrations) later in this tutorial.</span></span>

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a><span data-ttu-id="a7910-219">응용 프로그램 데이터베이스에서 권한 부여 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-219">Run the grant script in the application database</span></span>

<span data-ttu-id="a7910-220">데이터베이스 배포 사용 하기 때문에 멤버 자격 데이터베이스에서 권한 부여 스크립트를 배포 하는 동안 실행 하려면 게시 프로필을 구성할 수 있습니다 합니다 [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-220">You can configure the publish profile to run the grant script in the membership database during deployment because that database deployment uses the [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) provider.</span></span> <span data-ttu-id="a7910-221">응용 프로그램 데이터베이스를 배포 하는 Code First 마이그레이션을 배포 하는 동안 스크립트를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-221">You can't run scripts during Code First Migrations deployment, which is how you're deploying the application database.</span></span> <span data-ttu-id="a7910-222">즉, 수동으로 응용 프로그램 데이터베이스에 배포 하기 전에 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-222">This means you have to manually run the script before deployment in the application database.</span></span>

1. <span data-ttu-id="a7910-223">Visual Studio에서 엽니다는 *Grant.sql* 앞에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-223">In Visual Studio, open the *Grant.sql* file that you created earlier.</span></span>

2. <span data-ttu-id="a7910-224">선택 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-224">Select **Connect**.</span></span> 

    ![연결 단추](deploying-to-iis/_static/image11.png)

3. <span data-ttu-id="a7910-226">에 **서버에 연결** 대화 상자에 입력 합니다 *. \SQLExpress* 으로 **서버 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-226">In the **Connect to Server** dialog box, enter *.\SQLExpress* as the **Server Name**.</span></span> <span data-ttu-id="a7910-227">선택 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-227">Select **Connect**.</span></span>

4. <span data-ttu-id="a7910-228">데이터베이스 드롭다운 목록에서 선택 **ContosoUniversity**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-228">In the database drop-down list select **ContosoUniversity**.</span></span> <span data-ttu-id="a7910-229">선택 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-229">Select **Execute**.</span></span> 

   ![](deploying-to-iis/_static/image12.png)

<span data-ttu-id="a7910-230">기본 응용 프로그램 풀 id는 데이터베이스 테이블을 만드는 응용 프로그램을 실행 하는 경우 Code First 마이그레이션을 위해 응용 프로그램 데이터베이스에 충분 한 권한이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-230">The default application pool identity now has sufficient permissions in the application database for Code First Migrations to create the database tables when the application runs.</span></span>

## <a name="publish-to-iis"></a><span data-ttu-id="a7910-231">IIS에 게시</span><span class="sxs-lookup"><span data-stu-id="a7910-231">Publish to IIS</span></span>

<span data-ttu-id="a7910-232">여러 가지 방법으로 Visual Studio 및 웹 배포를 사용 하 여 IIS에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-232">There are several ways you can deploy to IIS using Visual Studio and Web Deploy:</span></span>

* <span data-ttu-id="a7910-233">One-click 게시 하는 Visual Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-233">Use Visual Studio one-click publish.</span></span>
* <span data-ttu-id="a7910-234">명령줄에서 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-234">Publish from the command line.</span></span>
* <span data-ttu-id="a7910-235">배포 패키지를 만들고 IIS 관리자를 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-235">Create a deployment package and install it using IIS Manager.</span></span> <span data-ttu-id="a7910-236">패키지에 있는 모든 파일 및 IIS에서 사이트를 설치 하는 데 필요한 메타 데이터를 사용 하 여.zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-236">The package has a .zip file with all the files and metadata required to install a site in IIS.</span></span>
* <span data-ttu-id="a7910-237">배포 패키지를 만들고 명령줄을 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-237">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="a7910-238">진행 하면서 자동화 하도록 Visual Studio를 설정 하려면 이전 자습서에서 이러한 모든 메서드를 적용 하는 배포 작업 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-238">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these methods.</span></span> <span data-ttu-id="a7910-239">이 자습서에서는 처음 두 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-239">In these tutorials, you'll use the first two methods.</span></span> <span data-ttu-id="a7910-240">배포 패키지 사용에 대 한 자세한 내용은 [웹 응용 프로그램 만들기 및 웹 배포 패키지를 설치 하 여 배포](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) 에서 Visual Studio 및 ASP.NET 웹 배포 콘텐츠 맵.</span><span class="sxs-lookup"><span data-stu-id="a7910-240">For information about using deployment packages, see [Deploying a web application by creating and installing a web deployment package](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

<span data-ttu-id="a7910-241">게시 하기 전에 Visual Studio 관리자 모드에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-241">Before publishing, make sure that you're running Visual Studio in administrator mode.</span></span> <span data-ttu-id="a7910-242">찾을 수 없으면 **(관리자)** 제목 표시줄에서 Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-242">If you don't see **(Administrator)** in the title bar, close Visual Studio.</span></span> <span data-ttu-id="a7910-243">Windows 8에서 (또는 이상) **시작** 페이지 또는 Windows 7 **시작** 메뉴에서 Visual Studio 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-243">In the Windows 8 (or later) **Start** page or the Windows 7 **Start** menu, right-click the Visual Studio icon and select **Run as Administrator**.</span></span> <span data-ttu-id="a7910-244">관리자 모드를 로컬 컴퓨터의 IIS에 게시할 경우 게시에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-244">Administrator mode is only required for publishing when you're publishing to IIS on the local computer.</span></span>

### <a name="create-the-publish-profile"></a><span data-ttu-id="a7910-245">게시 프로필을 만들려면</span><span class="sxs-lookup"><span data-stu-id="a7910-245">Create the publish profile</span></span>

1. <span data-ttu-id="a7910-246">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **ContosoUniversity** 프로젝트 (하지는 **ContosoUniversity.DAL** 프로젝트).</span><span class="sxs-lookup"><span data-stu-id="a7910-246">In **Solution Explorer**, right-click the **ContosoUniversity** project (not the **ContosoUniversity.DAL** project).</span></span> <span data-ttu-id="a7910-247">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-247">Select **Publish**.</span></span> <span data-ttu-id="a7910-248">합니다 **게시** 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-248">The **Publish** page appears.</span></span>

2. <span data-ttu-id="a7910-249">선택 **새 프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-249">Select **New Profile**.</span></span> <span data-ttu-id="a7910-250">합니다 **게시 대상 선택** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-250">The **Pick a publish target** dialog box appears.</span></span>

3. <span data-ttu-id="a7910-251">선택 **IIS, FTP 등**합니다. **프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-251">Select **IIS, FTP, etc**. Select **Create Profile**.</span></span> <span data-ttu-id="a7910-252">합니다 **게시** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-252">The **Publish** wizard appears.</span></span>

   ![게시 웹 마법사 프로필 탭](deploying-to-iis/_static/image26.png)

4. <span data-ttu-id="a7910-254">**메서드를 게시** 드롭 다운 메뉴에서 **웹 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-254">From the **Publish method** drop-down menu, select **Web Deploy**.</span></span>

5. <span data-ttu-id="a7910-255">에 대 한 **Server**를 입력 *localhost*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-255">For **Server**, enter *localhost*.</span></span>

6. <span data-ttu-id="a7910-256">에 대 한 **사이트 이름**를 입력 *기본 웹 사이트/ContosoUniversity*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-256">For **Site name**, enter *Default Web Site/ContosoUniversity*.</span></span>

7. <span data-ttu-id="a7910-257">에 대 한 **대상 URL**를 입력 *http://localhost/ContosoUniversity*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-257">For **Destination URL**, enter *http://localhost/ContosoUniversity*.</span></span>

   <span data-ttu-id="a7910-258">합니다 **대상 URL** 설정이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-258">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="a7910-259">Visual Studio 응용 프로그램 배포 완료 되 면 기본 브라우저가이 URL로 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-259">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="a7910-260">배포 후 자동으로 열려면 브라우저를 사용 하지 않으려는 경우에이 상자를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-260">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>

8. <span data-ttu-id="a7910-261">선택 **연결 유효성 검사** 설정이 올바른지 고 로컬 컴퓨터의 IIS에 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-261">Select **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

   <span data-ttu-id="a7910-262">녹색 확인 표시가 성공적으로 연결 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-262">A green check mark verifies that the connection is successful.</span></span>

   ![게시 웹 마법사 연결 탭](deploying-to-iis/_static/image27.png)

9. <span data-ttu-id="a7910-264">선택 **다음** 이동 합니다 **설정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-264">Select **Next** to advance to the **Settings** tab.</span></span>

10. <span data-ttu-id="a7910-265">합니다 **구성** 드롭다운 목록 상자에 배포 하도록 빌드 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-265">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="a7910-266">기본값은 그대로 **릴리스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-266">Leave it set to the default value of **Release**.</span></span> <span data-ttu-id="a7910-267">이 자습서의 디버그 빌드 배포 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-267">You won't be deploying Debug builds in this tutorial.</span></span>

11. <span data-ttu-id="a7910-268">확장 **파일 게시 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-268">Expand **File Publish Options**.</span></span> <span data-ttu-id="a7910-269">선택 **앱에서 파일 제외\_데이터 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-269">Select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="a7910-270">응용 프로그램을 테스트 환경에서 로컬 SQL Server Express 인스턴스에서.mdf 파일에서 만든 데이터베이스에 액세스 합니다 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-270">In the test environment, the application accesses the databases that you created in the local SQL Server Express instance, not the .mdf files in the *App\_Data* folder.</span></span>

12. <span data-ttu-id="a7910-271">유지 합니다 **게시 중 미리 컴파일** 하 고 **대상에서 추가 파일 제거** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-271">Leave the **Precompile during publishing** and **Remove additional files at destination** check boxes cleared.</span></span>

    ![설정 탭에서 파일 게시 옵션](deploying-to-iis/_static/image15a.png)

    <span data-ttu-id="a7910-273">미리 컴파일 주로 대규모 사이트에 대 한 유용한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-273">Precompiling is an option that is useful mainly for large sites.</span></span> <span data-ttu-id="a7910-274">시작 시간 페이지 요청에 사이트를 게시 한 후 처음으로 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-274">It can reduce startup time the first time a page is requested after the site is published.</span></span>

    <span data-ttu-id="a7910-275">이 첫 번째 배포 후 없습니다 모든 파일이 대상 폴더에 아직 추가 파일을 제거할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-275">You don't need to remove additional files since this is your first deployment and there won't be any files in the destination folder yet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7910-276">선택 하는 경우 **대상에서 추가 파일 제거** 동일한 사이트에는 후속 배포에 대 한 확인 표시를 배포 하기 전에 파일이 삭제 됩니다 미리 되도록 미리 보기 기능을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-276">If you select **Remove additional files at destination** for a subsequent deployment to the same site, make sure that you use the preview feature so that you see in advance which files will be deleted before you deploy.</span></span> <span data-ttu-id="a7910-277">예상 되는 동작은 웹 배포 프로젝트에서 삭제 된 대상 서버에서 파일 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-277">The expected behavior is that Web Deploy will delete files on the destination server that you have deleted in your project.</span></span> <span data-ttu-id="a7910-278">그러나 원본 및 대상 폴더 아래에 전체 폴더 구조 비교 됩니다. 일부 시나리오에서는 웹 배포 실수로 삭제를 삭제 하지 않으려는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-278">However, the entire folder structure under the source and destination folders is compared; and in some scenarios, Web Deploy might delete files you don't want to delete.</span></span>
    > 
    > <span data-ttu-id="a7910-279">예를 들어 하위 폴더를 삭제할 경우 웹 응용 프로그램 서버의 하위 폴더에 루트 폴더에 프로젝트를 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a7910-279">For example if you have a web application in a subfolder on the server when you deploy a project to the root folder, the subfolder will be deleted.</span></span> <span data-ttu-id="a7910-280">Contoso.com에서 기본 사이트에 대 한 하나의 프로젝트와 다른 프로젝트 contoso.com/blog의 블로그에 대 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-280">You might have one project for the main site at contoso.com and another project for a blog at contoso.com/blog.</span></span> <span data-ttu-id="a7910-281">블로그 응용 프로그램은 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-281">The blog application is in a subfolder.</span></span> <span data-ttu-id="a7910-282">선택 하는 경우 **대상에서 추가 파일 제거** 블로그 응용 프로그램 주 사이트를 배포할 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-282">If you select **Remove additional files at destination** when you deploy the main site, the blog application will be deleted.</span></span>
    > 
    > <span data-ttu-id="a7910-283">또 다른 예로, 앱에 대 한\_데이터 폴더 예기치 않게 삭제 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-283">For another example, your App\_Data folder might get deleted unexpectedly.</span></span> <span data-ttu-id="a7910-284">앱에서 데이터베이스 파일을 저장 하는 SQL Server Compact와 같은 특정 데이터베이스\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="a7910-284">Certain databases such as SQL Server Compact store database files in the App\_Data folder.</span></span> <span data-ttu-id="a7910-285">초기 배포 후 사용자가 선택할 수 있도록 이후 배포에서 데이터베이스 파일을 복사 유지 않으려는 **제외 앱\_데이터** 웹 패키지 및 게시 탭 합니다. 있는 경우 작업을 수행한 후 **대상에서 추가 파일 제거** 선택 하면 데이터베이스 파일 및 앱\_게시할 때마다 데이터 폴더 자체가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-285">After the initial deployment, you don't want to keep copying the database files in subsequent deployments, so you select  **Exclude App\_Data** on the Package/Publish Web tab. After you do that if you have **Remove additional files at destination** selected, your database files and the App\_Data folder itself will be deleted the next time you publish.</span></span>

### <a name="configure-deployment-for-the-membership-database"></a><span data-ttu-id="a7910-286">멤버 자격 데이터베이스에 대 한 배포 구성</span><span class="sxs-lookup"><span data-stu-id="a7910-286">Configure deployment for the membership database</span></span>

<span data-ttu-id="a7910-287">다음 단계를 적용 합니다 **DefaultConnection** 대화 상자에서 데이터베이스 **데이터베이스** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-287">The following steps apply to the **DefaultConnection** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="a7910-288">에 **원격 연결 문자열** 상자에 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-288">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express membership database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   <span data-ttu-id="a7910-289">배포 프로세스 때문에 배포 된 Web.config 파일에이 연결 문자열을 넣습니다 **런타임에이 연결 문자열을 사용 하 여** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-289">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="a7910-290">연결 문자열을 가져올 수도 있습니다 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-290">You can also get the connection string from **Server Explorer**.</span></span> <span data-ttu-id="a7910-291">**서버 탐색기**를 확장 하 고 **데이터 연결** 선택 합니다  **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** 데이터베이스에서 다음를 **속성** 창 복사 합니다 **연결 문자열** 값.</span><span class="sxs-lookup"><span data-stu-id="a7910-291">In **Server Explorer**, expand **Data Connections** and select the **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** database, then from the **Properties** window copy the **Connection String** value.</span></span> <span data-ttu-id="a7910-292">연결 문자열 삭제할 수 있는 하나의 추가 설정 되어: `Pooling=False`합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-292">That connection string will have one additional setting that you can delete: `Pooling=False`.</span></span>

2. <span data-ttu-id="a7910-293">선택 **데이터베이스 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-293">Select **Update database**.</span></span>

   <span data-ttu-id="a7910-294">이렇게 하면 데이터베이스 스키마를 배포 하는 동안 대상 데이터베이스에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-294">This causes the database schema to be created in the destination database during deployment.</span></span> <span data-ttu-id="a7910-295">다음 단계를 실행 해야 하는 추가 스크립트를 지정 합니다: 기본 응용 프로그램 풀 및 데이터를 배포 하는 것에 대 한 데이터베이스 액세스 권한을 부여 하려면 하나.</span><span class="sxs-lookup"><span data-stu-id="a7910-295">In next steps, you specify the additional scripts that you need to run: one to grant database access to the default application pool and one to deploy data.</span></span>

3. <span data-ttu-id="a7910-296">선택 **데이터베이스 업데이트 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-296">Select **Configure database updates**.</span></span>
 
4. <span data-ttu-id="a7910-297">에 **데이터베이스 업데이트 구성** 대화 상자에서 **SQL 스크립트 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-297">In the **Configure Database Updates** dialog box, select **Add SQL Script**.</span></span> <span data-ttu-id="a7910-298">로 이동 합니다 *Grant.sql* 솔루션 폴더에서 이전에 저장 하는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-298">Navigate to the *Grant.sql* script that you saved earlier in the solution folder.</span></span>

5. <span data-ttu-id="a7910-299">추가 하는 프로세스를 반복 합니다 *aspnet-데이터-dev.sql* 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-299">Repeat the process to add the *aspnet-data-dev.sql* script.</span></span>

   ![멤버 자격 데이터베이스에 대 한 데이터베이스 업데이트 구성](deploying-to-iis/_static/image16.png)

6. <span data-ttu-id="a7910-301">선택 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-301">Select **Close**.</span></span>

### <a name="configure-deployment-for-the-application-database"></a><span data-ttu-id="a7910-302">응용 프로그램 데이터베이스에 대 한 배포 구성</span><span class="sxs-lookup"><span data-stu-id="a7910-302">Configure deployment for the application database</span></span>

<span data-ttu-id="a7910-303">Visual Studio는 Entity Framework를 감지 하는 경우 `DbContext` 클래스의 항목을 만듭니다 합니다 **데이터베이스** 포함 된 섹션에는 **Execute Code First Migrations** 대신 확인란은  **데이터베이스 업데이트** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-303">When Visual Studio detects an Entity Framework `DbContext` class, it creates an entry in the **Databases** section that has an **Execute Code First Migrations** check box instead of an **Update Database** check box.</span></span> <span data-ttu-id="a7910-304">이 자습서에서는 Code First 마이그레이션을 배포를 지정 하려면 해당 확인란을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-304">For this tutorial, you'll use that check box to specify Code First Migrations deployment.</span></span>

<span data-ttu-id="a7910-305">일부 시나리오에서는 사용할 수는 `DbContext` 수 있지만 데이터베이스 마이그레이션 대신 dbDacFx 공급자를 사용 하 여 데이터베이스를 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-305">In some scenarios, you might be using a `DbContext` database but you want to use the dbDacFx provider instead of Migrations to deploy the database.</span></span> <span data-ttu-id="a7910-306">이 경우 참조 [Code First 마이그레이션 없이 데이터베이스를 배포 하려면 어떻게 하나요?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) MSDN에서 ASP.NET 웹 배포 faq에서.</span><span class="sxs-lookup"><span data-stu-id="a7910-306">In that case, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the ASP.NET Web Deployment FAQ on MSDN.</span></span>

<span data-ttu-id="a7910-307">다음 단계를 적용 합니다 **SchoolContext** 대화 상자에서 데이터베이스 **데이터베이스** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-307">The following steps apply to the **SchoolContext** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="a7910-308">에 **원격 연결 문자열** 상자에 새 SQL Server Express 응용 프로그램 데이터베이스를 가리키는 다음 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-308">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express application database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   <span data-ttu-id="a7910-309">배포 프로세스 때문에 배포 된 Web.config 파일에이 연결 문자열을 넣습니다 **런타임에이 연결 문자열을 사용 하 여** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-309">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

   <span data-ttu-id="a7910-310">응용 프로그램 데이터베이스 연결 문자열을 가져올 수도 있습니다 **서버 탐색기** 멤버 자격 데이터베이스 연결 문자열을 동일한 방식으로 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-310">You can also get the application database connection string from **Server Explorer** in the same way you got the membership database connection string.</span></span>

2. <span data-ttu-id="a7910-311">선택 **Execute Code First Migrations (응용 프로그램 시작 시 실행)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-311">Select **Execute Code First Migrations (runs on application start)**.</span></span>

   <span data-ttu-id="a7910-312">이 옵션을 지정 하려면 배포 된 Web.config 파일을 구성 하는 배포 프로세스 사용 하면는 `MigrateDatabaseToLatestVersion` 이니셜라이저입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-312">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="a7910-313">자동으로이 이니셜라이저 응용 프로그램 배포 후 처음으로 데이터베이스에 액세스 하는 경우 데이터베이스를 최신 버전에 게 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-313">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

### <a name="configure-publish-profile-transforms"></a><span data-ttu-id="a7910-314">구성 프로필 변환 게시</span><span class="sxs-lookup"><span data-stu-id="a7910-314">Configure publish profile transforms</span></span>

1. <span data-ttu-id="a7910-315">선택 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-315">Select **Close**.</span></span> <span data-ttu-id="a7910-316">선택 **예** 변경 내용을 저장 하려는 경우 묻는 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a7910-316">Select **Yes** when you are asked if you want to save changes.</span></span>

2. <span data-ttu-id="a7910-317">**솔루션 탐색기**, 확장 **속성**를 확장 하 고 **PublishProfiles**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-317">In **Solution Explorer**, expand **Properties**, expand **PublishProfiles**.</span></span>

3. <span data-ttu-id="a7910-318">마우스 오른쪽 단추로 클릭 *CustomProfile.pubxml* 하 고 이름을 *Test.pubxml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-318">Right-click *CustomProfile.pubxml* and rename it *Test.pubxml*.</span></span>

4. <span data-ttu-id="a7910-319">마우스 오른쪽 단추로 클릭 *Test.pubxml*합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-319">Right-click *Test.pubxml*.</span></span> <span data-ttu-id="a7910-320">선택 **Config 변환 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-320">Select **Add Config Transform**.</span></span>

   ![Config 변환 메뉴 추가](deploying-to-iis/_static/image17.png)

   <span data-ttu-id="a7910-322">Visual Studio 만듭니다는 *Web.Test.config* 변환 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-322">Visual Studio creates the *Web.Test.config* transform file and opens it.</span></span>

5. <span data-ttu-id="a7910-323">에 *Web.Test.config* 변환 파일에서 바로 뒤에 다음 코드를 삽입 구성 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-323">In the *Web.Test.config* transform file, insert the following code immediately after the opening configuration tag.</span></span>

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    <span data-ttu-id="a7910-324">테스트를 사용 하는 경우 게시 프로필,이 변환은 환경 표시기 "Test"를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-324">When you use the Test publish profile, this transform sets the environment indicator to "Test".</span></span> <span data-ttu-id="a7910-325">배포 된 사이트에서 "Contoso University" H1 제목을 후 "(테스트)"에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-325">In the deployed site, you'll see "(Test)" after the "Contoso University" H1 heading.</span></span>

6. <span data-ttu-id="a7910-326">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-326">Save and close the file.</span></span>

7. <span data-ttu-id="a7910-327">마우스 오른쪽 단추로 클릭 합니다 *Web.Test.config* 파일을 선택 **미리 보기 변환** 변환을 코딩 예상된 변경 내용이 생성 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-327">Right-click the *Web.Test.config* file and select **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="a7910-328">**Web.config 미리 보기** 창 모두에 적용 한 결과 표시 합니다 *Web.Release.config* 변환 및 *Web.Test.config* 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-328">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Test.config* transforms.</span></span>

### <a name="preview-the-deployment-updates"></a><span data-ttu-id="a7910-329">배포 업데이트를 미리 보기</span><span class="sxs-lookup"><span data-stu-id="a7910-329">Preview the deployment updates</span></span>

1. <span data-ttu-id="a7910-330">엽니다는 **웹 게시** 마법사를 다시 (ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **게시**, 한 다음 **미리 보기**).</span><span class="sxs-lookup"><span data-stu-id="a7910-330">Open the **Publish Web** wizard again (right-click the ContosoUniversity project, select **Publish**, then **Preview**).</span></span>

2. <span data-ttu-id="a7910-331">에 **미리 보기** 대화 상자에서 **미리 보기 시작** 복사 될 파일의 목록을 보려면.</span><span class="sxs-lookup"><span data-stu-id="a7910-331">In the **Preview** dialog box, select **Start Preview** to see a list of the files that will be copied.</span></span> 

   ![게시 미리 보기](deploying-to-iis/_static/image29.png)

   <span data-ttu-id="a7910-333">선택할 수도 있습니다는 **미리 보기 데이터베이스** 멤버 자격 데이터베이스에서 실행 될 스크립트를 보려면이 링크를 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-333">You can also select the **Preview database** link to see the scripts that will run in the membership database.</span></span> <span data-ttu-id="a7910-334">(스크립트가 실행 됩니다 Code First 마이그레이션을 배포에 대 한 응용 프로그램 데이터베이스에 대 한 미리 보기에 항목이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="a7910-334">(No scripts are run for Code First Migrations deployment, so there's nothing to preview for the application database.)</span></span>

3. <span data-ttu-id="a7910-335">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-335">Select **Publish**.</span></span>

   <span data-ttu-id="a7910-336">Visual Studio 관리자 모드에 없는 경우 사용 권한 오류 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-336">If Visual Studio is not in administrator mode, you might get a permissions error message.</span></span> <span data-ttu-id="a7910-337">이 경우 Visual Studio를 닫습니다, 그리고 관리자 모드에서 엽니다 및 다시 게시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-337">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

   <span data-ttu-id="a7910-338">Visual Studio 관리자 모드에 있으면 합니다 **출력** 창 보고서를 성공적으로 빌드 및 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-338">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   <span data-ttu-id="a7910-340">URL을 입력 한 경우는 **대상 URL** 상자에서 게시 프로필 **연결** 탭 브라우저 IIS 컴퓨터에서 실행 되는 Contoso University 홈 페이지에 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-340">If you entered the URL in the **Destination URL** box on the publish profile **Connection** tab, the browser automatically opens to the Contoso University Home page running in IIS on your computer.</span></span>

## <a name="test-in-the-test-environment"></a><span data-ttu-id="a7910-341">테스트 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="a7910-341">Test in the test environment</span></span>

<span data-ttu-id="a7910-342">환경 표시기 표시 "(테스트)" 대신 "(개발),"는 것을 보여 줍니다 합니다 *Web.config* 환경 표시기에 대 한 변환의 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-342">Notice that the environment indicator shows "(Test)" instead of "(Dev)," which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="a7910-343">실행 합니다 **강사** 페이지는 Code First 시드 강사 데이터를 사용 하 여 데이터베이스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-343">Run the **Instructors** page to verify that Code First seeded the database with instructor data.</span></span> <span data-ttu-id="a7910-344">이 페이지를 선택 하면 Code First는 데이터베이스를 만듭니다 및 다음을 실행 하기 때문에 로드 하려면 몇 분 정도 걸릴 수 있습니다는 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a7910-344">When you select this page, it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="a7910-345">(수행 되지 않은 것을 응용 프로그램 데이터베이스에 아직 액세스 하지 않은 시도 하기 때문에 홈 페이지에서 했을 때.)</span><span class="sxs-lookup"><span data-stu-id="a7910-345">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="a7910-346">선택 된 **학생** 배포 된 데이터베이스에 학생이 없는 있는지 확인 하는 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-346">Select the **Students** tab to verify that the deployed database has no students.</span></span>

<span data-ttu-id="a7910-347">선택 **추가 학생** 에서 합니다 **학생** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="a7910-347">Select **Add Students** from the **Students** menu.</span></span> <span data-ttu-id="a7910-348">학생을 추가 하 고 다음에 새 학생을 확인 합니다 **학생** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a7910-348">Add a student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="a7910-349">이 데이터베이스에 작성 했습니다. 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-349">This verifies that you can successfully write to the database.</span></span>

<span data-ttu-id="a7910-350">**과정** 메뉴에서 **업데이트 크레딧**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-350">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="a7910-351">합니다 **업데이트 크레딧** 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-351">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="a7910-352">이전 버전 ("admin" 및 "devpwd") 만든 관리자 계정 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-352">Enter the administrator account credentials that you created earlier ("admin" and "devpwd").</span></span> <span data-ttu-id="a7910-353">합니다 **업데이트 크레딧** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-353">The **Update Credits** page is displayed.</span></span> <span data-ttu-id="a7910-354">이전 자습서에서 만든 관리자 계정을 테스트 환경에 배포한 올바르게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-354">This verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="a7910-355">확인을 *ELMAH* 폴더에 있습니다는 *c:\inetpub\wwwroot\ContosoUniversity* 자리 표시자 파일을 사용 하 여 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-355">Verify that an *ELMAH* folder exists in the *c:\inetpub\wwwroot\ContosoUniversity* folder with only the placeholder file in it.</span></span>

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="a7910-356">Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토</span><span class="sxs-lookup"><span data-stu-id="a7910-356">Review the automatic Web.config changes for Code First Migrations</span></span>

<span data-ttu-id="a7910-357">엽니다는 *Web.config* 배포 된 응용 프로그램에서 파일 *C:\inetpub\wwwroot\ContosoUniversity* 여기서 배포 프로세스를 구성 하도록 Code First 마이그레이션을 자동으로 확인할 수 있습니다 최신 버전으로 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-357">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deploying-to-iis/_static/image21.png)

<span data-ttu-id="a7910-358">배포 프로세스는 데이터베이스 스키마 업데이트에 대 한 단독으로 사용 하도록 Code First 마이그레이션에 대 한 새 연결 문자열도 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-358">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![Database_Publish 연결 문자열](deploying-to-iis/_static/image22.png)

<span data-ttu-id="a7910-360">이 추가 연결 문자열을 사용 하면 데이터베이스 스키마 업데이트에 대 한 하나의 사용자 계정 및 응용 프로그램 데이터 액세스에 대 한 다른 사용자 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-360">This additional connection string enables you to specify one user account for database schema updates and a different user account for application data access.</span></span> <span data-ttu-id="a7910-361">예를 들어, 할당할 수 있습니다 합니다 **db\_소유자** Code First 마이그레이션을 역할 및 **db\_datareader** 사용 하 여 **db\_datawriter**응용 프로그램 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-361">For example, you could assign the **db\_owner** role to Code First Migrations and **db\_datareader** with **db\_datawriter** roles to the application.</span></span> <span data-ttu-id="a7910-362">데이터베이스 스키마 변경에서 응용 프로그램의 잠재적 악성 코드 방지 하는 일반적인 심층 방어 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-362">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="a7910-363">(예를 들어이 발생할 수 있습니다 SQL 주입 공격에.) 이 자습서는이 패턴을 사용 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a7910-363">(For example, this might happen in a successful SQL injection attack.) These tutorials don't use this pattern.</span></span> <span data-ttu-id="a7910-364">시나리오에서이 패턴을 구현 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-364">To implement this pattern in your scenario, take these steps:</span></span>

1. <span data-ttu-id="a7910-365">에 **웹 게시** 에서 마법사를 **설정** 탭에서 전체 데이터베이스 스키마 업데이트 권한이 있는 사용자를 지정 하는 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-365">In the **Publish Web** wizard under the **Settings** tab, enter the connection string that specifies a user with full database schema update permissions.</span></span> <span data-ttu-id="a7910-366">선택을 취소 합니다 **런타임에이 연결 문자열을 사용 하 여** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-366">Clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="a7910-367">이것이 배포 된 Web.config 파일에는 `DatabasePublish` 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-367">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>

2. <span data-ttu-id="a7910-368">응용 프로그램에서 런타임 시 사용 하는 연결 문자열에 대 한 Web.config 파일 변환을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-368">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

## <a name="summary"></a><span data-ttu-id="a7910-369">요약</span><span class="sxs-lookup"><span data-stu-id="a7910-369">Summary</span></span>

<span data-ttu-id="a7910-370">이제 개발 컴퓨터에서 IIS에 응용 프로그램을 배포 하 고 있는 테스트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-370">You've now deployed your application to IIS on your development computer and tested it there.</span></span>

![테스트의 홈페이지](deploying-to-iis/_static/image23.png)

<span data-ttu-id="a7910-372">배포 프로세스 (배포 되지 않은 하려는 파일 제외) 올바른 위치에 응용 프로그램의 콘텐츠를 복사 하 고 또한 웹 배포는 IIS 구성 올바르게 배포 하는 동안 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-372">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy) and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="a7910-373">다음 자습서에서는 아직 수행 하지 않은 배포 작업을 발견 하는 하나 이상의 테스트 실행:에 대해 폴더 사용 권한을 설정 합니다 *Elm ah* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-373">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elm ah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="a7910-374">추가 정보</span><span class="sxs-lookup"><span data-stu-id="a7910-374">More information</span></span>

<span data-ttu-id="a7910-375">Visual Studio에서 IIS 또는 IIS Express를 실행 하는 방법에 대 한 내용은 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-375">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="a7910-376">[IIS Express 개요](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 사이트의.</span><span class="sxs-lookup"><span data-stu-id="a7910-376">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="a7910-377">[IIS Express 소개](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-377">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="a7910-378">[ASP.NET 웹 프로젝트에 대 한 Visual Studio에서 서버를 웹](https://msdn.microsoft.com/library/58wxa9w5.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-378">[Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>
- <span data-ttu-id="a7910-379">[코어 IIS 간의 차이점 및 ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 사이트의.</span><span class="sxs-lookup"><span data-stu-id="a7910-379">[Core Differences Between IIS and the ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>

<span data-ttu-id="a7910-380">어떤 문제에 대 한 정보는 보통 신뢰 수준에서 응용 프로그램을 실행 하는 경우에 발생할 수, 참조 [보통 신뢰에서 ASP.NET 응용 프로그램 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) Rolla 사이트에서 4 명의 Guys에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7910-380">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the four Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a7910-381">[이전](project-properties.md)
> [다음](setting-folder-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="a7910-381">[Previous](project-properties.md)
[Next](setting-folder-permissions.md)</span></span>
