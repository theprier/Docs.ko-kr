---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS에서 팀 프로젝트를 만들면 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: 98725b9d2f669e6520f24c3a8122be086002e96a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810226"
---
<a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="11a47-103">TFS에서 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="11a47-103">Creating a Team Project in TFS</span></span>
====================
<span data-ttu-id="11a47-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="11a47-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="11a47-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="11a47-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="11a47-106">이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>


<span data-ttu-id="11a47-107">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="11a47-108">작업 개요</span><span class="sxs-lookup"><span data-stu-id="11a47-108">Task Overview</span></span>

<span data-ttu-id="11a47-109">프로 비전 하 고 TFS에서 새 팀 프로젝트를 사용 하 여, 이러한 높은 수준의 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="11a47-110">새 팀 프로젝트를 생성 하는 사용자에 게 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="11a47-111">팀 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-111">Create the team project.</span></span>
- <span data-ttu-id="11a47-112">프로젝트에서 작동 하는 팀 멤버에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="11a47-113">일부 콘텐츠를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-113">Check in some content.</span></span>

<span data-ttu-id="11a47-114">이 항목에서는 이러한 절차를 수행 하는 방법을 표시 되 고 사용자 및 각 프로시저에 대 한 책임을 집니다 가능성이 있는 작업 역할을 식별 하는.</span><span class="sxs-lookup"><span data-stu-id="11a47-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="11a47-115">조직의 구조에 따라 이러한 각 작업 수를 다른 사용자의 책임에 유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="11a47-116">작업은이 문서의 연습 설치 되었으며 TFS를 구성 하 고 팀 프로젝트 컬렉션 구성 프로세스의 일부로 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="11a47-117">이러한 가정에 대 한 자세한 내용은 및 시나리오에 보다 일반적인 배경 정보에 대 한 참조 [웹 배포용 TFS 빌드 서버를 구성](configuring-a-tfs-build-server-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="11a47-118">팀 프로젝트 생성기에 대 한 권한 부여</span><span class="sxs-lookup"><span data-stu-id="11a47-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="11a47-119">새 팀 프로젝트를 만들기 위해 이러한 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="11a47-120">있어야 합니다 **새 프로젝트를 만들** TFS 응용 프로그램 계층에 대 한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="11a47-121">일반적으로 사용자를 추가 하 여이 권한을 부여 합니다 **Project Collection Administrators** TFS 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="11a47-122">합니다 **Team Foundation Administrators** 전역 그룹에도이 권한을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="11a47-123">TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 컬렉션 내의 새 팀 사이트를 만들 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="11a47-124">일반적으로 사용 하 여 SharePoint 그룹에 사용자를 추가 하 여이 권한을 부여 **전면적인** SharePoint에 대 한 권한 사이트 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="11a47-125">SQL Server Reporting Services 기능을 사용 하는 경우의 구성원 이어야 합니다 **Team Foundation Content Manager** Reporting Services의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="11a47-126">이러한 절차를 수행 하는 사람?</span><span class="sxs-lookup"><span data-stu-id="11a47-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="11a47-127">일반적으로 개인 또는 TFS 배포를 관리 하는 방법과 그룹 이러한 프로시저도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="11a47-128">사용 권한 집합을 높은 이기 때문에 새 팀 프로젝트 일반적으로 생성 됩니다 사용자의 작은 하위 집합에서 TFS 배포를 관리 하는 것에 대 한 책임을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="11a47-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="11a47-129">개발자가 부여 되지 않습니다 일반적으로 새 팀 프로젝트를 만드는 데 필요한 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="11a47-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="11a47-130">TFS에서 권한 부여</span><span class="sxs-lookup"><span data-stu-id="11a47-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="11a47-131">첫 번째 상위 수준 작업 사용자를 추가 하는 사용자가 새 팀 프로젝트를 만들 수 있도록 하려는 경우는 **Project Collection Administrators** 팀 프로젝트 컬렉션에 대 한 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="11a47-132">**Project Collection Administrators 그룹에 사용자를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="11a47-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="11a47-133">TFS 서버의는 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Team Foundation Server 2010**를 클릭 하 고 **Team Foundation 관리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="11a47-134">탐색 트리 뷰에서 확장 **응용 프로그램 계층**를 클릭 하 고 **팀 프로젝트 컬렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="11a47-135">에 **팀 프로젝트 컬렉션** 창 팀 프로젝트를 관리 하려는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="11a47-136">에 **일반적인** 탭을 클릭 **그룹 멤버 자격**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="11a47-137">에 **글로벌 그룹** 대화 상자에서를 **Project Collection Administrators** 그룹을 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="11a47-138">에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="11a47-139">에 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 새 팀 프로젝트를 만들 수 있게 되기를 원하는 사용자의 사용자 이름을 클릭 **이름 확인**를 클릭 하 고 **확인** .</span><span class="sxs-lookup"><span data-stu-id="11a47-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="11a47-140">에 **Team Foundation Server 그룹 속성** 대화 상자, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="11a47-141">에 **글로벌 그룹** 대화 상자, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="11a47-142">SharePoint Services의 권한 부여</span><span class="sxs-lookup"><span data-stu-id="11a47-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="11a47-143">다음으로, TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 컬렉션에서 새 팀 사이트를 만들 수 있는 사용자 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="11a47-144">**SharePoint 사이트 컬렉션에 대 한 모든 권한을 부여 하려면**</span><span class="sxs-lookup"><span data-stu-id="11a47-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="11a47-145">Team Foundation Server 관리 콘솔에서에 **팀 프로젝트 컬렉션** 페이지에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="11a47-146">에 **SharePoint 사이트** 탭에서 값을 확인 합니다 **현재 기본 사이트 위치** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="11a47-147">Internet Explorer를 열고 2 단계에서 언급 한 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a47-148">하지 로그인 Windows에는 팀 프로젝트 컬렉션을 만든 사용자로, SharePoint에 로그인이 사용자로 계속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="11a47-149">에 **사이트 작업** 메뉴에서 클릭 **사이트 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="11a47-150">에 **사이트 설정** 페이지의 **사용자 권한과**, 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="11a47-151">왼쪽된 탐색 창에서 클릭 **그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="11a47-152">에 **사용자 및 그룹: 모든 그룹** 페이지에서 클릭 **그룹이이 사이트에 대 한 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="11a47-153">표시 될 수 있습니다는 <strong>HTTP 404 찾을 수 없음</strong> 이중 HTTP 인코딩 버그로 인해 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="11a47-154">이 경우이 사용 하 여 URL을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="11a47-155">`[site_collection_URL]/_layouts/permsetup.aspx` 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="11a47-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="11a47-156">에 **그룹이이 사이트에 대 한 설정** 페이지, 팀 프로젝트를 생성 하는 사용자를 추가 합니다 **소유자** 그룹을 마우스 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="11a47-157">사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 하는 방법은 참조 하세요 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="11a47-158">새 팀 프로젝트를 만들고 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="11a47-159">사용자에 게 필요한 권한이 후 사용할 수 있습니다 합니다 **팀 탐색기** 새 팀 프로젝트를 만들려면 Visual Studio 2010의 창.</span><span class="sxs-lookup"><span data-stu-id="11a47-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="11a47-160">이 방법은 필요한 모든 정보를 수집 하 고 TFS, SharePoint 및 SQL Server Reporting Services에서 필요한 작업을 수행 하는 마법사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="11a47-161">추가 하 고 콘텐츠를 수정할 수 있도록 개발자 팀의 구성원에 게 새 팀 프로젝트에 대 한 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="11a47-162">이러한 절차를 수행 하는 사람?</span><span class="sxs-lookup"><span data-stu-id="11a47-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="11a47-163">일반적으로 TFS 관리자 또는 개발자 팀 리더는 이러한 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="11a47-164">새 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="11a47-164">Create a New Team Project</span></span>

