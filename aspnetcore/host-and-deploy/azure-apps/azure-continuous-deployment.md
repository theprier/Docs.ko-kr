---
title: "Visual Studio 및 Git을 사용하여 Azure에 연속 배포"
author: rick-anderson
description: "Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다."
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: host-and-deploy/azure-apps/azure-continuous-deployment
ms.openlocfilehash: c1d25b109bbf211eb476860ff77b649565960b62
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="continuous-deployment-to-azure-for-aspnet-core-with-visual-studio-and-git"></a><span data-ttu-id="be15d-103">Visual Studio 및 Git에 ASP.NET Core에 대 한 Azure로 지속적인 배포</span><span class="sxs-lookup"><span data-stu-id="be15d-103">Continuous deployment to Azure for ASP.NET Core with Visual Studio and Git</span></span>

<span data-ttu-id="be15d-104">작성자: [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="be15d-104">By [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="be15d-105">이 자습서 연속 배포를 사용 하 여 Visual Studio를 사용 하 여 ASP.NET Core 웹 앱을 만들고 Visual Studio에서 Azure 앱 서비스에 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-105">This tutorial shows how to create an ASP.NET Core web app using Visual Studio and deploy it from Visual Studio to Azure App Service using continuous deployment.</span></span>

<span data-ttu-id="be15d-106">또한 [연속 배포를 사용하여 Azure Web App을 빌드하고 게시하기 위해 VSTS 사용](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)을 참조하세요. 여기서는 Visual Studio Team Services를 사용하여 [Azure App Service](/azure/app-service/app-service-web-overview)에 대한 CD(지속적인 업데이트) 워크플로를 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-106">See also [Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic), which shows how to configure a continuous delivery (CD) workflow for [Azure App Service](/azure/app-service/app-service-web-overview) using Visual Studio Team Services.</span></span> <span data-ttu-id="be15d-107">Team Services에서 azure 지속적인 업데이트 Azure 앱 서비스에서 호스트 되는 앱에 대 한 업데이트를 게시 하는 강력한 배포 파이프라인 설정을 간단 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-107">Azure Continuous Delivery in Team Services simplifies setting up a robust deployment pipeline to publish updates for apps hosted in Azure App Service.</span></span> <span data-ttu-id="be15d-108">파이프라인을 빌드, 테스트 실행, 스테이징 슬롯에 배포 및 다음 프로덕션에 배포 하기 위해 Azure 포털에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-108">The pipeline can be configured from the Azure portal to build, run tests, deploy to a staging slot, and then deploy to production.</span></span>

> [!NOTE]
> <span data-ttu-id="be15d-109">이 자습서를 완료 하려면 Microsoft Azure 계정은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-109">To complete this tutorial, a Microsoft Azure account is required.</span></span> <span data-ttu-id="be15d-110">계정을 가져오려면 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F) 또는 [무료 평가판에 등록](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-110">To obtain an account, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be15d-111">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="be15d-111">Prerequisites</span></span>

<span data-ttu-id="be15d-112">이 자습서에서는 다음 소프트웨어가 설치 되어 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-112">This tutorial assumes the following software is installed:</span></span>

* [<span data-ttu-id="be15d-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="be15d-113">Visual Studio</span></span>](https://www.visualstudio.com)
* <span data-ttu-id="be15d-114">[.NET core SDK](https://www.microsoft.com/net/download/core) (런타임 및 도구가)</span><span class="sxs-lookup"><span data-stu-id="be15d-114">[.NET Core SDK](https://www.microsoft.com/net/download/core) (runtime and tooling)</span></span>
* <span data-ttu-id="be15d-115">Windows용 [Git](https://git-scm.com/downloads)</span><span class="sxs-lookup"><span data-stu-id="be15d-115">[Git](https://git-scm.com/downloads) for Windows</span></span>

## <a name="create-an-aspnet-core-web-app"></a><span data-ttu-id="be15d-116">ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="be15d-116">Create an ASP.NET Core web app</span></span>

1. <span data-ttu-id="be15d-117">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-117">Start Visual Studio.</span></span>

1. <span data-ttu-id="be15d-118">**파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-118">From the **File** menu, select **New** > **Project**.</span></span>

1. <span data-ttu-id="be15d-119">**ASP.NET Core 웹 응용 프로그램** 프로젝트 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-119">Select the **ASP.NET Core Web Application** project template.</span></span> <span data-ttu-id="be15d-120">**설치됨** > **템플릿** > **Visual C#** > **.NET Core** 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-120">It appears under **Installed** > **Templates** > **Visual C#** > **.NET Core**.</span></span> <span data-ttu-id="be15d-121">프로젝트 이름을 `SampleWebAppDemo`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-121">Name the project `SampleWebAppDemo`.</span></span> <span data-ttu-id="be15d-122">**새 Git 리포지토리 만들기** 옵션을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-122">Select the **Create new Git respository** option and click **OK**.</span></span>

   ![새 프로젝트 대화 상자](azure-continuous-deployment/_static/01-new-project.png)

1. <span data-ttu-id="be15d-124">**새 ASP.NET Core 프로젝트** 대화 상자에서 ASP.NET Core **빈** 템플릿을 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-124">In the **New ASP.NET Core Project** dialog, select the ASP.NET Core **Empty** template, then click **OK**.</span></span>

   ![새 ASP.NET 프로젝트 대화 상자](azure-continuous-deployment/_static/02-web-site-template.png)

> [!NOTE]
> <span data-ttu-id="be15d-126">.NET Core의 최신 버전은 2.0입니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-126">The most recent release of .NET Core is 2.0.</span></span>

### <a name="running-the-web-app-locally"></a><span data-ttu-id="be15d-127">로컬로 웹앱 실행</span><span class="sxs-lookup"><span data-stu-id="be15d-127">Running the web app locally</span></span>

1. <span data-ttu-id="be15d-128">Visual Studio에서 앱 만들기를 완료하면 **디버그** > **디버깅 시작**을 선택하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-128">Once Visual Studio finishes creating the app, run the app by selecting **Debug** > **Start Debugging**.</span></span> <span data-ttu-id="be15d-129">눌러 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-129">As an alternative, press **F5**.</span></span>

   <span data-ttu-id="be15d-130">Visual Studio 및 새 앱을 초기화하는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-130">It may take time to initialize Visual Studio and the new app.</span></span> <span data-ttu-id="be15d-131">완료 되 면 브라우저에서 실행 중인 응용 프로그램으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-131">Once it's complete, the browser shows the running app.</span></span>

   ![브라우저 창에서는 'Hello World!'을 표시하는 응용 프로그램이 실행 중이라고 표시합니다.](azure-continuous-deployment/_static/04-browser-runapp.png)

1. <span data-ttu-id="be15d-133">실행 중인 웹 응용 프로그램을 검토 한 후 브라우저를 닫고 응용 프로그램을 중지 하려면 Visual Studio의 도구 모음에서 "디버깅을 중지" 아이콘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-133">After reviewing the running Web app, close the browser and select the "Stop Debugging" icon in the toolbar of Visual Studio to stop the app.</span></span>

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="be15d-134">Azure Portal에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="be15d-134">Create a web app in the Azure Portal</span></span>

<span data-ttu-id="be15d-135">다음 단계에서는 Azure 포털에서 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-135">The following steps create a web app in the Azure Portal:</span></span>

1. <span data-ttu-id="be15d-136">에 로그인 하 고 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-136">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="be15d-137">선택 **새로** 에서 맨 왼쪽 포털 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-137">Select **NEW** at the top left of the portal interface.</span></span>

1. <span data-ttu-id="be15d-138">선택 **웹 + 모바일** > **웹 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-138">Select **Web + Mobile** > **Web App**.</span></span>

   ![Microsoft Azure Portal: 새 단추: Marketplace 아래에서 웹 + 모바일: 주요 앱 아래에서 Web App 단추](azure-continuous-deployment/_static/05-azure-newwebapp.png)

1. <span data-ttu-id="be15d-140">**Web App** 블레이드에서 **App Service 이름**에 고유한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-140">In the **Web App** blade, enter a unique value for the **App Service Name**.</span></span>

   ![Web App 블레이드](azure-continuous-deployment/_static/06-azure-newappblade.png)

   > [!NOTE]
   > <span data-ttu-id="be15d-142">**응용 프로그램 서비스 이름** 이름은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-142">The **App Service Name** name must be unique.</span></span> <span data-ttu-id="be15d-143">포털에서 이름이 제공 된 경우이 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-143">The portal enforces this rule when the name is provided.</span></span> <span data-ttu-id="be15d-144">다른 값을 제공 하는 경우 각 해당 값을 대체 **SampleWebAppDemo** 이 자습서에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-144">If providing a different value, substitute that value for each occurrence of **SampleWebAppDemo** in this tutorial.</span></span>

   <span data-ttu-id="be15d-145">또한 **Web App** 블레이드에서 기존 **App Service 계획/위치**를 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-145">Also in the **Web App** blade, select an existing **App Service Plan/Location** or create a new one.</span></span> <span data-ttu-id="be15d-146">새 계획을 만드는 경우 가격 책정 계층, 위치 및 기타 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-146">If creating a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="be15d-147">앱 서비스 계획에 대 한 자세한 내용은 참조 하십시오. [Azure 앱 서비스 계획 심도 깊은 개요](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-147">For more information on App Service plans, see [Azure App Service plans in-depth overview](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

1. <span data-ttu-id="be15d-148">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-148">Select **Create**.</span></span> <span data-ttu-id="be15d-149">Azure 프로 비전 하 고 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-149">Azure will provision and start the web app.</span></span>

   ![Azure Portal: 샘플 Web App 데모 01 Essentials 블레이드](azure-continuous-deployment/_static/07-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="be15d-151">새 웹앱에 대한 Git 게시 사용</span><span class="sxs-lookup"><span data-stu-id="be15d-151">Enable Git publishing for the new web app</span></span>

<span data-ttu-id="be15d-152">Git는 Azure 앱 서비스 웹 앱을 배포 하는 데 사용할 수 있는 분산된 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-152">Git is a distributed version control system that can be used to deploy an Azure App Service web app.</span></span> <span data-ttu-id="be15d-153">웹 앱 코드는 로컬 Git 리포지토리에 저장 됩니다 및 코드를 원격 리포지토리에 푸시 하 여 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-153">Web app code is stored in a local Git repository, and the code is deployed to Azure by pushing to a remote repository.</span></span>

1. <span data-ttu-id="be15d-154">에 로그인 된 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-154">Log into the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="be15d-155">선택 **응용 프로그램 서비스** Azure 구독과 연결 된 응용 프로그램 서비스의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-155">Select **App Services** to view a list of the app services associated with the Azure subscription.</span></span>

1. <span data-ttu-id="be15d-156">이 자습서의 이전 섹션에서 만든 웹 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-156">Select the web app created in the previous section of this tutorial.</span></span>

1. <span data-ttu-id="be15d-157">**배포** 블레이드에서 **배포 옵션** > **원본 선택** > **로컬 Git 리포지토리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-157">In the **Deployment** blade, select **Deployment options** > **Choose Source** > **Local Git Repository**.</span></span>

   ![설정 블레이드: 배포 원본 블레이드: 원본 블레이드 선택](azure-continuous-deployment/_static/deployment-options.png)

1. <span data-ttu-id="be15d-159">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-159">Select **OK**.</span></span>

1. <span data-ttu-id="be15d-160">웹 앱 또는 다른 앱 서비스 앱 게시에 대 한 배포 자격 증명 설정 이전에 하지 않은, 경우에 지금 설정:</span><span class="sxs-lookup"><span data-stu-id="be15d-160">If deployment credentials for publishing a web app or other App Service app haven't previously been set up, set them up now:</span></span>

   * <span data-ttu-id="be15d-161">선택 **설정** > **배포 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-161">Select **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="be15d-162">**배포 자격 증명 설정** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-162">The **Set deployment credentials** blade is displayed.</span></span>
   * <span data-ttu-id="be15d-163">사용자 이름 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-163">Create a user name and password.</span></span> <span data-ttu-id="be15d-164">Git를 설정 하는 경우 나중에 사용할 암호를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-164">Save the password for later use when setting up Git.</span></span>
   * <span data-ttu-id="be15d-165">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-165">Select **Save**.</span></span>

1. <span data-ttu-id="be15d-166">에 **웹 앱** 블레이드를 **설정** > **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-166">In the **Web App** blade, select **Settings** > **Properties**.</span></span> <span data-ttu-id="be15d-167">배포 하려면 원격 Git 리포지토리의 URL은 아래에 표시 된 **GIT URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-167">The URL of the remote Git repository to deploy to is shown under **GIT URL**.</span></span>

1. <span data-ttu-id="be15d-168">나중에 자습서에서 사용할 **GIT URL** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-168">Copy the **GIT URL** value for later use in the tutorial.</span></span>

   ![Azure Portal: 응용 프로그램 속성 블레이드](azure-continuous-deployment/_static/09-azure-giturl.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="be15d-170">Azure 앱 서비스에 웹 앱을 게시</span><span class="sxs-lookup"><span data-stu-id="be15d-170">Publish the web app to Azure App Service</span></span>

<span data-ttu-id="be15d-171">이 섹션에서는 사용 하 여 Visual Studio 및 푸시 해당 리포지토리 로부터 Azure에 웹 앱을 배포 하는 로컬 Git 리포지토리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-171">In this section, create a local Git repository using Visual Studio and push from that repository to Azure to deploy the web app.</span></span> <span data-ttu-id="be15d-172">관련 단계에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-172">The steps involved include the following:</span></span>

* <span data-ttu-id="be15d-173">로컬 저장소를 Azure에 배포할 수 있도록 GIT URL 값을 사용 하 여 원격 리포지토리 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-173">Add the remote repository setting using the GIT URL value, so the local repository can be deployed to Azure.</span></span>
* <span data-ttu-id="be15d-174">프로젝트 변경 내용을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="be15d-174">Commit project changes.</span></span>
* <span data-ttu-id="be15d-175">Azure에서 원격 저장소에 로컬 저장소에서 프로젝트 변경 내용 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-175">Push project changes from the local repository to the remote repository on Azure.</span></span>

1. <span data-ttu-id="be15d-176">**솔루션 탐색기**에서 **솔루션 'SampleWebAppDemo'**를 마우스 오른쪽 단추로 클릭하고 **커밋**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-176">In **Solution Explorer** right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="be15d-177">**팀 탐색기** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-177">The **Team Explorer** is displayed.</span></span>

   ![팀 탐색기 연결 탭](azure-continuous-deployment/_static/10-team-explorer.png)

1. <span data-ttu-id="be15d-179">**팀 탐색기**에서 **홈**(홈 아이콘) > **설정** > **리포지토리 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-179">In **Team Explorer**, select the **Home** (home icon) > **Settings** > **Repository Settings**.</span></span>

1. <span data-ttu-id="be15d-180">에 **원격** 섹션은 **리포지토리 설정**선택, **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-180">In the **Remotes** section of the **Repository Settings**, select **Add**.</span></span> <span data-ttu-id="be15d-181">**원격 추가** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-181">The **Add Remote** dialog box is displayed.</span></span>

1. <span data-ttu-id="be15d-182">원격 리포지토리의 **이름**을 **Azure SampleApp**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-182">Set the **Name** of the remote to **Azure-SampleApp**.</span></span>

1. <span data-ttu-id="be15d-183">에 대 한 값 설정 **인출** 에 **Git URL** 이 자습서의 앞부분에 나오는 Azure에서 복사 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-183">Set the value for **Fetch** to the **Git URL** that copied from Azure earlier in this tutorial.</span></span> <span data-ttu-id="be15d-184">이 URL은 **.git**로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-184">Note that this is the URL that ends with **.git**.</span></span>

   ![원격 대화 상자 편집](azure-continuous-deployment/_static/11-add-remote.png)

   > [!NOTE]
   > <span data-ttu-id="be15d-186">대신 원격 저장소에서 지정는 **명령 창** 열어는 **명령 창**프로젝트 디렉터리를 변경 하 고 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-186">As an alternative, specify the remote repository from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering the command.</span></span> <span data-ttu-id="be15d-187">예제:</span><span class="sxs-lookup"><span data-stu-id="be15d-187">Example:</span></span>
   >
   > `git remote add Azure-SampleApp https://me@sampleapp.scm.azurewebsites.net:443/SampleApp.git`

1. <span data-ttu-id="be15d-188">**홈**(홈 아이콘) > **설정** > **전역 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-188">Select the **Home** (home icon) > **Settings** > **Global Settings**.</span></span> <span data-ttu-id="be15d-189">이름 및 전자 메일 주소가 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-189">Confirm that the name and email address are set.</span></span> <span data-ttu-id="be15d-190">선택 **업데이트** 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="be15d-190">Select **Update** if required.</span></span>

1. <span data-ttu-id="be15d-191">**홈** > **변경 내용**을 선택하여 **변경 내용** 보기로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-191">Select **Home** > **Changes** to return to the **Changes** view.</span></span>

1. <span data-ttu-id="be15d-192">커밋 메시지를 같은 입력 **초기 푸시 #1** 선택 **커밋**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-192">Enter a commit message, such as **Initial Push #1** and select **Commit**.</span></span> <span data-ttu-id="be15d-193">이 작업을 만듭니다는 *커밋* 로컬로 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-193">This action creates a *commit* locally.</span></span>

   ![팀 탐색기 연결 탭](azure-continuous-deployment/_static/12-initial-commit.png)

   > [!NOTE]
   > <span data-ttu-id="be15d-195">변경 커밋 엔터티나는 **명령 창** 열어는 **명령 창**프로젝트 디렉터리를 변경 하 고에서 git 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-195">As an alternative, commit changes from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering the git commands.</span></span> <span data-ttu-id="be15d-196">예제:</span><span class="sxs-lookup"><span data-stu-id="be15d-196">Example:</span></span>
   >
   > `git add .`
   >
   > `git commit -am "Initial Push #1"`

1. <span data-ttu-id="be15d-197">**홈** > **동기화** > **동작** > **명령 프롬프트 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-197">Select **Home** > **Sync** > **Actions** > **Open Command Prompt**.</span></span> <span data-ttu-id="be15d-198">프로젝트 디렉터리에 명령 프롬프트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-198">The command prompt opens to the project directory.</span></span>

1. <span data-ttu-id="be15d-199">명령 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-199">Enter the following command in the command window:</span></span>

   `git push -u Azure-SampleApp master`

1. <span data-ttu-id="be15d-200">Azure 입력 **배포 자격 증명** Azure 앞부분에서 만든 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-200">Enter the Azure **deployment credentials** password created earlier in Azure.</span></span>

   <span data-ttu-id="be15d-201">이 명령은 로컬 프로젝트 파일을 Azure로 푸시할 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-201">This command starts the process of pushing the local project files to Azure.</span></span> <span data-ttu-id="be15d-202">위 명령의 출력을에서 배포가 성공 했다는 메시지가로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-202">The output from the above command ends with a message that the deployment was successful.</span></span>

   ```
   remote: Finished successfully.
   remote: Running post deployment command(s)...
   remote: Deployment successful.
   To https://username@samplewebappdemo01.scm.azurewebsites.net:443/SampleWebAppDemo01.git
   * [new branch]      master -> master
   Branch master set up to track remote branch master from Azure-SampleApp.
   ```

   > [!NOTE]
   > <span data-ttu-id="be15d-203">공동 작업 프로젝트에 필요한 경우에 강제 설치 하 여 [GitHub](https://github.com) azure 푸시하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-203">If collaboration on the project is required, consider pushing to [GitHub](https://github.com) before pushing to Azure.</span></span>
 
### <a name="verify-the-active-deployment"></a><span data-ttu-id="be15d-204">활성 배포 확인</span><span class="sxs-lookup"><span data-stu-id="be15d-204">Verify the Active Deployment</span></span>

<span data-ttu-id="be15d-205">로컬 환경에서 웹 앱 전송 하기 위해서는 Azure 성공 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-205">Verify that the web app transfer from the local environment to Azure is successful.</span></span>

<span data-ttu-id="be15d-206">에 [Azure 포털](https://portal.azure.com), 웹 사이트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-206">In the [Azure Portal](https://portal.azure.com), select the web app.</span></span> <span data-ttu-id="be15d-207">선택 **배포** > **배포 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-207">Select **Deployment** > **Deployment options**.</span></span>

![Azure Portal: 설정 블레이드: 성공적인 배포를 보여주는 배포 블레이드](azure-continuous-deployment/_static/13-verify-deployment.png)

## <a name="run-the-app-in-azure"></a><span data-ttu-id="be15d-209">Azure에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="be15d-209">Run the app in Azure</span></span>

<span data-ttu-id="be15d-210">웹 앱을 Azure에 배포 했으므로 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-210">Now that the web app is deployed to Azure, run the app.</span></span>

<span data-ttu-id="be15d-211">이 두 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-211">This can be accomplished in two ways:</span></span>

* <span data-ttu-id="be15d-212">Azure 포털에서 웹 앱에 대 한 웹 앱 블레이드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-212">In the Azure Portal, locate the web app blade for the web app.</span></span> <span data-ttu-id="be15d-213">선택 **찾아보기** 기본 브라우저에서 앱을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-213">Select **Browse** to view the app in the default browser.</span></span>
* <span data-ttu-id="be15d-214">브라우저를 열고 웹 앱에 대 한 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-214">Open a browser and enter the URL for the web app.</span></span> <span data-ttu-id="be15d-215">예: `http://SampleWebAppDemo.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="be15d-215">Example: `http://SampleWebAppDemo.azurewebsites.net`</span></span>

## <a name="update-the-web-app-and-republish"></a><span data-ttu-id="be15d-216">웹 앱을 업데이트 하 고 다시 게시</span><span class="sxs-lookup"><span data-stu-id="be15d-216">Update the web app and republish</span></span>

<span data-ttu-id="be15d-217">로컬 코드를 변경한 후 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-217">After making changes to the local code, republish:</span></span>

1. <span data-ttu-id="be15d-218">Visual Studio의 **솔루션 탐색기**에서 *Startup.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-218">In **Solution Explorer** of Visual Studio, open the *Startup.cs* file.</span></span>

1. <span data-ttu-id="be15d-219">`Configure` 메서드에서 `Response.WriteAsync` 메서드를 수정하여 다음과 같이 표시되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-219">In the `Configure` method, modify the `Response.WriteAsync` method so that it appears as follows:</span></span>

   ```csharp
   await context.Response.WriteAsync("Hello World! Deploy to Azure.");
   ```

1. <span data-ttu-id="be15d-220">에 변경 내용을 저장 *Startup.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-220">Save the changes to *Startup.cs*.</span></span>

1. <span data-ttu-id="be15d-221">**솔루션 탐색기**에서 **솔루션 'SampleWebAppDemo'**를 마우스 오른쪽 단추로 클릭하고 **커밋**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-221">In **Solution Explorer**, right-click **Solution 'SampleWebAppDemo'** and select **Commit**.</span></span> <span data-ttu-id="be15d-222">**팀 탐색기** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-222">The **Team Explorer** is displayed.</span></span>

1. <span data-ttu-id="be15d-223">커밋 메시지를 같은 입력 `Update #2`합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-223">Enter a commit message, such as `Update #2`.</span></span>

1. <span data-ttu-id="be15d-224">**커밋** 단추를 눌러 프로젝트 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-224">Press the **Commit** button to commit the project changes.</span></span>

1. <span data-ttu-id="be15d-225">**홈** > **동기화** > **작업** > **푸시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-225">Select **Home** > **Sync** > **Actions** > **Push**.</span></span>

> [!NOTE]
> <span data-ttu-id="be15d-226">변경 내용 적용을 사용 하는 대신는 **명령 창** 열어는 **명령 창**프로젝트 디렉터리를 변경 하 고 git 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-226">As an alternative, push the changes from the **Command Window** by opening the **Command Window**, changing to the project directory, and entering a git command.</span></span> <span data-ttu-id="be15d-227">예제:</span><span class="sxs-lookup"><span data-stu-id="be15d-227">Example:</span></span>
> 
> `git push -u Azure-SampleApp master`

## <a name="view-the-updated-web-app-in-azure"></a><span data-ttu-id="be15d-228">Azure에서 업데이트된 웹앱 보기</span><span class="sxs-lookup"><span data-stu-id="be15d-228">View the updated web app in Azure</span></span>

<span data-ttu-id="be15d-229">업데이트 된 웹 응용 프로그램을 선택 하 여 볼 **찾아보기** Azure 포털에서 또는 브라우저를 열고 웹 앱에 대 한 URL을 입력 하 여 웹 앱 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="be15d-229">View the updated web app by selecting **Browse** from the web app blade in the Azure Portal or by opening a browser and entering the URL for the web app.</span></span> <span data-ttu-id="be15d-230">예: `http://SampleWebAppDemo.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="be15d-230">Example: `http://SampleWebAppDemo.azurewebsites.net`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be15d-231">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="be15d-231">Additional resources</span></span>

* [<span data-ttu-id="be15d-232">VSTS 연속 배포를 사용 하 여 Azure 웹 앱을 빌드하고 게시를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="be15d-232">Use VSTS to Build and Publish to an Azure Web App with Continuous Deployment</span></span>](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)
* [<span data-ttu-id="be15d-233">프로젝트 Kudu</span><span class="sxs-lookup"><span data-stu-id="be15d-233">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
