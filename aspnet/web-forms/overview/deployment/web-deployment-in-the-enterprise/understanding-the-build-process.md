---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: 빌드 프로세스를 이해 | Microsoft Docs
author: jrjlee
description: 이 항목의 엔터프라이즈급 빌드 및 배포 프로세스의 연습을 제공 합니다. 이 항목에서 설명 하는 방식은 사용자 지정 Microsoft 빌드 Engin 사용...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 4544a5e6212ea9b1247062dc35edc135ff7ca354
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30888002"
---
<a name="understanding-the-build-process"></a><span data-ttu-id="2acde-104">빌드 프로세스 이해</span><span class="sxs-lookup"><span data-stu-id="2acde-104">Understanding the Build Process</span></span>
====================
<span data-ttu-id="2acde-105">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="2acde-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="2acde-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="2acde-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="2acde-107">이 항목의 엔터프라이즈급 빌드 및 배포 프로세스의 연습을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-107">This topic provides a walkthrough of an enterprise-scale build and deployment process.</span></span> <span data-ttu-id="2acde-108">이 항목에서 설명 하는 방식은 Microsoft Build Engine (MSBuild) 프로젝트 파일 사용자 지정을 사용 하 여 프로세스의 모든 요소에 대해 세분화 된 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-108">The approach described in this topic uses custom Microsoft Build Engine (MSBuild) project files to provide fine-grained control over every aspect of the process.</span></span> <span data-ttu-id="2acde-109">프로젝트 파일 내에서 사용자 지정 MSBuild 대상은 인터넷 정보 서비스 (IIS) 웹 배포 도구 (MSDeploy.exe)와 같은 배포 유틸리티 및 VSDBCMD.exe 데이터베이스 배포 유틸리티를 실행 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-109">Within the project files, custom MSBuild targets are used to run deployment utilities like the Internet Information Services (IIS) Web Deployment Tool (MSDeploy.exe) and the database deployment utility VSDBCMD.exe.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="2acde-110">이전 항목 [프로젝트 파일 이해](understanding-the-project-file.md), MSBuild 프로젝트 파일의 주요 구성 요소를 설명 하 고 여러 대상 환경에 배포를 지원 하도록 분할 프로젝트 파일의 개념이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-110">The previous topic, [Understanding the Project File](understanding-the-project-file.md), described the key components of an MSBuild project file and introduced the concept of split project files to support deployment to multiple target environments.</span></span> <span data-ttu-id="2acde-111">검토 해야 모르겠으면 이미 이러한 개념을 이해, [프로젝트 파일 이해](understanding-the-project-file.md) 작업 수행 하기 전에이 항목을 통해.</span><span class="sxs-lookup"><span data-stu-id="2acde-111">If you're not already familiar with these concepts, you should review [Understanding the Project File](understanding-the-project-file.md) before you work through this topic.</span></span>


<span data-ttu-id="2acde-112">이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [Contact Manager 솔루션](the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="2acde-112">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="2acde-113">이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](understanding-the-project-file.md), 두 개의 프로젝트 파일에 빌드 프로세스에 의해 제어 되는&#x2014;포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="2acde-113">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="2acde-114">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-114">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="build-and-deployment-overview"></a><span data-ttu-id="2acde-115">빌드 및 배포 개요</span><span class="sxs-lookup"><span data-stu-id="2acde-115">Build and Deployment Overview</span></span>

<span data-ttu-id="2acde-116">에 [Contact Manager 솔루션](the-contact-manager-solution.md), 빌드 및 배포 프로세스를 제어 하는 세 개의 파일:</span><span class="sxs-lookup"><span data-stu-id="2acde-116">In the [Contact Manager solution](the-contact-manager-solution.md), three files control the build and deployment process:</span></span>

- <span data-ttu-id="2acde-117">A *유니버설 프로젝트 파일* (*Publish.proj*).</span><span class="sxs-lookup"><span data-stu-id="2acde-117">A *universal project file* (*Publish.proj*).</span></span> <span data-ttu-id="2acde-118">이 대상 환경 간에 변경 되지 않는 빌드 및 배포 지침을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-118">This contains build and deployment instructions that do not change between destination environments.</span></span>
- <span data-ttu-id="2acde-119">*환경별 프로젝트 파일* (*Env Dev.proj*).</span><span class="sxs-lookup"><span data-stu-id="2acde-119">An *environment-specific project file* (*Env-Dev.proj*).</span></span> <span data-ttu-id="2acde-120">이 특정 대상 환경에 고유한 빌드 및 배포 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-120">This contains build and deployment settings that are specific to a particular destination environment.</span></span> <span data-ttu-id="2acde-121">예를 들어, 사용할 수는 *Env Dev.proj* 개발자 또는 테스트 환경에 대 한 설정을 제공 하 고 라는 대체 파일을 만들고 파일을 *Env Stage.proj* 준비에 대 한 설정을 제공 하려면 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-121">For example, you could use the *Env-Dev.proj* file to provide settings for a developer or test environment and create an alternative file named *Env-Stage.proj* to provide settings for a staging environment.</span></span>
- <span data-ttu-id="2acde-122">A *명령 파일* (*게시 Dev.cmd*).</span><span class="sxs-lookup"><span data-stu-id="2acde-122">A *command file* (*Publish-Dev.cmd*).</span></span> <span data-ttu-id="2acde-123">이 프로젝트는이 파일을 지정 하는 명령을 실행 하려고 하는 MSBuild.exe 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-123">This contains an MSBuild.exe command that specifies which project files you want to execute.</span></span> <span data-ttu-id="2acde-124">각 파일 다양 한 환경 관련 프로젝트 파일을 지정 하는 MSBuild.exe 명령에 포함 된 모든 대상 환경에 대 한 명령에 대 한 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-124">You can create a command file for every destination environment, where each file contains an MSBuild.exe command that specifies a different environment-specific project file.</span></span> <span data-ttu-id="2acde-125">따라서 개발자를 적절 한 명령 파일을 실행 하 여 다른 환경에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-125">This lets the developer deploy to different environments simply by running the appropriate command file.</span></span>

