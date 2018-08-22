---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 패키징 프로세스 문제 해결 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 M EnablePackageProcessLoggingAndAssert 속성을 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법 설명 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 22be1ccc5a1ec52d143bedffd79264918c1a45e1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829905"
---
<a name="troubleshooting-the-packaging-process"></a><span data-ttu-id="b3062-103">패키징 프로세스 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b3062-103">Troubleshooting the Packaging Process</span></span>
====================
<span data-ttu-id="b3062-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="b3062-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="b3062-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="b3062-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="b3062-106">이 항목에서는 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법에 대해 설명 합니다 **EnablePackageProcessLoggingAndAssert** Microsoft Build Engine (MSBuild)의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-106">This topic describes how you can collect detailed information about the packaging process by using the **EnablePackageProcessLoggingAndAssert** property in the Microsoft Build Engine (MSBuild).</span></span>
> 
> <span data-ttu-id="b3062-107">설정한 경우 합니다 **EnablePackageProcessLoggingAndAssert** 속성을 **true**, MSBuild는:</span><span class="sxs-lookup"><span data-stu-id="b3062-107">When you set the **EnablePackageProcessLoggingAndAssert** property to **true**, MSBuild will:</span></span>
> 
> - <span data-ttu-id="b3062-108">빌드 로그에는 패키징 프로세스에 대 한 추가 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-108">Add additional information about the packaging process to the build logs.</span></span>
> - <span data-ttu-id="b3062-109">중복 파일 패키징 목록에 없으면 예를 들어, 특정 조건에서 오류를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-109">Log errors under certain conditions, for example, if duplicate files are found in the packaging list.</span></span>
> - <span data-ttu-id="b3062-110">로그 디렉터리를 만듭니다는 *ProjectName*\_패키지 폴더를 압축 하 고 있는 파일에 대 한 정보를 기록 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-110">Create a Log directory in the *ProjectName*\_Package folder and use it to record information about the files you're packaging.</span></span>
> 
> <span data-ttu-id="b3062-111">패키징 프로세스가 실패 하는 경우 웹 배포 패키지는 예상 되는 파일을 포함 하지 가지 잘못 된 것은이 정보 프로세스 및 pinpoint 문제를 해결 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-111">If the packaging process is failing, or your web deployment packages don't contain the files that you expect, you can use this information to troubleshoot the process and pinpoint where things are going wrong.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="b3062-112">합니다 **EnablePackageProcessLoggingAndAssert** 속성이 사용 하 여 프로젝트를 빌드하는 경우에 작동 합니다 **디버그** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-112">The **EnablePackageProcessLoggingAndAssert** property only works if you build your project using the **Debug** configuration.</span></span> <span data-ttu-id="b3062-113">속성은 다른 구성에서 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-113">The property is ignored in other configurations.</span></span>


<span data-ttu-id="b3062-114">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-114">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="b3062-115">이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3062-115">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="b3062-116">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-116">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a><span data-ttu-id="b3062-117">EnablePackageProcessLoggingAndAssert 속성 이해</span><span class="sxs-lookup"><span data-stu-id="b3062-117">Understanding the EnablePackageProcessLoggingAndAssert Property</span></span>

<span data-ttu-id="b3062-118">[빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) 웹 게시 파이프라인 (WPP) MSBuild의 기능을 확장 하 고 인터넷 정보 서비스 (IIS) 웹을 통합할 수 있도록 하는 MSBuild 대상 집합을 제공 하는 방법을 설명 합니다. 배포 도구 (웹 배포).</span><span class="sxs-lookup"><span data-stu-id="b3062-118">[Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) described how the Web Publishing Pipeline (WPP) provides a set of MSBuild targets that extend the functionality of MSBuild and enable it to integrate with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="b3062-119">웹 응용 프로그램 프로젝트를 패키지할 때는 WPP 대상을 호출 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-119">When you package a web application project, you're invoking WPP targets.</span></span>

<span data-ttu-id="b3062-120">이러한 WPP 대상 많은 추가 정보를 기록 하는 조건부 논리를 포함할 때 합니다 **EnablePackageProcessLoggingAndAssert** 속성이 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-120">Lots of these WPP targets include conditional logic that logs additional information when the **EnablePackageProcessLoggingAndAssert** property is set to **true**.</span></span> <span data-ttu-id="b3062-121">예를 들어, 검토 하는 경우는 **패키지** 대상에 추가 로그 디렉터리를 만드는 경우 파일의 목록을 텍스트 파일에 쓰는 볼 수 있습니다 **EnablePackageProcessLoggingAndAssert** 같으면**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-121">For example, if you review the **Package** target, you can see that it creates an additional log directory and writes a list of files to a text file if **EnablePackageProcessLoggingAndAssert** is equal to **true**.</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]