<span data-ttu-id="11a47-165">다음 절차에는 TFS 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="11a47-166">**새 팀 프로젝트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="11a47-166">**To create a new team project**</span></span>

1. <span data-ttu-id="11a47-167">에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Visual Studio 2010**를 마우스 오른쪽 단추로 클릭 **Microsoft Visual Studio 2010**, 클릭 하 고 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a47-168">관리자 권한으로 Visual Studio 2010을 실행 하지 않으면, 새 팀 프로젝트 마법사에서 마지막 단계에서 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="11a47-169">경우는 **사용자 계정 컨트롤** 대화 상자가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="11a47-170">Visual Studio에서에 **Team** 메뉴에서 클릭 **Team Foundation Server에 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a47-171">TFS 서버에 연결을 이미 구성한 경우에 4 ~ 7 단계를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="11a47-172">에 **팀 프로젝트에 연결** 대화 상자, 클릭 **서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="11a47-173">에 **Team Foundation Server 추가/제거** 대화 상자, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="11a47-174">에 **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 제공 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="11a47-175">에 **Team Foundation Server 추가/제거** 대화 상자, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="11a47-176">에 **팀 프로젝트에 연결** 대화 상자에서 팀을 선택 하려면 연결 하려는 TFS 인스턴스에 프로젝트 컬렉션에 추가 하 고 클릭 하려는 **Connect**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="11a47-177">에 **팀 탐색기** 창을 마우스 오른쪽 단추로 클릭 팀 프로젝트 컬렉션, 클릭 **새 팀 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="11a47-178">에 **새 프로젝트** 대화 상자에서 이름 및 팀 프로젝트에 대 한 설명을 제공 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a47-179">공백이 포함 된 팀 프로젝트에는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 출력 경로에서 패키지를 배포할 수에 도달 하면 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="11a47-180">경로에 공백이 웹 배포 명령을 실행 하는 훨씬 더 어렵게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="11a47-181">에 **프로세스 템플릿 선택** 페이지에서 프로세스 템플릿을 사용 하 여 개발 프로세스를 관리 하 고 클릭 하려는 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="11a47-182">Tfs 프로세스 템플릿에 자세한 내용은 참조 [프로세스 템플릿 및 도구](https://msdn.microsoft.com/vstudio/aa718795)합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="11a47-183">에 **팀 사이트 설정** 페이지에서 변경 하지 않고 기본 설정을 유지 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="11a47-184">이 설정을 만들거나 TFS 팀 프로젝트와 연결 된 SharePoint 팀 사이트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="11a47-185">개발 팀이이 사이트를 사용 설명서를 관리, 토론에 참여, wiki 페이지 만들기 및 코드에 관련 되지 않은 다른 다양 한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="11a47-186">자세한 내용은 [SharePoint 제품 간의 상호 작용 및 Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="11a47-187">에 **소스 제어 설정 지정** 페이지에서 변경 하지 않고 기본 설정을 유지 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="11a47-188">이 설정은 식별 하거나 콘텐츠에 대 한 루트 폴더로 할 TFS 폴더 계층의 위치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="11a47-189">에 **팀 프로젝트 설정 확인** 페이지에서 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="11a47-190">경우 새 팀 프로젝트를 성공적으로 생성 되는 **팀 프로젝트를 만들었습니다** 페이지에서 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="11a47-191">팀 프로젝트에 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-191">Add Users to a Team Project</span></span>