<span data-ttu-id="2acde-126">샘플 솔루션에 게시 솔루션 폴더에 이러한 3 개의 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-126">In the sample solution, you can find these three files in the Publish solution folder.</span></span>

![](understanding-the-build-process/_static/image1.png)

<span data-ttu-id="2acde-127">이러한 파일을 보다 자세히 살펴보기 전에이 방법을 사용할 경우 전체 빌드 프로세스의 작동 방식을 살펴보겠습니다를 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-127">Before you look at these files in more detail, let's take a look at how the overall build process works when you use this approach.</span></span> <span data-ttu-id="2acde-128">상위 수준에서 빌드 및 배포 프로세스는 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-128">At a high level, the build and deployment process looks like this:</span></span>

![](understanding-the-build-process/_static/image2.png)

<span data-ttu-id="2acde-129">발생 하는 첫 번째 항목은 프로젝트 파일의 두&#x2014;유니버설 빌드 및 배포 지침이 포함 된 실행과 한 환경 관련 설정이 포함 된&#x2014;단일 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-129">The first thing that happens is that the two project files&#x2014;one containing universal build and deployment instructions, and one containing environment-specific settings&#x2014;are merged into a single project file.</span></span> <span data-ttu-id="2acde-130">다음 MSBuild 프로젝트 파일의 지침을 통해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-130">MSBuild then works through the instructions in the project file.</span></span> <span data-ttu-id="2acde-131">각 프로젝트 파일을 사용 하 여 각 프로젝트에 대 한 솔루션에 프로젝트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-131">It builds each of the projects in the solution, using the project file for each project.</span></span> <span data-ttu-id="2acde-132">그런 다음 Web Deploy (MSDeploy.exe)와 같은 다른 도구 및 대상 환경에 웹 콘텐츠 및 데이터베이스를 배포 하는 VSDBCMD 유틸리티 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-132">It then calls out to other tools, like Web Deploy (MSDeploy.exe) and the VSDBCMD utility to deploy your web content and databases to the target environment.</span></span>

<span data-ttu-id="2acde-133">처음부터 끝까지 빌드 및 배포 프로세스에서는 이러한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-133">From start to finish, the build and deployment process performs these tasks:</span></span>

1. <span data-ttu-id="2acde-134">새 빌드를 위한 준비를 출력 디렉터리의 내용을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-134">It deletes the contents of the output directory, in preparation for a fresh build.</span></span>
2. <span data-ttu-id="2acde-135">솔루션의 각 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-135">It builds each project in the solution:</span></span>

    1. <span data-ttu-id="2acde-136">웹 프로젝트에 대 한&#x2014;ASP.NET MVC 웹 응용 프로그램 및 WCF 웹 서비스에이 예에서&#x2014;빌드 프로세스는 각 프로젝트에 대해 웹 배포 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-136">For web projects&#x2014;in this case, an ASP.NET MVC web application and a WCF web service&#x2014;the build process creates a web deployment package for each project.</span></span>
    2. <span data-ttu-id="2acde-137">데이터베이스 프로젝트에 대 한 빌드 프로세스는 각 프로젝트에 대 한 배포 매니페스트 (.deploymanifest 파일)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-137">For database projects, the build process creates a deployment manifest (.deploymanifest file) for each project.</span></span>
3. <span data-ttu-id="2acde-138">VSDBCMD.exe 유틸리티를 사용 하 여 프로젝트 파일에서 다양 한 속성을 사용 하 여 솔루션의 각 데이터베이스 프로젝트를 배포 하려면&#x2014;대상 연결 문자열 및 데이터베이스 이름을&#x2014;.deploymanifest 파일과 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-138">It uses the VSDBCMD.exe utility to deploy each database project in the solution, using various properties from the project files&#x2014;a target connection string and a database name&#x2014;together with the .deploymanifest file.</span></span>
4. <span data-ttu-id="2acde-139">MSDeploy.exe 유틸리티를 사용 하 여 프로젝트 파일에서 다양 한 속성을 사용 하 여 배포 프로세스를 제어 하는 솔루션의 각 웹 프로젝트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-139">It uses the MSDeploy.exe utility to deploy each web project in the solution, using various properties from the project files to control the deployment process.</span></span>

<span data-ttu-id="2acde-140">이 과정을 자세히 추적 하는 샘플 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-140">You can use the sample solution to trace this process in more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="2acde-141">사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하십시오. [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-141">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


