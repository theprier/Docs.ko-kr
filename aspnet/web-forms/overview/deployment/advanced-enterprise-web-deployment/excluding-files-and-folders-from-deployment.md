---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 배포에서 파일 및 폴더 제외 | Microsoft Docs
author: jrjlee
description: 이 설명 하는 방법에서 제외할 수 있습니다 파일 및 폴더 웹 배포 패키지를 빌드하고 웹 응용 프로그램 프로젝트를 패키지 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: c50352d423f41f84677dbf048e74088214340f3a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382584"
---
<a name="excluding-files-and-folders-from-deployment"></a><span data-ttu-id="aace7-103">배포에서 파일 및 폴더 제외</span><span class="sxs-lookup"><span data-stu-id="aace7-103">Excluding Files and Folders from Deployment</span></span>
====================
<span data-ttu-id="aace7-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="aace7-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="aace7-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="aace7-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="aace7-106">이 설명 하는 방법에서 제외할 수 있습니다 파일 및 폴더 웹 배포 패키지를 빌드하고 웹 응용 프로그램 프로젝트를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-106">This topic describes how you can exclude files and folders from a web deployment package when you build and package a web application project.</span></span>


<span data-ttu-id="aace7-107">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="aace7-108">이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="aace7-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="aace7-109">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="overview"></a><span data-ttu-id="aace7-110">개요</span><span class="sxs-lookup"><span data-stu-id="aace7-110">Overview</span></span>