> [!NOTE]
> <span data-ttu-id="b3062-122">WPP 대상에 정의 된 합니다 *Microsoft.Web.Publishing.targets* %PROGRAMFILES (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-122">The WPP targets are defined in the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span> <span data-ttu-id="b3062-123">이 파일을 열고 Visual Studio 2010 또는 XML 편집기에서 대상 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-123">You can open this file and review the targets in Visual Studio 2010 or any XML editor.</span></span> <span data-ttu-id="b3062-124">파일의 내용을 수정할 수 없도록 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-124">Take care not to modify the contents of the file.</span></span>


## <a name="enabling-the-additional-logging"></a><span data-ttu-id="b3062-125">추가 로깅을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b3062-125">Enabling the Additional Logging</span></span>

<span data-ttu-id="b3062-126">에 대 한 값을 제공할 수 있습니다 합니다 **EnablePackageProcessLoggingAndAssert** 프로젝트를 작성 하는 방법에 따라 다양 한 방법으로 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-126">You can supply a value for the **EnablePackageProcessLoggingAndAssert** property in various ways, depending on how you build your project.</span></span>

<span data-ttu-id="b3062-127">명령줄에서 프로젝트를 빌드하는 경우에 대 한 값을 제공할 수 있습니다 합니다 **EnablePackageProcessLoggingAndAssert** 명령줄 인수로 속성:</span><span class="sxs-lookup"><span data-stu-id="b3062-127">If you build your project from the command line, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property as a command-line argument:</span></span>


[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]


<span data-ttu-id="b3062-128">사용자 지정 프로젝트 파일에 프로젝트 빌드를 사용 하는 경우 포함할 수 있습니다는 **EnablePackageProcessLoggingAndAssert** 값을 **속성** 특성을 **MSBuild**작업:</span><span class="sxs-lookup"><span data-stu-id="b3062-128">If you're using a custom project file to build your projects, you can include the **EnablePackageProcessLoggingAndAssert** value in the **Properties** attribute of the **MSBuild** task:</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]


<span data-ttu-id="b3062-129">를 사용 하 여 프로젝트를 빌드할 Team Foundation Server (TFS) 빌드 정의 사용 하는 경우에 대 한 값을 제공할 수 있습니다 합니다 **EnablePackageProcessLoggingAndAssert** 속성에는 **MSBuild 인수** 행:![](troubleshooting-the-packaging-process/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b3062-129">If you're using a Team Foundation Server (TFS) build definition to build your projects, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property in the **MSBuild Arguments** row:![](troubleshooting-the-packaging-process/_static/image1.png)</span></span>

> [!NOTE]
> <span data-ttu-id="b3062-130">작성 및 빌드 정의 구성에 대 한 자세한 내용은 참조 하세요. [배포를 만드는 빌드 정의 지 원하는](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-130">For more information on creating and configuring build definitions, see [Creating a Build Definition That Supports Deployment](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).</span></span>


<span data-ttu-id="b3062-131">또는 모든 빌드에서 패키지를 포함 하려는 경우 수정할 수 있습니다 설정 하 여 웹 응용 프로그램 프로젝트용 프로젝트 파일을 **EnablePackageProcessLoggingAndAssert** 속성을 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-131">Alternatively, if you want to include the package in every build, you can modify the project file for your web application project to set the **EnablePackageProcessLoggingAndAssert** property to **true**.</span></span> <span data-ttu-id="b3062-132">첫 번째 속성을 추가 해야 하면 **PropertyGroup** .csproj 또는.vbproj 파일 내의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-132">You should add the property to the first **PropertyGroup** element within your .csproj or .vbproj file.</span></span>


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]


## <a name="reviewing-the-log-files"></a><span data-ttu-id="b3062-133">로그 파일 검토</span><span class="sxs-lookup"><span data-stu-id="b3062-133">Reviewing the Log Files</span></span>

<span data-ttu-id="b3062-134">빌드 및 사용 하 여 웹 응용 프로그램 프로젝트를 패키지 있습니다 **EnablePackageProcessLoggingAndAssert** 로 설정 **true**, MSBuild 로그인 이라는 추가 폴더를 만듭니다는 *ProjectName* \_패키지 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-134">When you build and package a web application project with **EnablePackageProcessLoggingAndAssert** set to **true**, MSBuild creates an additional folder named Log in the *ProjectName*\_Package folder.</span></span> <span data-ttu-id="b3062-135">로그 폴더에는 다양 한 파일이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-135">The Log folder contains various files:</span></span>

![](troubleshooting-the-packaging-process/_static/image2.png)

<span data-ttu-id="b3062-136">표시 되는 파일 목록을 프로젝트 및 빌드 프로세스 작업에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-136">The list of files that you see will vary according to the things in your project and your build process.</span></span> <span data-ttu-id="b3062-137">그러나 이러한 파일은 프로세스의 여러 단계에서 패키징의 경우 WPP가 수집 하는 파일 목록을 기록 하려면 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-137">However, these files are typically used to record the list of files that the WPP is collecting for packaging, at various stages of the process:</span></span>

- <span data-ttu-id="b3062-138">합니다 *PreExcludePipelineCollectFilesPhaseFileList.txt* 파일 제외에 대 한 지정 된 모든 파일이 제거 되기 전에 패키지에 MSBuild를 수집 하는 파일을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-138">The *PreExcludePipelineCollectFilesPhaseFileList.txt* file lists the files that MSBuild collects for packaging before any files that are specified for exclusion are removed.</span></span>
- <span data-ttu-id="b3062-139">합니다 *AfterExcludeFilesFilesList.txt* 파일 제외에 대 한 지정 된 모든 파일을 제거한 후 수정 된 파일 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-139">The *AfterExcludeFilesFilesList.txt* file contains the modified file list after any files that are specified for exclusion are removed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b3062-140">패키징 프로세스에서 파일 및 폴더를 제외 하는 방법은 참조 하세요 [배포에서 제외 하 고 파일 및 폴더](excluding-files-and-folders-from-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-140">For more information on excluding files and folders from the packaging process, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>
- <span data-ttu-id="b3062-141">*AfterTransformWebConfig.txt* 파일에 대 한 패키징 후 수집 된 파일에 나열 *Web.config* 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-141">The *AfterTransformWebConfig.txt* file lists the files collected for packaging after any *Web.config* transforms have been performed.</span></span> <span data-ttu-id="b3062-142">이 목록의 모든 구성별 *Web.config* 같은 파일을 변환 *Web.Debug.config* 하 고 *Web.Release.config*, 파일 목록에서 제외 됩니다 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-142">In this list, any configuration-specific *Web.config* transform files, like *Web.Debug.config* and *Web.Release.config*, are excluded from the list of files for packaging.</span></span> <span data-ttu-id="b3062-143">변환 하는 단일 *Web.config* 그 자리에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-143">A single transformed *Web.config* is included in their place.</span></span>
- <span data-ttu-id="b3062-144">*PostAutoParameterizationWebConfigConnectionStrings.txt* 파일의 연결 문자열을 한 후 파일의 목록을 포함 합니다 *Web.config* 파일 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-144">The *PostAutoParameterizationWebConfigConnectionStrings.txt* file contains the list of files after the connection strings in the *Web.config* file have been parameterized.</span></span> <span data-ttu-id="b3062-145">이것이 패키지를 배포할 때 대상 환경에 대 한 올바른 설정을 사용 하 여 연결 문자열을 대체할 수 있도록 허용 하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-145">This is the process that lets you replace your connection strings with the right settings for your target environment when you deploy the package.</span></span>
- <span data-ttu-id="b3062-146">합니다 *Prepackage.txt* 파일 패키지에 포함 될 파일의 완료 된 빌드 전 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-146">The *Prepackage.txt* file contains the finalized pre-build list of files to be included in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="b3062-147">WPP 대상에 추가 로그 파일의 이름은 일반적으로 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-147">The names of the additional log files typically correspond to WPP targets.</span></span> <span data-ttu-id="b3062-148">검사 하 여 이러한 목표를 검토할 수 있습니다 합니다 *Microsoft.Web.Publishing.targets* %PROGRAMFILES (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-148">You can review these targets by examining the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>


<span data-ttu-id="b3062-149">웹 패키지의 내용을 예상한 바가 없는 경우 이러한 파일을 검토 프로세스 작업에서 어떤 지점 잘못 식별 하는 유용한 방법 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-149">If the contents of your web package aren't what you expected, reviewing these files can be a useful way to identify at what point in the process things went wrong.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b3062-150">결론</span><span class="sxs-lookup"><span data-stu-id="b3062-150">Conclusion</span></span>

<span data-ttu-id="b3062-151">이 항목에서는 사용 하는 방법을 설명 합니다 **EnablePackageProcessLoggingAndAssert** 패키징 프로세스 문제를 해결 하는 MSBuild의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-151">This topic described how you can use the **EnablePackageProcessLoggingAndAssert** property in MSBuild to troubleshoot the packaging process.</span></span> <span data-ttu-id="b3062-152">속성을 설정 하는 경우 기록 되는 추가 정보를 설명 하 고 빌드 프로세스에 속성 값을 제공할 수 있는 다양 한 방법을 설명 했습니다 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-152">It explained the different ways in which you can supply the property value to the build process, and it described the additional information that is recorded when you set the property to **true**.</span></span>

## <a name="further-reading"></a><span data-ttu-id="b3062-153">추가 정보</span><span class="sxs-lookup"><span data-stu-id="b3062-153">Further Reading</span></span>

<span data-ttu-id="b3062-154">사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하에 대 한 자세한 내용은 참조 하세요. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-154">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="b3062-155">WPP 및 패키징 프로세스를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-155">For more information on the WPP and how it manages the packaging process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="b3062-156">웹 배포 패키지에서 특정 파일 및 폴더를 제외 하는 방법에 대 한 지침을 참조 하세요 [배포에서 제외 하 고 파일 및 폴더](excluding-files-and-folders-from-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3062-156">For guidance on how to exclude specific files and folders from web deployment packages, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b3062-157">이전</span><span class="sxs-lookup"><span data-stu-id="b3062-157">Previous</span></span>](running-windows-powershell-scripts-from-msbuild-project-files.md)