## <a name="invoking-the-build-and-deployment-process"></a><span data-ttu-id="2acde-142">빌드 및 배포 프로세스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-142">Invoking the Build and Deployment Process</span></span>

<span data-ttu-id="2acde-143">Contact Manager 솔루션 개발자 테스트 환경에 배포 하려면 개발자는 다음과 같이 실행 됩니다.는 *게시 Dev.cmd* 명령 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-143">To deploy the Contact Manager solution to a developer test environment, the developer runs the *Publish-Dev.cmd* command file.</span></span> <span data-ttu-id="2acde-144">MSBuild.exe를 호출 지정 *Publish.proj* 으로 프로젝트 파일을 실행 하 고 *Env Dev.proj* 매개 변수 값으로.</span><span class="sxs-lookup"><span data-stu-id="2acde-144">This invokes MSBuild.exe, specifying *Publish.proj* as the project file to execute and *Env-Dev.proj* as a parameter value.</span></span>


[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]


> [!NOTE]
> <span data-ttu-id="2acde-145">**/fl** 전환 (짧은 **/fileLogger**) 라는 파일에 빌드 출력을 기록 *msbuild.log* 현재 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-145">The **/fl** switch (short for **/fileLogger**) logs the build output to a file named *msbuild.log* in the current directory.</span></span> <span data-ttu-id="2acde-146">자세한 내용은 참조는 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-146">For more information, see the [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>


<span data-ttu-id="2acde-147">MSBuild의 실행을 시작, 로드이 시점에서 *Publish.proj* 파일 및 그 안에 지침을 처리 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-147">At this point, MSBuild starts running, loads the *Publish.proj* file, and starts processing the instructions within it.</span></span> <span data-ttu-id="2acde-148">첫 번째 명령 프로젝트 MSBuild 지시 파일을 **TargetEnvPropsFile** 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-148">The first instruction tells MSBuild to import the project file that the **TargetEnvPropsFile** parameter specifies.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]


<span data-ttu-id="2acde-149">**TargetEnvPropsFile** 매개 변수 지정는 *Env Dev.proj* 파일 이기 때문에 MSBuild의 내용을 병합 하는 *Env Dev.proj* 파일는  *Publish.proj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-149">The **TargetEnvPropsFile** parameter specifies the *Env-Dev.proj* file, so MSBuild merges the contents of the *Env-Dev.proj* file into the *Publish.proj* file.</span></span>

<span data-ttu-id="2acde-150">MSBuild에서 병합 된 프로젝트 파일에서 발생 하는 다음 요소는 속성 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-150">The next elements that MSBuild encounters in the merged project file are property groups.</span></span> <span data-ttu-id="2acde-151">속성은 파일에 나타나는 순서 대로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-151">Properties are processed in the order in which they appear in the file.</span></span> <span data-ttu-id="2acde-152">MSBuild는 지정 된 조건을 충족 제공 각 속성에 대 한 키-값 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-152">MSBuild creates a key-value pair for each property, providing that any specified conditions are met.</span></span> <span data-ttu-id="2acde-153">나중에 파일에 정의 된 속성 이름이 같은 파일에 앞에서 정의한 속성을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-153">Properties defined later in the file will overwrite any properties with the same name defined earlier in the file.</span></span> <span data-ttu-id="2acde-154">예를 들어는 **OutputRoot** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-154">For example, consider the **OutputRoot** properties.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]


<span data-ttu-id="2acde-155">MSBuild에서 첫 번째를 처리 하는 경우 **OutputRoot** 의 값을 설정, 요소를 유사한 이름의 매개 변수를 제공 합니다. 지정 하지 않았습니다 고 **OutputRoot** 속성을 **... \Publish\Out**합니다. 두 번째 발견 하면 **OutputRoot** 요소를 조건이 **true**의 값을 덮어쓰게 됩니다는 **OutputRoot** 속성의 값으로는 **OutDir** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-155">When MSBuild processes the first **OutputRoot** element, providing a similarly named parameter has not been provided, it sets the value of the **OutputRoot** property to **..\Publish\Out**. When it encounters the second **OutputRoot** element, if the condition evaluates to **true**, it will overwrite the value of the **OutputRoot** property with the value of the **OutDir** parameter.</span></span>

<span data-ttu-id="2acde-156">MSBuild에서 발생 하는 다음 요소 라는 항목이 포함 된 단일 항목 그룹은 **ProjectsToBuild**합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-156">The next element that MSBuild encounters is a single item group, containing an item named **ProjectsToBuild**.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]


<span data-ttu-id="2acde-157">MSBuild 항목 목록이 작성 하 여이 명령을 처리 **ProjectsToBuild**합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-157">MSBuild processes this instruction by building an item list named **ProjectsToBuild**.</span></span> <span data-ttu-id="2acde-158">이 경우 항목 목록에는 단일 값&#x2014;경로 솔루션 파일의 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-158">In this case, the item list contains a single value&#x2014;the path and filename of the solution file.</span></span>

