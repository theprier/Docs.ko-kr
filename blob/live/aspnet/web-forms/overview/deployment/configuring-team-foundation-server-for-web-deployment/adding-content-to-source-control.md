---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: "소스 제어에 콘텐츠 추가 | Microsoft Docs"
author: jrjlee
description: "이 Team Foundation Server (TFS) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다. 팀 proje에 솔루션 및 프로젝트를 추가 하는 방법을 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: a6a90a03674cfe7565da0ed56148186ee9525707
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adding-content-to-source-control"></a><span data-ttu-id="c5f73-104">소스 제어에 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="c5f73-104">Adding Content to Source Control</span></span>
====================
<span data-ttu-id="c5f73-105">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c5f73-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c5f73-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="c5f73-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c5f73-107">이 Team Foundation Server (TFS) 2010에서 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="c5f73-108">TFS의 팀 프로젝트에 솔루션 및 프로젝트를 추가 하는 방법을 설명 하 고 소스 제어에 프레임 워크 또는 어셈블리와 같은 외부 종속성을 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>


<span data-ttu-id="c5f73-109">이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="c5f73-110">작업 개요</span><span class="sxs-lookup"><span data-stu-id="c5f73-110">Task Overview</span></span>

<span data-ttu-id="c5f73-111">대부분의 경우에서 개발자 팀의 모든 멤버는 소스 제어에 콘텐츠를 추가 할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="c5f73-112">TFS에서 소스 제어에 솔루션을 추가 하려면 같은 대략적인 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="c5f73-113">팀 프로젝트에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-113">Connect to a team project.</span></span>
- <span data-ttu-id="c5f73-114">로컬 컴퓨터의 폴더 구조를 서버에서 팀 프로젝트 폴더 구조를 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="c5f73-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="c5f73-115">소스 제어에 솔루션 및 해당 내용을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="c5f73-116">소스 제어에는 외부 종속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="c5f73-117">이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="c5f73-118">작업은이 항목의 연습에서는 콘텐츠를 관리할 새 TFS 팀 프로젝트를 이미 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="c5f73-119">새 팀 프로젝트를 만드는 방법에 대 한 자세한 내용은 참조 하십시오. [TFS에서 팀 프로젝트를 만드는](creating-a-team-project-in-tfs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="c5f73-120">이러한 절차를 수행 하는 사람?</span><span class="sxs-lookup"><span data-stu-id="c5f73-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="c5f73-121">대부분의 경우에서 개발자 팀의 모든 멤버를 추가 및 특정 팀 프로젝트 내에서 콘텐츠를 수정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="c5f73-122">팀 프로젝트에 연결 하 고 폴더 매핑 만들기</span><span class="sxs-lookup"><span data-stu-id="c5f73-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="c5f73-123">소스 제어에 콘텐츠를 추가 하기 전에 팀 프로젝트에 연결 하 고 로컬 컴퓨터의 서버에서 폴더 구조 및 파일 시스템 간에 매핑을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="c5f73-124">**로컬 경로 매핑한 팀 프로젝트에 연결 하려면**</span><span class="sxs-lookup"><span data-stu-id="c5f73-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="c5f73-125">개발자 워크스테이션에서 Visual Studio 2010을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="c5f73-126">Visual Studio에서에 **팀** 메뉴를 클릭 하 여 **Team Foundation Server에 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c5f73-127">TFS 서버에 대 한 연결을 이미 구성 했다면 3-6 단계를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="c5f73-128">에 **팀 프로젝트에 연결** 대화 상자를 클릭 **서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="c5f73-129">에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="c5f73-130">에 **Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="c5f73-131">에 **Team Foundation Server 추가/제거** 대화 상자를 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="c5f73-132">에 **팀 프로젝트에 연결** 대화 상자에서 팀 선택에 연결 하려면 TFS 인스턴스 선택 프로젝트 컬렉션에 추가 하려는 팀 프로젝트를 선택 하 고 클릭 한 다음 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="c5f73-133">에 **팀 탐색기** 창, 팀 프로젝트를 확장 하 고 두 번 클릭 **소스 제어**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="c5f73-134">에 **소스 제어 탐색기** 탭을 클릭 **매핑되지**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="c5f73-135">에 **지도** 대화 상자는 **로컬 폴더** 상자, 찾은 (만들거나) 역할을 팀 프로젝트에 대 한 루트 폴더를 클릭 한 다음 로컬 폴더 **지도**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="c5f73-136">소스 파일을 다운로드 하도록 메시지가 면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="c5f73-137">이 시점에서 팀 프로젝트에 대 한 서버 쪽 폴더 개발자 워크스테이션의 로컬 폴더에 매핑 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="c5f73-138">또한 팀 프로젝트에서 기존 내용을 로컬 폴더 구조에 다운로드 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="c5f73-139">소스 제어에 내용을 직접 추가를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="c5f73-140">소스 제어에 프로젝트와 솔루션 추가</span><span class="sxs-lookup"><span data-stu-id="c5f73-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="c5f73-141">프로젝트 및 솔루션 소스 제어에 추가 하려면 먼저 로컬 컴퓨터에서 매핑된 팀 프로젝트에 대 한 폴더로 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="c5f73-142">다음에 서버와 동기화 할 콘텐츠에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="c5f73-143">**소스 제어에 프로젝트를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="c5f73-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="c5f73-144">개발자 워크스테이션에서 팀 프로젝트에 매핑된 폴더 구조 내에서 적절 한 위치 프로젝트 및 솔루션을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c5f73-145">대부분의 조직에서는 소스 제어에서 프로젝트 및 솔루션을 구성 하는 방법을 대 한 기본 액세스를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="c5f73-146">폴더를 구조화 하는 방법에 대 한 지침을 참조 하십시오. [How To: Team Foundation Server에서 구조 Your 소스 제어 폴더](https://msdn.microsoft.com/en-us/library/bb668992.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/en-us/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="c5f73-147">Visual Studio 2010에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="c5f73-148">에 **솔루션 탐색기** 창 솔루션을 마우스 오른쪽 단추로 클릭 **소스 제어에 솔루션 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="c5f73-149">TFS의 구조 콘텐츠를 조직 선호 하는 방법에 따라 소스 코드의 구성 하는 방법을 보다 세부적으로 제어를 제공 하는 개별적으로 소스 제어에 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="c5f73-150">확인 하는 **소스 제어 탐색기** 추가할 팀 프로젝트에 대 한 서버 폴더 구조 내에서 콘텐츠 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="c5f73-151">**소스 제어 탐색기** 더 이상 로컬 파일 시스템에 매핑된 폴더에 솔루션을 추가 하기 때문에 메시지를 표시 하는 사용 하 여 콘텐츠 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="c5f73-152">솔루션을 매핑되지 않은 위치에 있는 경우에서 TFS 및 로컬 파일 시스템 폴더 위치를 지정 하 라는 메시지가 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="c5f73-153">에 **소스 제어 탐색기** 탭에 **폴더** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭 (예를 들어 **ContactManager**)를 클릭 하 고 **체크 인 보류 중인 변경 내용을**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="c5f73-154">에 **체크 인-소스 파일** 대화 상자에 설명을 입력 하 고 클릭 **체크 인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="c5f73-155">이 시점에서 TFS의 소스 제어에 솔루션을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="c5f73-156">소스 제어에 외부 종속성 추가</span><span class="sxs-lookup"><span data-stu-id="c5f73-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="c5f73-157">소스 제어에 프로젝트 또는 솔루션을 추가 하는 경우 모든 파일 및 폴더를 프로젝트 또는 솔루션 내에서 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="c5f73-158">그러나 대부분의 경우에서 프로젝트 및 솔루션에 의존할 수 제대로 작동 하려면 로컬 어셈블리와 같은 외부 종속성.</span><span class="sxs-lookup"><span data-stu-id="c5f73-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="c5f73-159">코드를 성공적으로 빌드 팀 빌드 및 개발자 팀의 다른 멤버 수 있도록 소스 제어에 이러한 리소스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="c5f73-160">예를 들어 않아 샘플 솔루션에 대 한 폴더 구조에는 패키지 라는 폴더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="c5f73-161">ADO.NET Entity Framework 4.1에 대 한 어셈블리 및 다양 한 지원 리소스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="c5f73-162">패키지 폴더 Contact Manager 솔루션의 일부가 아닙니다. 하지만 솔루션 없이 성공적으로 빌드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="c5f73-163">팀이 솔루션을 빌드하려면 빌드를 사용 하도록 설정 하려면 소스 제어에 패키지 폴더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="c5f73-164">패키지 폴더의 포함 여부는 Visual Studio 2010 용 NuGet 확장을 사용 하 여 솔루션에는 Entity Framework 또는 유사한 리소스를 추가 하면 어떤 일이 생기의 전형입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>


<span data-ttu-id="c5f73-165">**소스 제어에 프로젝트 이외의 콘텐츠를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="c5f73-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="c5f73-166">(예: 패키지 폴더) 항목을 추가 로컬 파일 시스템에 매핑된 폴더 내에서 적절 한 위치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="c5f73-167">Visual Studio 2010에서에 **팀 탐색기** 창, 팀 프로젝트를 확장 하 고 두 번 클릭 **소스 제어**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="c5f73-168">에 **소스 제어 탐색기** 탭에 **폴더** 창에서 항목 또는 항목을 포함 하는 폴더를 추가 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="c5f73-169">클릭는 **폴더에 항목 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="c5f73-170">에 **소스 제어에 추가** 대화 상자에서 폴더 또는 항목을 추가 하 고, 클릭 한 다음 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="c5f73-171">에 **항목 제외** 탭에서 자동으로 제외 되었습니다 (예: 어셈블리)을 클릭 한 다음 필요한 항목을 선택 **항목 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="c5f73-172">에 **추가할 항목을** 탭에서 포함 하려는 모든 파일 나열 되 고 클릭 한 다음 확인 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="c5f73-173">에 **소스 제어 탐색기** 창 클릭는 **체크 인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="c5f73-174">에 **체크 인-소스 파일** 대화 상자에 설명을 입력 하 고 클릭 **체크 인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="c5f73-175">이 시점에서 소스 제어에 솔루션에 대 한 외부 종속성을 추가 했으므로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c5f73-176">결론</span><span class="sxs-lookup"><span data-stu-id="c5f73-176">Conclusion</span></span>

<span data-ttu-id="c5f73-177">이 항목에는 팀 프로젝트에 연결 하 고 폴더 구조를 매핑할 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="c5f73-178">소스 제어에서 항목을 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [버전 제어를 사용 하 여](https://msdn.microsoft.com/en-us/library/ms181368.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/en-us/library/ms181368.aspx).</span></span>

<span data-ttu-id="c5f73-179">다음 항목인 [웹 배포를 위한 TFS 빌드 서버 구성](configuring-a-tfs-build-server-for-web-deployment.md), 빌드 및 솔루션 배포를 TFS 팀 빌드 서버를 준비 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="c5f73-180">추가 정보</span><span class="sxs-lookup"><span data-stu-id="c5f73-180">Further Reading</span></span>

<span data-ttu-id="c5f73-181">TFS에서 소스 제어를 사용한 작업에 대 한 자세한 내용은 참조 하십시오. [버전 제어를 사용 하 여](https://msdn.microsoft.com/en-us/library/ms181368.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f73-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/en-us/library/ms181368.aspx).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c5f73-182">[이전](creating-a-team-project-in-tfs.md)
[다음](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="c5f73-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
