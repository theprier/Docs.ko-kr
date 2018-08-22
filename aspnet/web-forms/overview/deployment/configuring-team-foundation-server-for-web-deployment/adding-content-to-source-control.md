---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 소스 제어에 콘텐츠 추가 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 Team Foundation Server (TFS) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법에 설명 합니다. 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 2119705a75d0717d05d4a7db69b3f5d38b1cdd45
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829626"
---
<a name="adding-content-to-source-control"></a><span data-ttu-id="6ccbb-104">소스 제어에 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="6ccbb-104">Adding Content to Source Control</span></span>
====================
<span data-ttu-id="6ccbb-105">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="6ccbb-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="6ccbb-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="6ccbb-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="6ccbb-107">이 항목에서는 Team Foundation Server (TFS) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="6ccbb-108">TFS에서 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법을 설명 하 고 소스 제어에 프레임 워크 또는 어셈블리와 같은 외부 종속성을 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>


<span data-ttu-id="6ccbb-109">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="6ccbb-110">작업 개요</span><span class="sxs-lookup"><span data-stu-id="6ccbb-110">Task Overview</span></span>

<span data-ttu-id="6ccbb-111">대부분의 경우에서 개발자 팀의 모든 멤버는 소스 제어에 내용을 추가할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="6ccbb-112">TFS에서 소스 제어에 솔루션을 추가 하려면 다음 대략적인 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="6ccbb-113">팀 프로젝트에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-113">Connect to a team project.</span></span>
- <span data-ttu-id="6ccbb-114">로컬 컴퓨터의 폴더 구조에는 서버의 팀 프로젝트 폴더 구조를 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="6ccbb-115">소스 제어에 솔루션 및 해당 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="6ccbb-116">소스 제어에 모든 외부 종속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="6ccbb-117">이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="6ccbb-118">작업은이 항목의 연습에서는 콘텐츠를 관리 하려면 새 TFS 팀 프로젝트를 이미 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="6ccbb-119">새 팀 프로젝트를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [TFS에서 팀 프로젝트를 만들면](creating-a-team-project-in-tfs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="6ccbb-120">이러한 절차를 수행 하는 사람?</span><span class="sxs-lookup"><span data-stu-id="6ccbb-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="6ccbb-121">대부분의 경우, 개발자 팀의 모든 멤버를 추가 하 여 특정 팀 프로젝트 내에서 콘텐츠를 수정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="6ccbb-122">팀 프로젝트에 연결한 폴더 매핑 만들기</span><span class="sxs-lookup"><span data-stu-id="6ccbb-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="6ccbb-123">소스 제어에 콘텐츠를 추가 하기 전에 로컬 컴퓨터에 서버 폴더 구조 및 파일 시스템 간의 매핑을 만들고 팀 프로젝트에 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="6ccbb-124">**팀 프로젝트에 연결 하 여 로컬 경로 매핑**</span><span class="sxs-lookup"><span data-stu-id="6ccbb-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="6ccbb-125">개발자 워크스테이션에서 Visual Studio 2010을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="6ccbb-126">Visual Studio에서에 **Team** 메뉴에서 클릭 **Team Foundation Server에 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6ccbb-127">TFS 서버에 연결을 이미 구성한 경우에 3 ~ 6 단계를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="6ccbb-128">에 **팀 프로젝트에 연결** 대화 상자, 클릭 **서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="6ccbb-129">에 **Team Foundation Server 추가/제거** 대화 상자, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="6ccbb-130">에 **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 제공 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="6ccbb-131">에 **Team Foundation Server 추가/제거** 대화 상자, 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="6ccbb-132">에 **팀 프로젝트에 연결** 대화 상자에서 팀을 선택 하려면 연결 하려는 TFS 인스턴스 선택 프로젝트 컬렉션에 추가 하려는 팀 프로젝트를 선택 하 고 클릭 한 다음 **Connect**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="6ccbb-133">에 **팀 탐색기** 창에서 팀 프로젝트를 확장 하 고 두 번 클릭 **소스 제어**입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="6ccbb-134">에 **소스 제어 탐색기** 탭을 클릭 **매핑되지**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="6ccbb-135">에 **맵** 대화 상자의 합니다 **로컬 폴더** 상자로 이동 (또는 만들기) 팀 프로젝트에 대 한 루트 폴더와 작동 하 고 클릭 한 다음 로컬 폴더 **맵**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="6ccbb-136">원본 파일을 다운로드 하 라는 메시지가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="6ccbb-137">이 시점에서 팀 프로젝트에 대 한 서버 쪽 폴더 개발자 워크스테이션의 로컬 폴더에 매핑 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="6ccbb-138">로컬 폴더 구조에 팀 프로젝트에서 모든 기존 콘텐츠를 다운로드 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="6ccbb-139">이제 소스 제어에 고유한 콘텐츠를 추가 하려면 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="6ccbb-140">소스 제어에 프로젝트 및 솔루션 추가</span><span class="sxs-lookup"><span data-stu-id="6ccbb-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="6ccbb-141">프로젝트 및 솔루션 소스 제어에 추가 하려면 먼저 로컬 컴퓨터에서 팀 프로젝트의 매핑된 폴더를 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="6ccbb-142">다음에 추가 된 서버와 동기화 할 콘텐츠에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="6ccbb-143">**소스 제어에 프로젝트를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="6ccbb-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="6ccbb-144">개발자 워크스테이션에서 프로젝트 및 솔루션 팀 프로젝트의 매핑된 폴더 구조 내에서 적절 한 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6ccbb-145">대부분의 조직에서는 소스 제어에서 프로젝트 및 솔루션은 구성 하는 방법에 대 한 기본 접근법을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="6ccbb-146">폴더를 구조화 하는 방법에 대 한 지침을 참조 하세요 [방법: Team Foundation Server에서 구조 Your 소스 제어 폴더](https://msdn.microsoft.com/library/bb668992.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="6ccbb-147">Visual Studio 2010에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="6ccbb-148">에 **솔루션 탐색기** 창에서 솔루션을 마우스 오른쪽 단추로 클릭 **원본 제어에 솔루션 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="6ccbb-149">조직 구조 내용 TFS에 좋아요 표시 하는 방법에 따라 일부 경우에 개별적으로 소스 코드에 구성 되는 방식을 더 세밀 하 게 제어할 수 있도록 소스 제어에 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="6ccbb-150">있는지 확인 합니다 **소스 제어 탐색기** 탭에는 팀 프로젝트에 대 한 서버 폴더 구조에 추가한 콘텐츠가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="6ccbb-151">합니다 **소스 제어 탐색기** 탭 더 이상 로컬 파일 시스템에 매핑된 폴더에 솔루션을 추가 하기 때문에 메시지를 표시 하 여 콘텐츠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="6ccbb-152">솔루션이 매핑되지 않은 위치에 있는 경우 TFS와 로컬 파일 시스템의 폴더 위치를 지정 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="6ccbb-153">에 **소스 제어 탐색기** 탭을 **폴더** 창 팀 프로젝트를 마우스 오른쪽 단추로 클릭 (예를 들어 **ContactManager**), 클릭 하 고 **체크 인 보류 중인 변경 내용을**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="6ccbb-154">에 **체크 인-소스 파일** 대화 상자에 설명을 입력 하 고 클릭 **체크**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="6ccbb-155">이 시점에서 TFS에서 소스 제어에 솔루션을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="6ccbb-156">소스 제어에 외부 종속성 추가</span><span class="sxs-lookup"><span data-stu-id="6ccbb-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="6ccbb-157">소스 제어에 프로젝트 또는 솔루션에 추가 하면 모든 파일 및 프로젝트 또는 솔루션 내에 폴더 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="6ccbb-158">그러나 대부분의 경우 프로젝트 및 솔루션도 사용 제대로 작동 하려면 로컬 어셈블리와 같은 외부 종속성을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="6ccbb-159">코드를 성공적으로 빌드 팀 빌드 및 개발자 팀의 다른 멤버를 둘 다를 수 있도록 하려면 소스 제어 하는 이러한 리소스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="6ccbb-160">예를 들어 Contact Manager 샘플 솔루션에 대 한 폴더 구조는 패키지 폴더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="6ccbb-161">ADO.NET Entity Framework 4.1에 대 한 어셈블리 및 다양 한 지원 리소스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="6ccbb-162">패키지 폴더 Contact Manager 솔루션의 일부가 아닙니다. 하지만 솔루션 없이 성공적으로 빌드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="6ccbb-163">솔루션을 빌드하려면 Team Build를 사용 하려면 소스 제어에 패키지 폴더를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="6ccbb-164">패키지 폴더를 포함 하는 것이 Visual Studio 2010 용 NuGet 확장을 사용 하 여 솔루션은 Entity Framework 또는 유사한 리소스를 추가 하면 어떻게 되는지 알아보려면 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>


<span data-ttu-id="6ccbb-165">**소스 제어에 프로젝트 이외의 콘텐츠를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="6ccbb-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="6ccbb-166">(예: packages 폴더)를 추가 하려는 항목을 로컬 파일 시스템에 매핑된 폴더 내에서 적절 한 위치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="6ccbb-167">Visual Studio 2010에서에 **팀 탐색기** 창에서 팀 프로젝트를 확장 하 고 두 번 클릭 **소스 제어**입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="6ccbb-168">에 **소스 제어 탐색기** 탭의 **폴더** 창 선택 항목 또는 항목을 포함 된 폴더를 추가 하려면.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="6ccbb-169">클릭 합니다 **폴더에 항목 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="6ccbb-170">에 **소스 제어에 추가** 대화 상자에서 폴더 또는 항목을 추가 하 고 클릭 하려는 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="6ccbb-171">에 **항목을 제외** 탭에서 자동으로 제외 되었습니다 (예: 어셈블리)를 누른 다음 모든 필요한 항목을 선택 **항목을 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="6ccbb-172">에 **추가할 항목** 탭에서 확인 하 여 포함 하려는 모든 파일 나열 된 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="6ccbb-173">에 **소스 제어 탐색기** 창 클릭 합니다 **체크** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="6ccbb-174">에 **체크 인-소스 파일** 대화 상자에 설명을 입력 하 고 클릭 **체크**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="6ccbb-175">이 시점에서 소스 제어에 솔루션에 대 한 외부 종속성을 추가 했으므로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="6ccbb-176">결론</span><span class="sxs-lookup"><span data-stu-id="6ccbb-176">Conclusion</span></span>

<span data-ttu-id="6ccbb-177">이 항목에서는 팀 프로젝트에 연결 하 고 폴더 구조를 매핑할 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="6ccbb-178">소스 제어에서 항목을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [버전 제어를 사용 하 여](https://msdn.microsoft.com/library/ms181368.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="6ccbb-179">다음 항목인 [웹 배포용 TFS 빌드 서버를 구성](configuring-a-tfs-build-server-for-web-deployment.md)을 TFS 팀 빌드 서버에 솔루션을 빌드 및 배포를 준비 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="6ccbb-180">추가 정보</span><span class="sxs-lookup"><span data-stu-id="6ccbb-180">Further Reading</span></span>

<span data-ttu-id="6ccbb-181">TFS에서 소스 제어를 사용 하 여 작업에 대 한 자세한 내용은 참조 하세요. [버전 제어를 사용 하 여](https://msdn.microsoft.com/library/ms181368.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ccbb-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6ccbb-182">[이전](creating-a-team-project-in-tfs.md)
> [다음](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="6ccbb-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
