---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: "TFS에서 팀 프로젝트를 만들면 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: 4cb0d72330086ecb8cd9e6fb70ce0a57698dda5a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="b1490-103">TFS에서 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b1490-103">Creating a Team Project in TFS</span></span>
====================
<span data-ttu-id="b1490-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="b1490-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="b1490-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="b1490-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="b1490-106">이 항목에서는 Team Foundation Server (TFS) 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>


<span data-ttu-id="b1490-107">이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="b1490-108">작업 개요</span><span class="sxs-lookup"><span data-stu-id="b1490-108">Task Overview</span></span>

<span data-ttu-id="b1490-109">프로 비전 하 고 TFS에서 새 팀 프로젝트를 사용 하려면 같은 대략적인 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="b1490-110">사용자에 게 새 팀 프로젝트를 만들 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="b1490-111">팀 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-111">Create the team project.</span></span>
- <span data-ttu-id="b1490-112">프로젝트에서 작업 하는 팀 멤버에 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="b1490-113">일부 콘텐츠를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-113">Check in some content.</span></span>

<span data-ttu-id="b1490-114">이 항목에서는 이러한 절차를 수행 하는 방법을 설명 하 고 사용자와 각 프로시저에 대 한 책임을 가능성이 있는 작업 역할 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="b1490-115">즉, 조직의 구조에 따라 각이 작업 수 있으므로 주의 해야 다른 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="b1490-116">작업은이 항목의 연습에서는 설치 되었으며 TFS를 구성 하 고 팀 프로젝트 컬렉션의 구성 프로세스의 일부로 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="b1490-117">이러한 가정에 대 한 자세한 내용은 하 고 그렇지 않은 경우 보다 일반적인 배경 정보에 대 한 참조 [웹 배포를 위한 TFS 빌드 서버 구성](configuring-a-tfs-build-server-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="b1490-118">팀 프로젝트 생성자에 게 권한을 부여합니다</span><span class="sxs-lookup"><span data-stu-id="b1490-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="b1490-119">새 팀 프로젝트를 만들기 위해 이러한 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="b1490-120">있어야는 **새 프로젝트를 만들** TFS 응용 프로그램 계층에 대 한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="b1490-121">일반적으로 사용자를 추가 하 여이 권한을 부여는 **Project Collection Administrators** TFS 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="b1490-122">**Team Foundation Administrators** 글로벌 그룹에도이 권한이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="b1490-123">TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 모음 내에서 새 팀 사이트를 만들 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="b1490-124">일반적으로 SharePoint 그룹에 사용자를 추가 하 여이 권한을 부여 **모든 권한** SharePoint에 대 한 권한 사이트 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="b1490-125">SQL Server Reporting Services 기능을 사용 하는 경우의 멤버 여야 합니다는 **Team Foundation Content Manager** Reporting Services의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="b1490-126">이러한 절차를 수행 하는 사람?</span><span class="sxs-lookup"><span data-stu-id="b1490-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="b1490-127">일반적으로 사람 또는 그룹에 TFS 배포를 운영 하는 이러한 프로시저도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="b1490-128">매우 강력한 권한의 권한 집합 이기 때문에 새 팀 프로젝트는 일반적 만들어집니다 사용자의 작은 하위 집합에서 TFS 배포를 관리 하기 위한 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="b1490-129">개발자는 일반적으로 권한은 할당 하지는 새 팀 프로젝트를 만드는 데 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="b1490-130">TFS에서 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="b1490-131">첫 번째 상위 수준 작업은 사용자를 추가 하려면 사용자가 새 팀 프로젝트를 만들 수 있도록 하려는 경우는 **Project Collection Administrators** 팀 프로젝트 컬렉션에 대 한 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="b1490-132">**Project Collection Administrators 그룹에 사용자를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="b1490-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="b1490-133">TFS 서버에서에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Team Foundation Server 2010**, 클릭 하 고 **Team Foundation 관리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="b1490-134">탐색 트리 보기에서 확장 **응용 프로그램 계층**, 클릭 하 고 **팀 프로젝트 컬렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="b1490-135">에 **팀 프로젝트 컬렉션** 창에서 팀 프로젝트를 관리 하려는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="b1490-136">에 **일반** 탭을 클릭 **그룹 구성원 자격**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="b1490-137">에 **글로벌 그룹** 대화 상자는 **Project Collection Administrators** 그룹을 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="b1490-138">에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="b1490-139">에 **사용자, 컴퓨터 또는 그룹 선택** 새 팀 프로젝트를 만들 수 있도록 하려는 사용자의 사용자 이름을 클릭 하 여 대화 상자에서 **이름 확인**, 클릭 하 고 **확인** .</span><span class="sxs-lookup"><span data-stu-id="b1490-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="b1490-140">에 **Team Foundation Server 그룹 속성** 대화 상자를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="b1490-141">에 **글로벌 그룹** 대화 상자를 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="b1490-142">SharePoint Services의 권한 부여</span><span class="sxs-lookup"><span data-stu-id="b1490-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="b1490-143">다음으로, TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 모음에 새 팀 사이트를 만들 수 있는 사용자 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="b1490-144">**SharePoint 사이트 모음에 대 한 모든 권한을 부여 하려면**</span><span class="sxs-lookup"><span data-stu-id="b1490-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="b1490-145">Team Foundation Server 관리 콘솔에에 **팀 프로젝트 컬렉션** 페이지에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="b1490-146">에 **SharePoint 사이트** 탭에서 값을 확인는 **현재 기본 사이트 위치** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="b1490-147">Internet Explorer를 열고 2 단계에서 기록해둔 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1490-148">하지 로그인 Windows에는 팀 프로젝트 컬렉션을 만든 사용자로, 하는 경우 SharePoint에이 사용자로 로그인이 계속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="b1490-149">에 **사이트 작업** 메뉴를 클릭 하 여 **사이트 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="b1490-150">에 **사이트 설정** 페이지의 **사용자 및 사용 권한**, 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="b1490-151">왼쪽된 탐색 패널에서 클릭 **그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="b1490-152">에 **사용자 및 그룹: 모든 그룹** 페이지 **그룹이이 사이트에 대 한 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

    > [!NOTE]
    > <span data-ttu-id="b1490-153">나타날 수 있습니다는 **HTTP 404 찾을 수 없음** 오류 이중 HTTP 인코딩 버그 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-153">You may receive an **HTTP 404 Not Found** error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="b1490-154">이 경우이 URL을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-154">If this occurs, replace the URL with this:</span></span>   
    > <span data-ttu-id="b1490-155">[*사이트 컬렉션 URL*] /\_layouts/permsetup.aspx</span><span class="sxs-lookup"><span data-stu-id="b1490-155">[*site collection URL*]/\_layouts/permsetup.aspx</span></span>  
    > <span data-ttu-id="b1490-156">예:</span><span class="sxs-lookup"><span data-stu-id="b1490-156">For example:</span></span>  
    > <span data-ttu-id="b1490-157">http://tfs/sites/Fabrikam%20Web%20Projects/\_layouts/permsetup.aspx</span><span class="sxs-lookup"><span data-stu-id="b1490-157">http://tfs/sites/Fabrikam%20Web%20Projects/\_layouts/permsetup.aspx</span></span>
8. <span data-ttu-id="b1490-158">에 **그룹이이 사이트에 대 한 설정** 페이지에서 사용자를 팀 프로젝트를 만들고는 추가 **소유자** 그룹을 마우스 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-158">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="b1490-159">사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만드는 설정에 대 한 자세한 내용은 참조 하십시오. [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/en-us/library/dd547204.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-159">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/en-us/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="b1490-160">새 팀 프로젝트를 만들고 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="b1490-160">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="b1490-161">필요한 사용 권한이 면 사용할 수 있습니다는 **팀 탐색기** 새 팀 프로젝트를 만들려면 Visual Studio 2010의 창.</span><span class="sxs-lookup"><span data-stu-id="b1490-161">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="b1490-162">이 방법은 필요한 모든 정보를 수집 하 고 TFS, SharePoint 및 SQL Server Reporting Services에서 필요한 작업을 수행 하는 마법사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-162">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="b1490-163">새 팀 프로젝트에 대 한 권한을 추가 하 고 콘텐츠를 수정할 수 있도록 개발자 팀의 멤버에 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-163">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="b1490-164">이러한 절차를 수행 하는 사람?</span><span class="sxs-lookup"><span data-stu-id="b1490-164">Who Performs These Procedures?</span></span>

<span data-ttu-id="b1490-165">일반적으로 TFS 관리자 또는 개발자 팀 리더는이 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-165">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="b1490-166">새 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b1490-166">Create a New Team Project</span></span>

<span data-ttu-id="b1490-167">다음 절차에는 TFS 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-167">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="b1490-168">**새 팀 프로젝트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="b1490-168">**To create a new team project**</span></span>

1. <span data-ttu-id="b1490-169">에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft Visual Studio 2010**를 마우스 오른쪽 단추로 클릭 **Microsoft Visual Studio 2010**, 클릭 하 고 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-169">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1490-170">관리자 권한으로 Visual Studio 2010을 실행 하지 않으면, 새 팀 프로젝트 마법사는 마지막 단계에서 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-170">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="b1490-171">경우는 **사용자 계정 컨트롤** 대화 상자가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-171">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="b1490-172">Visual Studio에서에 **팀** 메뉴를 클릭 하 여 **Team Foundation Server에 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-172">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1490-173">TFS 서버에 대 한 연결을 이미 구성 했다면 4-7 단계를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-173">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="b1490-174">에 **팀 프로젝트에 연결** 대화 상자를 클릭 **서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-174">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="b1490-175">에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-175">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="b1490-176">에 **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-176">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="b1490-177">에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-177">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="b1490-178">에 **팀 프로젝트에 연결** 대화 상자에서 팀 선택에 연결 하려는 TFS 인스턴스에 프로젝트 컬렉션에 추가 하 고 클릭 하려는 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-178">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="b1490-179">에 **팀 탐색기** 창에서 마우스 오른쪽 단추로 팀 프로젝트 컬렉션을 누른 **새 팀 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-179">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="b1490-180">에 **새 팀 프로젝트** 대화 상자에서 이름과 팀 프로젝트에 대 한 설명을 입력 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-180">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1490-181">팀 프로젝트에 공백이 있으면 출력 경로에서 패키지를 배포 하는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하도록 제공 되 면 몇 가지 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-181">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="b1490-182">경로에 공백이 웹 배포 명령을 실행 하 훨씬 더 어렵게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-182">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="b1490-183">에 **프로세스 템플릿 선택** 페이지에서 클릭 하 고 개발 프로세스를 관리 하는 데 사용할 프로세스 템플릿을 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-183">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1490-184">프로세스 템플릿 TFS에 대 한 자세한 내용은 참조 하십시오. [프로세스 템플릿과 도구](https://msdn.microsoft.com/en-us/vstudio/aa718795)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-184">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/en-us/vstudio/aa718795).</span></span>
12. <span data-ttu-id="b1490-185">에 **팀 사이트 설정** 페이지 변경 하지 않은 기본 설정을 유지 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-185">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="b1490-186">이 설정을 만들거나 TFS 팀 프로젝트와 연결 된 SharePoint 팀 사이트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-186">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="b1490-187">개발 팀이이 사이트를 사용 설명서를 관리할를 토론에 참여, wiki 페이지를 만들고 코드와 관련 되지 않은 다른 다양 한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-187">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="b1490-188">자세한 내용은 참조 [SharePoint 제품 간의 상호 작용 및 Team Foundation Server](https://msdn.microsoft.com/en-us/library/ms253177.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-188">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/en-us/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="b1490-189">에 **소스 제어 설정 지정** 페이지 변경 하지 않은 기본 설정을 유지 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-189">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="b1490-190">이 설정은 식별 하거나 루트 폴더 콘텐츠를 작동할 TFS 폴더 계층의 위치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-190">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="b1490-191">에 **팀 프로젝트 설정 확인** 페이지 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-191">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="b1490-192">때 새 팀 프로젝트가 성공적으로 만들어지면에 **팀 프로젝트를 만들었습니다** 페이지 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-192">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="b1490-193">팀 프로젝트에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="b1490-193">Add Users to a Team Project</span></span>