<span data-ttu-id="11a47-192">새 팀 프로젝트를 만들었으므로 이제 추가 하 고 콘텐츠 공동 작업을 시작할 수 있도록 사용자에 게 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="11a47-193">**팀 프로젝트에 사용자를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="11a47-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="11a47-194">Visual Studio 2010에서에 **팀 탐색기** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭을 가리킵니다 **팀 프로젝트 설정**, 클릭 하 고 **그룹 멤버 자격**.</span><span class="sxs-lookup"><span data-stu-id="11a47-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="11a47-195">추가, 수정, 소스 제어에서 코드를 제거 하는 사용자를 사용 하도록 설정 하려면에 그렇게 해야 합니다 **참가자** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="11a47-196">**프로젝트 그룹** 대화 상자를 선택 합니다 **참가자** 그룹을 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="11a47-197">에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="11a47-198">에 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 팀 프로젝트에 추가 하려는 사용자의 사용자 이름을 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="11a47-199">에 **Team Foundation Server 그룹 속성** 대화 상자, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="11a47-200">에 **프로젝트 그룹** 대화 상자, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="11a47-201">결론</span><span class="sxs-lookup"><span data-stu-id="11a47-201">Conclusion</span></span>

<span data-ttu-id="11a47-202">이 시점에서 새 팀 프로젝트를 사용 하려면 준비 되어 개발자 팀 콘텐츠를 추가 하 고 공동 작업 개발 프로세스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="11a47-203">다음 항목인 [소스 제어에 추가 콘텐츠](adding-content-to-source-control.md), 소스 제어에 콘텐츠를 추가 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="11a47-204">추가 정보</span><span class="sxs-lookup"><span data-stu-id="11a47-204">Further Reading</span></span>

<span data-ttu-id="11a47-205">TFS에서 팀 프로젝트 만들기에 대 한 광범위 한 지침을 참조 하세요 [팀 프로젝트를 만들](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="11a47-206">사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 하는 방법은 참조 하세요 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="11a47-207">팀 프로젝트에 사용자를 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [팀 프로젝트에 사용자 추가](https://msdn.microsoft.com/library/bb558971.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="11a47-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="11a47-208">[이전](configuring-team-foundation-server-for-web-deployment.md)
> [다음](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="11a47-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