<span data-ttu-id="2acde-159">이 시점에서 나머지 요소는 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-159">At this point, the remaining elements are targets.</span></span> <span data-ttu-id="2acde-160">대상 속성 및 항목에서 다르게 처리&#x2014;기본적으로, 대상으로 처리 되지 않습니다는 명시적으로 사용자가 지정한 또는 다른 구문이 프로젝트 파일 내에서 호출 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-160">Targets are processed differently from properties and items&#x2014;essentially, targets are not processed unless they are either explicitly specified by the user or invoked by another construct within the project file.</span></span> <span data-ttu-id="2acde-161">이전에 설명한 대로 열기 **프로젝트** 태그를 포함 한 **DefaultTargets** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-161">Recall that the opening **Project** tag includes a **DefaultTargets** attribute.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]


<span data-ttu-id="2acde-162">이렇게 하면 MSBuild를 호출 하는 **FullPublish** 대상, 대상이 MSBuild.exe가 호출 될 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-162">This instructs MSBuild to invoke the **FullPublish** target, if targets are not specified when MSBuild.exe is invoked.</span></span> <span data-ttu-id="2acde-163">**FullPublish** 대상에 작업이 없습니다; 대신 종속성 목록을 단순히 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-163">The **FullPublish** target doesn't contain any tasks; instead it simply specifies a list of dependencies.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]


<span data-ttu-id="2acde-164">이 종속성 지시 MSBuild 실행을 위해 해당는 **FullPublish** 이에서 대상이 목록을 제공 하는 순서를 호출 하는 데 필요한 대상:</span><span class="sxs-lookup"><span data-stu-id="2acde-164">This dependency tells MSBuild that in order to execute the **FullPublish** target, it needs to invoke this list of targets in the order provided:</span></span>

1. <span data-ttu-id="2acde-165">호출 해야는 **Clean** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-165">It must invoke the **Clean** target.</span></span>
2. <span data-ttu-id="2acde-166">호출 해야는 **BuildProjects** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-166">It must invoke the **BuildProjects** target.</span></span>
3. <span data-ttu-id="2acde-167">호출 해야는 **GatherPackagesForPublishing** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-167">It must invoke the **GatherPackagesForPublishing** target.</span></span>
4. <span data-ttu-id="2acde-168">호출 해야는 **PublishDbPackages** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-168">It must invoke the **PublishDbPackages** target.</span></span>
5. <span data-ttu-id="2acde-169">호출 해야는 **PublishWebPackages** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-169">It must invoke the **PublishWebPackages** target.</span></span>

### <a name="the-clean-target"></a><span data-ttu-id="2acde-170">Clean 대상</span><span class="sxs-lookup"><span data-stu-id="2acde-170">The Clean Target</span></span>

<span data-ttu-id="2acde-171">**Clean** 대상 기본적으로 삭제 출력 디렉터리 및 모든 내용이 새로 빌드에 대 한 준비 과정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-171">The **Clean** target basically deletes the output directory and all its contents, as preparation for a fresh build.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]


<span data-ttu-id="2acde-172">대상에 포함 된 통지는 **ItemGroup** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-172">Notice that the target includes an **ItemGroup** element.</span></span> <span data-ttu-id="2acde-173">속성 또는 내에서 항목을 정의 하는 경우는 **대상** 요소를 만드는 *동적* 속성 및 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-173">When you define properties or items within a **Target** element, you're creating *dynamic* properties and items.</span></span> <span data-ttu-id="2acde-174">즉, 속성 또는 항목 대상을 실행 될 때까지 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-174">In other words, the properties or items aren't processed until the target is executed.</span></span> <span data-ttu-id="2acde-175">출력 디렉터리 없거나 빌드할 수 있도록 빌드 프로세스가 시작 될 때까지 파일을 포함 하지 수는 **\_FilesToDelete** 정적 항목으로 나열; 실행이 진행 될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-175">The output directory might not exist or contain any files until the build process begins, so you can't build the **\_FilesToDelete** list as a static item; you have to wait until execution is underway.</span></span> <span data-ttu-id="2acde-176">이와 같이 대상에서 동적 항목으로 목록을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-176">As such, you build the list as a dynamic item within the target.</span></span>

> [!NOTE]
> <span data-ttu-id="2acde-177">이 경우 때문에 **Clean** 대상이 실행 될 첫 번째, 동적 항목 그룹을 사용 하려면 실제 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-177">In this case, because the **Clean** target is the first to be executed, there's no real need to use a dynamic item group.</span></span> <span data-ttu-id="2acde-178">그러나 이러한 유형의 시나리오에서는 동적 속성 및 항목을 사용 하 여 것이 좋습니다 이므로 특정 시점에 다른 순서로 대상을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-178">However, it's good practice to use dynamic properties and items in this type of scenario, as you might want to execute targets in a different order at some point.</span></span>  
> <span data-ttu-id="2acde-179">사용 하지 않을 항목을 선언 하지 않는 것 목표로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-179">You should also aim to avoid declaring items that will never be used.</span></span> <span data-ttu-id="2acde-180">특정 대상에만 사용 될 항목을 사용 하는 경우에 빌드 프로세스에서 불필요 한 오버 헤드를 제거 하려면 대상 내에 배치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-180">If you have items that will only be used by a specific target, consider placing them inside the target to remove any unnecessary overhead on the build process.</span></span>