<span data-ttu-id="b1490-194">새 팀 프로젝트를 만들었으므로 이제 추가 하 고 공동 작업에 콘텐츠를 시작할 수 있도록 사용자에 게 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-194">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="b1490-195">**팀 프로젝트에 사용자를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="b1490-195">**To add users to a team project**</span></span>

1. <span data-ttu-id="b1490-196">Visual Studio 2010에서에 **팀 탐색기** 창, 팀 프로젝트를 마우스 오른쪽 단추로 클릭를 가리킨 **팀 프로젝트 설정**, 클릭 하 고 **그룹 멤버 자격**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-196">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="b1490-197">그렇게 하는 추가, 수정 및 소스 제어에서 코드를 제거 하는 사용자를 사용 하도록 설정 하려면 필요는 **참가자** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-197">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="b1490-198">에 **프로젝트 그룹** 대화 상자는 **참가자** 그룹을 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-198">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="b1490-199">에 **Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-199">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="b1490-200">에 **사용자, 컴퓨터 또는 그룹 선택** 팀 프로젝트에 추가 하려는 사용자의 사용자 이름을 클릭 하 여 대화 상자에서 **이름 확인**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-200">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="b1490-201">에 **Team Foundation Server 그룹 속성** 대화 상자를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-201">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="b1490-202">에 **프로젝트 그룹** 대화 상자를 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-202">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b1490-203">결론</span><span class="sxs-lookup"><span data-stu-id="b1490-203">Conclusion</span></span>