<span data-ttu-id="aace7-111">Visual Studio 2010에서 웹 응용 프로그램 프로젝트를 빌드할 때 웹 게시 파이프라인 (WPP) 대 한 웹 배포 가능한 패키지로 컴파일된 웹 응용 프로그램 패키지를 빌드 프로세스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-111">When you build a web application project in Visual Studio 2010, the Web Publishing Pipeline (WPP) lets you extend this build process by packaging your compiled web application into a deployable web package.</span></span> <span data-ttu-id="aace7-112">원격 IIS 웹 서버에이 웹 패키지를 배포 하려면 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하거나 수동으로 IIS 관리자를 통해 웹 패키지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-112">You can then use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy this web package to a remote IIS web server, or import the web package manually through IIS Manager.</span></span> <span data-ttu-id="aace7-113">이 패키징 프로세스는 설명 [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-113">This packaging process is explained in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="aace7-114">그렇다면 어떻게 웹에 포함 된 항목을 가져옵니다 제어 하려면 패키지?</span><span class="sxs-lookup"><span data-stu-id="aace7-114">So how do you control what gets included in your web package?</span></span> <span data-ttu-id="aace7-115">많은 시나리오에 대 한 충분 한 제어를 제공 하는 기본 프로젝트 파일을 통해 Visual Studio에서 프로젝트 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-115">The project settings in Visual Studio, through the underlying project file, provide sufficient control for a lot of scenarios.</span></span> <span data-ttu-id="aace7-116">그러나 일부 경우 특정 대상 환경에 웹 패키지의 콘텐츠를 조정 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-116">However, in some cases you may want to tailor the contents of your web package to specific destination environments.</span></span> <span data-ttu-id="aace7-117">예를 들어, 다음 응용 프로그램 테스트 환경에 배포 해도 스테이징 또는 프로덕션 환경에 응용 프로그램을 배포 하는 경우 폴더를 제외 하는 경우 로그 파일에 대 한 폴더를 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-117">For example, you might want to include a folder for log files when you deploy your application to a test environment but exclude the folder when you deploy the application to a staging or production environment.</span></span> <span data-ttu-id="aace7-118">이 항목에서는이 작업을 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-118">This topic will show you how to do this.</span></span>

## <a name="what-gets-included-by-default"></a><span data-ttu-id="aace7-119">기본적으로 포함 가져옵니다 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="aace7-119">What Gets Included by Default?</span></span>

<span data-ttu-id="aace7-120">Visual Studio에서 웹 응용 프로그램 프로젝트 속성을 구성한 경우는 **배포할 항목** 목록에 **웹 패키지 및 게시** 페이지에서는 웹 배포에 포함 하도록 지정할 수 있습니다 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-120">When you configure your web application project properties in Visual Studio, the **Items to deploy** list on the **Package/Publish Web** page lets you specify what you want to include in your web deployment package.</span></span> <span data-ttu-id="aace7-121">기본적으로이 설정은 **이 응용 프로그램을 실행 하는 데 필요한 파일만**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-121">By default, this is set to **Only files needed to run this application**.</span></span>

![](excluding-files-and-folders-from-deployment/_static/image1.png)

<span data-ttu-id="aace7-122">선택 하는 경우 **이 응용 프로그램을 실행 하는 데 필요한 파일만**, WPP 웹 패키지에 추가할 파일을 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-122">When you choose **Only files needed to run this application**, the WPP will try to determine which files should be added to the web package.</span></span> <span data-ttu-id="aace7-123">여기에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-123">This includes:</span></span>

- <span data-ttu-id="aace7-124">프로젝트에 대 한 모든 빌드 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-124">All the build outputs for the project.</span></span>
- <span data-ttu-id="aace7-125">빌드 작업을 사용 하 여 모든 파일 표시 **콘텐츠**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-125">Any files marked with a build action of **Content**.</span></span>

> [!NOTE]
> <span data-ttu-id="aace7-126">포함할 파일을 결정 하는 논리는이 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-126">The logic that determines which files to include is contained in this file:</span></span>   
> <span data-ttu-id="aace7-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span><span class="sxs-lookup"><span data-stu-id="aace7-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span></span>


## <a name="excluding-specific-files-and-folders"></a><span data-ttu-id="aace7-128">특정 파일 및 폴더 제외</span><span class="sxs-lookup"><span data-stu-id="aace7-128">Excluding Specific Files and Folders</span></span>

<span data-ttu-id="aace7-129">일부 경우에는 파일 및 폴더는 배포 보다 세부적으로 제어를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-129">In some cases, you'll want more fine-grained control over which files and folders are deployed.</span></span> <span data-ttu-id="aace7-130">앞 제외 하려는 파일 시간을 알고 있고 제외를 모든 대상 환경에 적용 됩니다, 설정 하기만 하면 됩니다 합니다 **빌드 작업** 각 파일의 **None**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-130">If you know which files you want to exclude ahead of time, and the exclusion applies to all destination environments, you can simply set the **Build Action** of each file to **None**.</span></span>

<span data-ttu-id="aace7-131">**배포에서 특정 파일을 제외 하려면**</span><span class="sxs-lookup"><span data-stu-id="aace7-131">**To exclude specific files from deployment**</span></span>

1. <span data-ttu-id="aace7-132">에 **솔루션 탐색기** 창에서 파일을 마우스 오른쪽 단추로 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-132">In the **Solution Explorer** window, right-click the file, and then click **Properties**.</span></span>
2. <span data-ttu-id="aace7-133">에 **속성** 창에서를 **빌드 작업** 행을 선택 **None**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-133">In the **Properties** window, in the **Build Action** row, select **None**.</span></span>

<span data-ttu-id="aace7-134">그러나이 방법은 항상 편리한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-134">However, this approach is not always convenient.</span></span> <span data-ttu-id="aace7-135">예를 들어 파일을 변경 하는 것이 좋습니다 및 폴더는 대상 환경에 따라 Visual Studio 외부에서 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-135">For example, you may want to vary which files and folders are included according to your destination environment, and from outside Visual Studio.</span></span> <span data-ttu-id="aace7-136">예를 들어 Contact Manager 샘플 솔루션에서 ContactManager.Mvc 프로젝트의 내용 살펴봅니다를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-136">For example, in the Contact Manager sample solution, take a look at the contents of the ContactManager.Mvc project:</span></span>

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- <span data-ttu-id="aace7-137">내부 폴더 만들기, 삭제 및 개발을 위해 로컬 데이터베이스를 채우는 데 사용 하는 개발자는 몇 가지 SQL 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-137">The Internal folder contains some SQL scripts that the developer uses to create, drop, and populate local databases for development purposes.</span></span> <span data-ttu-id="aace7-138">이 폴더의 경우 nothing 스테이징 또는 프로덕션 환경에 배포 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-138">Nothing in this folder should be deployed to a staging or production environment.</span></span>
- <span data-ttu-id="aace7-139">스크립트 폴더에는 몇 가지 JavaScript 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-139">The Scripts folder contains several JavaScript files.</span></span> <span data-ttu-id="aace7-140">이러한 파일이 많이 디버깅을 지원 하거나 Visual Studio에서 IntelliSense 제공 순수 하 게 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-140">A lot of these files are included purely to support debugging or provide IntelliSense in Visual Studio.</span></span> <span data-ttu-id="aace7-141">이러한 파일 중 일부를 스테이징 또는 프로덕션 환경에 배포 하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-141">Some of these files should not be deployed to staging or production environments.</span></span> <span data-ttu-id="aace7-142">그러나 다음 문제 해결 용이 하 게 하는 개발자 테스트 환경에 배포 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-142">However, you may want to deploy them to a developer test environment to facilitate troubleshooting.</span></span>

<span data-ttu-id="aace7-143">특정 파일 및 폴더 제외 하려면 프로젝트 파일을 조작할 수 있습니다, 있지만 쉬운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-143">Although you could manipulate your project files to exclude specific files and folders, there is an easier way.</span></span> <span data-ttu-id="aace7-144">WPP 라는 항목 목록을 작성 하 여 파일 및 폴더를 제외 하는 메커니즘을 포함 **ExcludeFromPackageFolders** 하 고 **ExcludeFromPackageFiles**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-144">The WPP includes a mechanism to exclude files and folders by building item lists named **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles**.</span></span> <span data-ttu-id="aace7-145">이러한 목록에 고유한 항목을 추가 하 여이 메커니즘을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-145">You can extend this mechanism by adding your own items to these lists.</span></span> <span data-ttu-id="aace7-146">이렇게 하려면 다음 대략적인 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-146">To do this, you need to complete these high-level steps:</span></span>

1. <span data-ttu-id="aace7-147">라는 사용자 지정 프로젝트 파일을 만듭니다 *[프로젝트 이름].wpp.targets* 프로젝트 파일과 동일한 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-147">Create a custom project file named *[project name].wpp.targets* in the same folder as your project file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aace7-148">합니다 *. wpp.targets* 파일을 웹 응용 프로그램 프로젝트 파일과 동일한 폴더에 이동 해야&#x2014;예를 들어 *ContactManager.Mvc.csproj*&#x2014;아닌 같은 사용자 지정 폴더 프로젝트 파일을 사용 하면 빌드 및 배포 프로세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-148">The *.wpp.targets* file needs to go in the same folder as your web application project file&#x2014;for example, *ContactManager.Mvc.csproj*&#x2014;rather than in the same folder as any custom project files you use to control the build and deployment process.</span></span>
2. <span data-ttu-id="aace7-149">에 *. wpp.targets* 파일을 추가 **ItemGroup** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-149">In the *.wpp.targets* file, add an **ItemGroup** element.</span></span>
3. <span data-ttu-id="aace7-150">에 **ItemGroup** 요소를 추가 **ExcludeFromPackageFolders** 하 고 **ExcludeFromPackageFiles** 특정 파일 및 필요에 따라 폴더를 제외할 항목을 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-150">In the **ItemGroup** element, add **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles** items to exclude specific files and folders as required.</span></span>

<span data-ttu-id="aace7-151">이 기본 구조가 *. wpp.targets* 파일:</span><span class="sxs-lookup"><span data-stu-id="aace7-151">This is the basic structure of this *.wpp.targets* file:</span></span>


[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]


<span data-ttu-id="aace7-152">각 항목 라는 항목 메타 데이터 요소를 포함 하는 참고 **FromTarget**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-152">Note that each item includes an item metadata element named **FromTarget**.</span></span> <span data-ttu-id="aace7-153">이 값은 빌드 프로세스를 영향을 주지는 선택적 값 단순히 특정 파일 또는 폴더 생략 된 이유를 나타내는 데 사용 되 빌드 로그를 검토 하는 사용자가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="aace7-153">This is an optional value that doesn't affect the build process; it simply serves to indicate why particular files or folders were omitted if someone reviews the build logs.</span></span>

## <a name="excluding-files-and-folders-from-a-web-package"></a><span data-ttu-id="aace7-154">웹 패키지에서 파일 및 폴더 제외</span><span class="sxs-lookup"><span data-stu-id="aace7-154">Excluding Files and Folders from a Web Package</span></span>

<span data-ttu-id="aace7-155">다음 절차는 추가 하는 방법을 보여 줍니다.는 *. wpp.targets* 파일 웹 응용 프로그램 프로젝트 및 파일을 사용 하 여 프로젝트를 빌드할 때 웹 패키지에서 특정 파일 및 폴더를 제외 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-155">The next procedure shows you how to add a *.wpp.targets* file to a web application project and how to use the file to exclude specific files and folders from the web package when you build your project.</span></span>

<span data-ttu-id="aace7-156">**웹 배포 패키지에서 파일 및 폴더를 제외 하려면**</span><span class="sxs-lookup"><span data-stu-id="aace7-156">**To exclude files and folders from a web deployment package**</span></span>

1. <span data-ttu-id="aace7-157">Visual Studio 2010에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-157">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="aace7-158">에 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **ContactManager.Mvc**), 가리킵니다 **추가**, 클릭하고**새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-158">In the **Solution Explorer** window, right-click your web application project node (for example, **ContactManager.Mvc**), point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="aace7-159">에 **새 항목 추가** 대화 상자를 선택 합니다 **XML 파일** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="aace7-159">In the **Add New Item** dialog box, select the **XML File** template.</span></span>
4. <span data-ttu-id="aace7-160">에 **이름** 상자에 입력 *[프로젝트 이름] * * *.wpp.targets** (예를 들어 **ContactManager.Mvc.wpp.targets**)를 클릭 하 고 **추가**.</span><span class="sxs-lookup"><span data-stu-id="aace7-160">In the **Name** box, type *[project name]***.wpp.targets** (for example, **ContactManager.Mvc.wpp.targets**), and then click **Add**.</span></span>

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="aace7-161">새 항목을 프로젝트의 루트 노드로 추가 하는 경우 파일은 프로젝트 파일과 동일한 폴더에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-161">If you add a new item to the root node of a project, the file is created in the same folder as the project file.</span></span> <span data-ttu-id="aace7-162">Windows 탐색기에서 폴더를 열어이 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-162">You can verify this by opening the folder in Windows Explorer.</span></span>
5. <span data-ttu-id="aace7-163">파일에 추가 된 **프로젝트** 요소와 **ItemGroup** 요소:</span><span class="sxs-lookup"><span data-stu-id="aace7-163">In the file, add a **Project** element and an **ItemGroup** element:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. <span data-ttu-id="aace7-164">웹 패키지에서 폴더를 제외 하려는 경우 추가 된 **ExcludeFromPackageFolders** 요소를 **ItemGroup** 요소:</span><span class="sxs-lookup"><span data-stu-id="aace7-164">If you want to exclude folders from the web package, add an **ExcludeFromPackageFolders** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="aace7-165">에 **Include** 특성을 제외 하려는 폴더의 세미콜론으로 구분 된 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-165">In the **Include** attribute, provide a semicolon-separated list of the folders you want to exclude.</span></span>
   2. <span data-ttu-id="aace7-166">에 **FromTarget** 메타 데이터 요소를 의미 있는 이름와 같은 폴더 되 제외 이유를 나타내는 값을 제공 합니다 *. wpp.targets* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-166">In the **FromTarget** metadata element, provide a meaningful value to indicate why the folders are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. <span data-ttu-id="aace7-167">웹 패키지에서 파일을 제외 하려는 경우 추가 된 **ExcludeFromPackageFiles** 요소를 **ItemGroup** 요소:</span><span class="sxs-lookup"><span data-stu-id="aace7-167">If you want to exclude files from the web package, add an **ExcludeFromPackageFiles** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="aace7-168">에 **Include** 특성을 제외 하려는 파일의 세미콜론으로 구분 된 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-168">In the **Include** attribute, provide a semicolon-separated list of the files you want to exclude.</span></span>
   2. <span data-ttu-id="aace7-169">에 **FromTarget** 메타 데이터 요소를 의미 있는 이름와 같은 파일 되 제외 이유를 나타내는 값을 제공 합니다 *. wpp.targets* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-169">In the **FromTarget** metadata element, provide a meaningful value to indicate why the files are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. <span data-ttu-id="aace7-170">합니다 *[프로젝트 이름].wpp.targets* 파일 이제는 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-170">The *[project name].wpp.targets* file should now resemble this:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. <span data-ttu-id="aace7-171">저장 후 닫기 합니다 *[프로젝트 이름].wpp.targets* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-171">Save and close the *[project name].wpp.targets* file.</span></span>

<span data-ttu-id="aace7-172">다음에 웹 응용 프로그램 프로젝트 빌드 및 패키지 있습니다, WPP가 자동으로 감지 합니다 *. wpp.targets* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-172">The next time you build and package your web application project, the WPP will automatically detect the *.wpp.targets* file.</span></span> <span data-ttu-id="aace7-173">모든 파일 및 폴더를 지정한 웹 패키지에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-173">Any files and folders you specified will not be included in the web package.</span></span>

## <a name="conclusion"></a><span data-ttu-id="aace7-174">결론</span><span class="sxs-lookup"><span data-stu-id="aace7-174">Conclusion</span></span>

<span data-ttu-id="aace7-175">이 항목에서는 사용자 지정을 만들어 웹 패키지를 빌드할 때 특정 파일 및 폴더를 제외 하는 방법 설명 *. wpp.targets* 웹 응용 프로그램 프로젝트 파일과 동일한 폴더에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-175">This topic described how to exclude specific files and folders when you build a web package, by creating a custom *.wpp.targets* file in the same folder as your web application project file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="aace7-176">추가 정보</span><span class="sxs-lookup"><span data-stu-id="aace7-176">Further Reading</span></span>

<span data-ttu-id="aace7-177">사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하에 대 한 자세한 내용은 참조 하세요. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-177">For more information on using custom Microsoft Build Engine (MSBuild) project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="aace7-178">패키징 및 배포 프로세스에 대 한 자세한 내용은 참조 하세요. [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)하십시오 [웹 패키지 배포용 매개 변수 구성](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), 및 [ 웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aace7-178">For more information on the packaging and deployment process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Configuring Parameters for Web Package Deployment](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), and [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aace7-179">[이전](deploying-membership-databases-to-enterprise-environments.md)
> [다음](taking-web-applications-offline-with-web-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="aace7-179">[Previous](deploying-membership-databases-to-enterprise-environments.md)
[Next](taking-web-applications-offline-with-web-deploy.md)</span></span>