<span data-ttu-id="2acde-181">항목을 제외 하 고, 동적은 **Clean** 대상은 매우 간단 하 고 기본 제공 활용 **메시지**, **삭제**, 및 **RemoveDir**작업:</span><span class="sxs-lookup"><span data-stu-id="2acde-181">Dynamic items aside, the **Clean** target is fairly straightforward and makes use of the built-in **Message**, **Delete**, and **RemoveDir** tasks to:</span></span>

1. <span data-ttu-id="2acde-182">로 거에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-182">Send a message to the logger.</span></span>
2. <span data-ttu-id="2acde-183">삭제할 파일의 목록을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-183">Build a list of files to delete.</span></span>
3. <span data-ttu-id="2acde-184">파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-184">Delete the files.</span></span>
4. <span data-ttu-id="2acde-185">출력 디렉터리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-185">Remove the output directory.</span></span>

### <a name="the-buildprojects-target"></a><span data-ttu-id="2acde-186">BuildProjects 대상</span><span class="sxs-lookup"><span data-stu-id="2acde-186">The BuildProjects Target</span></span>

<span data-ttu-id="2acde-187">**BuildProjects** 대상에는 기본적으로 샘플 솔루션의 모든 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-187">The **BuildProjects** target basically builds all the projects in the sample solution.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]


<span data-ttu-id="2acde-188">이 대상은 이전 항목에서 자세히 설명 된 [프로젝트 파일 이해](understanding-the-project-file.md), 작업 및 대상 속성 및 항목 참조 하는 방법을 설명 하기 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-188">This target was described in some detail in the previous topic, [Understanding the Project File](understanding-the-project-file.md), to illustrate how tasks and targets reference properties and items.</span></span> <span data-ttu-id="2acde-189">이 시점에서 주로에 관심이 **MSBuild** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-189">At this point, you're mainly interested in the **MSBuild** task.</span></span> <span data-ttu-id="2acde-190">여러 프로젝트를 빌드하기 위해이 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-190">You can use this task to build multiple projects.</span></span> <span data-ttu-id="2acde-191">작업은 MSBuild.exe;의 새 인스턴스를 만들지 않습니다. 현재 실행 중인 인스턴스를 사용 하 여 각 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-191">The task does not create a new instance of MSBuild.exe; it uses the current running instance to build each project.</span></span> <span data-ttu-id="2acde-192">이 예의 핵심 사항은 배포 속성:</span><span class="sxs-lookup"><span data-stu-id="2acde-192">The key points of interest in this example are the deployment properties:</span></span>

- <span data-ttu-id="2acde-193">**DeployOnBuild** 속성 각 프로젝트의 빌드 완료 되 면 프로젝트 설정의 모든 배포 지침을 실행 하기 위해 MSBuild에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-193">The **DeployOnBuild** property instructs MSBuild to run any deployment instructions in the project settings when the build of each project is complete.</span></span>
- <span data-ttu-id="2acde-194">**DeployTarget** 프로젝트가 빌드된 후 호출 하려는 대상 속성을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-194">The **DeployTarget** property identifies the target that you want to invoke after the project is built.</span></span> <span data-ttu-id="2acde-195">이 경우에 **패키지** 대상 웹 배포 가능한 패키지에 프로젝트 출력을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-195">In this case, the **Package** target builds the project output into a deployable web package.</span></span>

> [!NOTE]
> <span data-ttu-id="2acde-196">**패키지** 대상은 웹 게시 파이프라인 (WPP)을 MSBuild 및 웹 배포 간의 통합을 제공 하는 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-196">The **Package** target invokes the Web Publishing Pipeline (WPP), which provides integration between MSBuild and Web Deploy.</span></span> <span data-ttu-id="2acde-197">기본 제공 되는 대상을 WPP 제공 검토 확인 하려는 경우는 *Microsoft.Web.Publishing.targets* %PROGRAMFILES (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-197">If you want to take a look at the built-in targets that the WPP provides, review the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>


### <a name="the-gatherpackagesforpublishing-target"></a><span data-ttu-id="2acde-198">GatherPackagesForPublishing 대상</span><span class="sxs-lookup"><span data-stu-id="2acde-198">The GatherPackagesForPublishing Target</span></span>

<span data-ttu-id="2acde-199">검토 하는 경우는 **GatherPackagesForPublishing** 대상, 작업 실제로 포함 하지 않는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-199">If you study the **GatherPackagesForPublishing** target, you'll notice that it doesn't actually contain any tasks.</span></span> <span data-ttu-id="2acde-200">대신 동적 항목 3 개를 정의 하는 단일 항목 그룹을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-200">Instead, it contains a single item group that defines three dynamic items.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]


<span data-ttu-id="2acde-201">이러한 항목을 참조 될 때 생성 된 배포 패키지는 **BuildProjects** 대상이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-201">These items refer to the deployment packages that were created when the **BuildProjects** target was executed.</span></span> <span data-ttu-id="2acde-202">있습니다 수 없습니다.이 항목을 정의 이러한 정적으로 프로젝트 파일에까지 존재 하지 않으므로 항목 참조는 파일 때문에 **BuildProjects** 대상이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-202">You couldn't define these items statically in the project file, because the files to which the items refer don't exist until the **BuildProjects** target is executed.</span></span> <span data-ttu-id="2acde-203">대신, 항목 정의 해야 동적으로 될 때까지 호출 되지 않는 대상 내에서 후의 **BuildProjects** 대상이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-203">Instead, the items must be defined dynamically within a target that is not invoked until after the **BuildProjects** target is executed.</span></span>