<span data-ttu-id="b1490-204">이 시점에서 새 팀 프로젝트 되 사용할 수 있는 상태가 하 고 콘텐츠를 추가 하 고 공동 작업 개발 프로세스에 개발자 팀 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-204">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="b1490-205">다음 항목인 [소스 제어에 추가 콘텐츠](adding-content-to-source-control.md), 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-205">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="b1490-206">추가 정보</span><span class="sxs-lookup"><span data-stu-id="b1490-206">Further Reading</span></span>

<span data-ttu-id="b1490-207">TFS에서 팀 프로젝트를 만드는 방법에 광범위 한 지침을 참조 하십시오. [팀 프로젝트를 만들](https://msdn.microsoft.com/en-us/library/ms181477(v=VS.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-207">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/en-us/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="b1490-208">사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만드는 설정에 대 한 자세한 내용은 참조 하십시오. [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/en-us/library/dd547204.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-208">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/en-us/library/dd547204.aspx).</span></span> <span data-ttu-id="b1490-209">팀 프로젝트에 사용자를 추가 하는 방법에 대 한 자세한 내용은 참조 하십시오. [팀 프로젝트에 사용자 추가](https://msdn.microsoft.com/en-us/library/bb558971.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1490-209">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/en-us/library/bb558971.aspx).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b1490-210">[이전](configuring-team-foundation-server-for-web-deployment.md)
[다음](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="b1490-210">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