<span data-ttu-id="2acde-204">이 대상 내의 항목 사용 되지 않는&#x2014;이 대상 단순히 항목 및 각 항목 값과 관련 된 메타 데이터를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-204">The items are not used within this target&#x2014;this target simply builds the items and the metadata associated with each item value.</span></span> <span data-ttu-id="2acde-205">이러한 요소를 처리 한 후의 **PublishPackages** 항목의 경로를 두 개의 값이 포함 됩니다는 *ContactManager.Mvc.deploy.cmd* 파일 및 경로를 *ContactManager.Service.deploy.cmd* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-205">Once these elements are processed, the **PublishPackages** item will contain two values, the path to the *ContactManager.Mvc.deploy.cmd* file and the path to the *ContactManager.Service.deploy.cmd* file.</span></span> <span data-ttu-id="2acde-206">이러한 파일은 호출 해야 하는 파일 및 웹 배포는 각 프로젝트에 대 한 웹 패키지의 일부로 이러한 파일을 만듭니다는 패키지를 배포 하기 위해 대상 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-206">Web Deploy creates these files as part of the web package for each project, and these are the files that you must invoke on the destination server in order to deploy the packages.</span></span> <span data-ttu-id="2acde-207">이러한 파일 중 하나를 열면 기본적으로 MSDeploy.exe 명령은 다양 한 빌드 관련 매개 변수 값으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-207">If you open up one of these files, you'll basically see an MSDeploy.exe command with various build-specific parameter values.</span></span>

<span data-ttu-id="2acde-208">**DbPublishPackages** 항목의 경로를 단일 값을 포함 됩니다는 *ContactManager.Database.deploymanifest* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-208">The **DbPublishPackages** item will contain a single value, the path to the *ContactManager.Database.deploymanifest* file.</span></span>

> [!NOTE]
> <span data-ttu-id="2acde-209">데이터베이스 프로젝트를 빌드하고 MSBuild 프로젝트 파일과 같은 스키마를 사용 하는 경우.deploymanifest 파일 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-209">A .deploymanifest file is generated when you build a database project, and it uses the same schema as an MSBuild project file.</span></span> <span data-ttu-id="2acde-210">데이터베이스 스키마 (.dbschema)의 위치 및 모든 배포 전 / 배포 후 스크립트의 세부 정보를 포함 하 여 데이터베이스를 배포 하는 데 필요한 모든 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-210">It contains all the information required to deploy a database, including the location of the database schema (.dbschema) and details of any pre-deployment and post-deployment scripts.</span></span> <span data-ttu-id="2acde-211">자세한 내용은 참조 [는 개요의 데이터베이스를 빌드하고 배포](https://msdn.microsoft.com/library/aa833165.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-211">For more information, see [An Overview of Database Build and Deployment](https://msdn.microsoft.com/library/aa833165.aspx).</span></span>


<span data-ttu-id="2acde-212">배포 패키지 및 데이터베이스 배포 매니페스트 생성 및 사용 방법을 자세히 알아봅니다 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md) 및 [데이터베이스 프로젝트 배포](deploying-database-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-212">You'll learn more about how deployment packages and database deployment manifests are created and used in [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md) and [Deploying Database Projects](deploying-database-projects.md).</span></span>

### <a name="the-publishdbpackages-target"></a><span data-ttu-id="2acde-213">PublishDbPackages 대상</span><span class="sxs-lookup"><span data-stu-id="2acde-213">The PublishDbPackages Target</span></span>

<span data-ttu-id="2acde-214">간단 하 게 말하면는 **PublishDbPackages** 대상은 VSDBCMD 유틸리티 배포를 호출 하는 **ContactManager** 대상 환경에는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-214">Briefly speaking, the **PublishDbPackages** target invokes the VSDBCMD utility to deploy the **ContactManager** database to a target environment.</span></span> <span data-ttu-id="2acde-215">다양 한 의사 결정 및 갖는, 데이터베이스 배포를 구성 하 고에서 여기에 대해 자세히 알아봅니다 [데이터베이스 프로젝트 배포](deploying-database-projects.md) 및 [여러환경에대한사용자지정데이터베이스배포](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).</span><span class="sxs-lookup"><span data-stu-id="2acde-215">Configuring database deployment involves lots of decisions and nuances, and you'll learn more about this in [Deploying Database Projects](deploying-database-projects.md) and [Customizing Database Deployments for Multiple Environments](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="2acde-216">이 항목에서는이 대상 실제로 작동 하는 방법을 집중적으로 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-216">In this topic, we'll focus on how this target actually functions.</span></span>

<span data-ttu-id="2acde-217">첫째, 여는 태그에 포함 되어 있는지 확인할 수는 **출력** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-217">First, notice that the opening tag includes an **Outputs** attribute.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]


<span data-ttu-id="2acde-218">한 예로이 *대상 일괄 처리*합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-218">This is an example of *target batching*.</span></span> <span data-ttu-id="2acde-219">MSBuild 프로젝트 파일의 일괄 처리는 컬렉션을 반복 하기 위한 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-219">In MSBuild project files, batching is a technique for iterating over collections.</span></span> <span data-ttu-id="2acde-220">값은 **출력** 특성 **"% (DbPublishPackages.Identity)"**, 참조 하는 **Identity** 의 메타 데이터 속성은 **DbPublishPackages** 항목 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-220">The value of the **Outputs** attribute, **"%(DbPublishPackages.Identity)"**, refers to the **Identity** metadata property of the **DbPublishPackages** item list.</span></span> <span data-ttu-id="2acde-221">이 표기 **Outputs=%***(ItemList.ItemMetadataName)*,으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-221">This notation, **Outputs=%***(ItemList.ItemMetadataName)*, is translated as:</span></span>

- <span data-ttu-id="2acde-222">에 있는 항목을 분할 **DbPublishPackages** 동일한 포함 된 항목의 일괄 처리로 **Identity** 메타 데이터 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-222">Split the items in **DbPublishPackages** into batches of items that contain the same **Identity** metadata value.</span></span>
- <span data-ttu-id="2acde-223">대상 일괄 처리에 한 번씩 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-223">Execute the target once per batch.</span></span>

> [!NOTE]
> <span data-ttu-id="2acde-224">**Identity** 중 하나는 [기본 제공 메타 데이터 값](https://msdn.microsoft.com/library/ms164313.aspx) 생성의 모든 항목에 할당 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-224">**Identity** is one of the [built-in metadata values](https://msdn.microsoft.com/library/ms164313.aspx) that is assigned to every item on creation.</span></span> <span data-ttu-id="2acde-225">값을 참조는 **Include** 특성에 **항목** 요소&#x2014;즉, 파일 경로 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-225">It refers to the value of the **Include** attribute in the **Item** element&#x2014;in other words, the path and filename of the item.</span></span>


<span data-ttu-id="2acde-226">이 경우 동일한 경로 및 파일 이름으로 둘 이상의 항목이 없어야, 때문에 기본적으로 최선을 다하고 하나의 일괄 처리 크기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-226">In this case, because there should never be more than one item with the same path and filename, we're essentially working with batch sizes of one.</span></span> <span data-ttu-id="2acde-227">대상 마다 데이터베이스 패키지를 한 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-227">The target is executed once for every database package.</span></span>

<span data-ttu-id="2acde-228">비슷한 표기법을 볼 수는 **\_Cmd** 속성을 적절 한 스위치도 VSDBCMD 명령을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-228">You can see a similar notation in the **\_Cmd** property, which builds a VSDBCMD command with the appropriate switches.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]


<span data-ttu-id="2acde-229">이 경우 **%(DbPublishPackages.DatabaseConnectionString)**, **%(DbPublishPackages.TargetDatabase)**, 및 **%(DbPublishPackages.FullPath)** 를 모두 참조 메타 데이터 값은 **DbPublishPackages** 항목 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-229">In this case, **%(DbPublishPackages.DatabaseConnectionString)**, **%(DbPublishPackages.TargetDatabase)**, and **%(DbPublishPackages.FullPath)** all refer to metadata values of the **DbPublishPackages** item collection.</span></span> <span data-ttu-id="2acde-230">**\_Cmd** 속성은 사용 된 **Exec** 명령을 호출 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-230">The **\_Cmd** property is used by the **Exec** task, which invokes the command.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]


<span data-ttu-id="2acde-231">이 표기법의 결과 **Exec** 작업 일괄 처리의 고유한 조합에 따라 만들어집니다는 **DatabaseConnectionString**, **TargetDatabase**, 및 **FullPath** 메타 데이터 값과 작업 각 일괄 처리에 대해 한 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-231">As a result of this notation, the **Exec** task will create batches based on unique combinations of the **DatabaseConnectionString**, **TargetDatabase**, and **FullPath** metadata values, and the task will execute once for each batch.</span></span> <span data-ttu-id="2acde-232">한 예로이 *작업 일괄 처리*합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-232">This is an example of *task batching*.</span></span> <span data-ttu-id="2acde-233">그러나 대상 수준 일괄 처리를 단일 항목 일괄 처리로 업체 항목 컬렉션 이미 나누 때문에 **Exec** 작업 대상의 각 반복에 대해 한 번만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-233">However, because the target-level batching has already divided our item collection into single-item batches, the **Exec** task will run once and only once for each iteration of the target.</span></span> <span data-ttu-id="2acde-234">즉,이 작업은 솔루션의 각 데이터베이스 패키지에 대해 한 번씩 VSDBCMD 유틸리티를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-234">In other words, this task invokes the VSDBCMD utility once for each database package in the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="2acde-235">MSBuild 대상 및 작업 일괄 처리에 대 한 자세한 내용은 참조 [일괄 처리가](https://msdn.microsoft.com/library/ms171473.aspx), [대상 일괄 처리의 항목 메타 데이터](https://msdn.microsoft.com/library/ms228229.aspx), 및 [작업 일괄 처리의 항목 메타 데이터](https://msdn.microsoft.com/library/ms171474.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-235">For more information on target and task batching, see MSBuild [Batching](https://msdn.microsoft.com/library/ms171473.aspx), [Item Metadata in Target Batching](https://msdn.microsoft.com/library/ms228229.aspx), and [Item Metadata in Task Batching](https://msdn.microsoft.com/library/ms171474.aspx).</span></span>


### <a name="the-publishwebpackages-target"></a><span data-ttu-id="2acde-236">PublishWebPackages 대상</span><span class="sxs-lookup"><span data-stu-id="2acde-236">The PublishWebPackages Target</span></span>

<span data-ttu-id="2acde-237">이 시점까지 호출한는 **BuildProjects** 샘플 솔루션의 각 프로젝트에 대해 웹 배포 패키지를 생성 하는 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-237">By this point, you've invoked the **BuildProjects** target, which generates a web deployment package for each project in the sample solution.</span></span> <span data-ttu-id="2acde-238">각 패키지와 함께 제공 되는 *deploy.cmd* 대상 환경에 패키지를 배포 하는 데 필요한 MSDeploy.exe 명령에 포함 하는 파일 및 *SetParameters.xml* 지정 하는 파일의 대상 환경의 세부 정보 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-238">Accompanying each package is a *deploy.cmd* file, which contains the MSDeploy.exe commands required to deploy the package to the target environment, and a *SetParameters.xml* file, which specifies the necessary details of the target environment.</span></span> <span data-ttu-id="2acde-239">또한 호출 되는 **GatherPackagesForPublishing** 포함 하는 항목 컬렉션에서 생성 하는 대상은 *deploy.cmd* 파일에 관심이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-239">You've also invoked the **GatherPackagesForPublishing** target, which generates an item collection containing the *deploy.cmd* files you're interested in.</span></span> <span data-ttu-id="2acde-240">기본적으로 **PublishWebPackages** 대상 이러한 기능을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-240">Essentially, the **PublishWebPackages** target performs these functions:</span></span>

- <span data-ttu-id="2acde-241">조작 하는 것은 *SetParameters.xml* 대상 환경에 대 한 올바른 정보를 포함 시킬 각 패키지에 대 한 파일 사용 하 여는 **XmlPoke** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-241">It manipulates the *SetParameters.xml* file for each package to include the correct details for the target environment, using the **XmlPoke** task.</span></span>
- <span data-ttu-id="2acde-242">호출 된 *deploy.cmd* 적절 한 스위치를 사용 하 여 각 패키지에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-242">It invokes the *deploy.cmd* file for each package, using the appropriate switches.</span></span>

<span data-ttu-id="2acde-243">마찬가지로 **PublishDbPackages** 대상에는 **PublishWebPackages** 대상을 사용 하 여 대상 일괄 처리 되도록 대상이 각 웹 패키지에 대해 한 번씩 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-243">Just like the **PublishDbPackages** target, the **PublishWebPackages** target uses target batching to ensure that the target is executed once for each web package.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]


<span data-ttu-id="2acde-244">대상 내에서 **Exec** 작업을 실행 하는 데 사용 됩니다는 *deploy.cmd* 각 웹 패키지에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-244">Within the target, the **Exec** task is used to run the *deploy.cmd* file for each web package.</span></span>


[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]


<span data-ttu-id="2acde-245">웹 패키지의 배포를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-245">For more information on configuring the deployment of web packages, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="2acde-246">결론</span><span class="sxs-lookup"><span data-stu-id="2acde-246">Conclusion</span></span>

<span data-ttu-id="2acde-247">이 항목 분할 프로젝트 파일 시작부터 완료 않아 샘플 솔루션에 대 한 빌드 및 배포 프로세스를 제어를 사용 하는 방법의 연습을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-247">This topic provided a walkthrough of how split project files are used to control the build and deployment process from start to finish for the Contact Manager sample solution.</span></span> <span data-ttu-id="2acde-248">이 방식을 사용 하 여 실행 하기 복잡을 하거나 반복 가능한를 단일 단계에서 엔터프라이즈 규모 배포 환경별 명령 파일을 실행 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-248">Using this approach lets you run complex, enterprise-scale deployments in a single, repeatable step, simply by running an environment-specific command file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="2acde-249">추가 정보</span><span class="sxs-lookup"><span data-stu-id="2acde-249">Further Reading</span></span>

<span data-ttu-id="2acde-250">프로젝트 파일 및 WPP에 대 한 자세한 소개를 참조 하십시오. [Microsoft Build Engine 안에: MSBuild를 사용 하 여 및 Team Foundation Build](http://amzn.com/0735645248) Sayed Ibrahim Hashimi 및 William Bartholomew, ISBN: 978-0-7356-4524-0입니다.</span><span class="sxs-lookup"><span data-stu-id="2acde-250">For a more in-depth introduction to project files and the WPP, see [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://amzn.com/0735645248) by Sayed Ibrahim Hashimi and William Bartholomew, ISBN: 978-0-7356-4524-0.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2acde-251">[이전](understanding-the-project-file.md)
> [다음](building-and-packaging-web-application-projects.md)</span><span class="sxs-lookup"><span data-stu-id="2acde-251">[Previous](understanding-the-project-file.md)
[Next](building-and-packaging-web-application-projects.md)</span></span>
