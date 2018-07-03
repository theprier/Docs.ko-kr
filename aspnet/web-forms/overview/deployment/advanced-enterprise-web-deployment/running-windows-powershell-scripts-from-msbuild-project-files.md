---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트 실행 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하는 방법을 설명 합니다. 스크립트를 로컬로 실행할 수 있습니다 (즉, b에....
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: ddb658d8a8f224a7c417321df3e17ce0610d2473
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37362897"
---
<a name="running-windows-powershell-scripts-from-msbuild-project-files"></a><span data-ttu-id="06e36-104">MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-104">Running Windows PowerShell Scripts from MSBuild Project Files</span></span>
====================
<span data-ttu-id="06e36-105">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="06e36-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="06e36-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="06e36-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="06e36-107">이 항목에서는 빌드 및 배포 프로세스의 일부로 Windows PowerShell 스크립트를 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-107">This topic describes how to run a Windows PowerShell script as part of a build and deployment process.</span></span> <span data-ttu-id="06e36-108">(즉, 빌드 서버)에서 로컬로 스크립트를 실행 하거나 대상 웹 서버 또는 데이터베이스 서버에서 원격으로 원하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-108">You can run a script locally (in other words, on the build server) or remotely, like on a destination web server or database server.</span></span>
> 
> <span data-ttu-id="06e36-109">배포 후 Windows PowerShell 스크립트를 실행 하려는 이유 많습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-109">There are lots of reasons why you might want to run a post-deployment Windows PowerShell script.</span></span> <span data-ttu-id="06e36-110">예를 들어, 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-110">For example, you might want to:</span></span>
> 
> - <span data-ttu-id="06e36-111">사용자 지정 이벤트 소스를 레지스트리에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-111">Add a custom event source to the registry.</span></span>
> - <span data-ttu-id="06e36-112">업로드에 대 한 파일 시스템 디렉터리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-112">Generate a file system directory for uploads.</span></span>
> - <span data-ttu-id="06e36-113">빌드 디렉터리를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-113">Clean up build directories.</span></span>
> - <span data-ttu-id="06e36-114">사용자 지정 로그 파일에 항목을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-114">Write entries to a custom log file.</span></span>
> - <span data-ttu-id="06e36-115">새로 프로 비전 된 웹 응용 프로그램에 사용자를 초대 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-115">Send emails inviting users to a newly provisioned web application.</span></span>
> - <span data-ttu-id="06e36-116">적절 한 권한을 가진 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-116">Create user accounts with the appropriate permissions.</span></span>
> - <span data-ttu-id="06e36-117">SQL Server 인스턴스 간에 복제를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-117">Configure replication between SQL Server instances.</span></span>
> 
> <span data-ttu-id="06e36-118">이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일에서 사용자 지정 대상을에서 로컬 및 원격으로 Windows PowerShell 스크립트를 실행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-118">This topic will show you how to run Windows PowerShell scripts both locally and remotely from a custom target in a Microsoft Build Engine (MSBuild) project file.</span></span>


<span data-ttu-id="06e36-119">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="06e36-120">이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="06e36-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="06e36-121">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="06e36-122">작업 개요</span><span class="sxs-lookup"><span data-stu-id="06e36-122">Task Overview</span></span>

<span data-ttu-id="06e36-123">Windows PowerShell 스크립트를 자동화 하거나 단일 단계 배포 프로세스의 일환으로를 실행 하려면 이러한 상위 수준의 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-123">To run a Windows PowerShell script as part of an automated or single-step deployment process, you'll need to complete these high-level tasks:</span></span>

- <span data-ttu-id="06e36-124">소스 제어에 솔루션을 Windows PowerShell 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-124">Add the Windows PowerShell script to your solution and to source control.</span></span>
- <span data-ttu-id="06e36-125">Windows PowerShell 스크립트를 호출 하는 명령을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-125">Create a command that invokes your Windows PowerShell script.</span></span>
- <span data-ttu-id="06e36-126">명령에 모든 예약 된 XML 문자를 이스케이프 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-126">Escape any reserved XML characters in your command.</span></span>
- <span data-ttu-id="06e36-127">사용자 지정 MSBuild 프로젝트 파일의 대상 만들기 및 사용 합니다 **Exec** 명령을 실행 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-127">Create a target in your custom MSBuild project file and use the **Exec** task to run your command.</span></span>

<span data-ttu-id="06e36-128">이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-128">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="06e36-129">작업은이 문서의 연습은 이미 친숙 해 MSBuild 대상 및 속성을 사용 하 여 빌드 및 배포 프로세스를 사용자 지정 MSBuild 프로젝트 파일을 사용 하는 방법을 이해 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-129">The tasks and walkthroughs in this topic assume that you're already familiar with MSBuild targets and properties, and that you understand how to use a custom MSBuild project file to drive a build and deployment process.</span></span> <span data-ttu-id="06e36-130">자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-130">For more information, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

## <a name="creating-and-adding-windows-powershell-scripts"></a><span data-ttu-id="06e36-131">만들기 및 Windows PowerShell 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-131">Creating and Adding Windows PowerShell Scripts</span></span>

<span data-ttu-id="06e36-132">라는 샘플 Windows PowerShell 스크립트를 사용 하 여이 항목의 태스크 **LogDeploy.ps1** MSBuild에서 스크립트를 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-132">The tasks in this topic use a sample Windows PowerShell script named **LogDeploy.ps1** to illustrate how to run scripts from MSBuild.</span></span> <span data-ttu-id="06e36-133">합니다 **LogDeploy.ps1** 스크립트 줄 항목을 로그 파일에 기록 하는 간단한 함수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-133">The **LogDeploy.ps1** script contains a simple function that writes a single-line entry to a log file:</span></span>


[!code-javascript[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.js)]


<span data-ttu-id="06e36-134">합니다 **LogDeploy.ps1** 스크립트는 두 개의 매개 변수를 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-134">The **LogDeploy.ps1** script accepts two parameters.</span></span> <span data-ttu-id="06e36-135">첫 번째 매개 변수는 항목을 추가 하려는 로그 파일에 전체 경로 나타내는 나타내고 두 번째 매개 변수를 로그 파일에 기록 하려면 배포 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-135">The first parameter represents the full path to the log file to which you want to add an entry, and the second parameter represents the deployment destination that you want to record in the log file.</span></span> <span data-ttu-id="06e36-136">스크립트를 실행 하면 줄이 형식으로 로그 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-136">When you run the script, it adds a line to the log file in this format:</span></span>


[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]


<span data-ttu-id="06e36-137">확인 합니다 **LogDeploy.ps1** MSBuild를 사용할 수 있는 스크립트를에:</span><span class="sxs-lookup"><span data-stu-id="06e36-137">To make the **LogDeploy.ps1** script available to MSBuild, you need to:</span></span>

- <span data-ttu-id="06e36-138">소스 제어에 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-138">Add the script to source control.</span></span>
- <span data-ttu-id="06e36-139">Visual Studio 2010의 솔루션에 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-139">Add the script to your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="06e36-140">빌드 서버에서 또는 원격 컴퓨터에서 스크립트를 실행 하려는 여부에 관계 없이 솔루션 콘텐츠를 사용 하 여 스크립트를 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-140">You don't need to deploy the script with your solution content, regardless of whether you plan to run the script on the build server or on a remote computer.</span></span> <span data-ttu-id="06e36-141">한 가지 방법은 솔루션 폴더에 스크립트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-141">One option is to add the script to a solution folder.</span></span> <span data-ttu-id="06e36-142">Contact Manager 예제에서는 배포 프로세스의 일부로 Windows PowerShell 스크립트를 사용 하려고 하기 때문에 것이 좋습니다 게시 솔루션 폴더에 스크립트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-142">In the Contact Manager example, because you want to use the Windows PowerShell script as part of the deployment process, it makes sense to add the script to the Publish solution folder.</span></span>

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

<span data-ttu-id="06e36-143">솔루션 폴더 내용의 원본 자료로 빌드 서버에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-143">The contents of solution folders are copied to build servers as source material.</span></span> <span data-ttu-id="06e36-144">그러나 프로젝트 출력의 일부가 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-144">However, they form no part of any project output.</span></span>

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a><span data-ttu-id="06e36-145">빌드 서버에서 Windows PowerShell 스크립트를 실행</span><span class="sxs-lookup"><span data-stu-id="06e36-145">Executing a Windows PowerShell Script on the Build Server</span></span>

<span data-ttu-id="06e36-146">일부 시나리오에서는 프로젝트를 작성 하는 컴퓨터의 Windows PowerShell 스크립트를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-146">In some scenarios, you may want to run Windows PowerShell scripts on the computer that builds your projects.</span></span> <span data-ttu-id="06e36-147">예를 들어 빌드 폴더를 정리 하거나 사용자 지정 로그 파일에 항목을 작성 하는 Windows PowerShell 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-147">For example, you might use a Windows PowerShell script to clean up build folders or write entries to a custom log file.</span></span>

<span data-ttu-id="06e36-148">구문 측면에서 MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행와 같습니다 일반 명령 프롬프트에서 Windows PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-148">In terms of syntax, running a Windows PowerShell script from an MSBuild project file is the same as running a Windows PowerShell script from a regular command prompt.</span></span> <span data-ttu-id="06e36-149">실행 powershell.exe를 호출 하 여 사용 해야 합니다 **– 명령** 스위치를 실행 하려면 Windows PowerShell 명령을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-149">You need to invoke the powershell.exe executable and use the **–command** switch to provide the commands you want Windows PowerShell to run.</span></span> <span data-ttu-id="06e36-150">(Windows PowerShell v2에서는 사용할 수도 있습니다는 **– 파일** 전환).</span><span class="sxs-lookup"><span data-stu-id="06e36-150">(In Windows PowerShell v2, you can also use the **–file** switch).</span></span> <span data-ttu-id="06e36-151">명령에는이 형식으로 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-151">The command should take this format:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]


<span data-ttu-id="06e36-152">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="06e36-152">For example:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]


<span data-ttu-id="06e36-153">스크립트 경로 공백이 포함 하는 경우 파일 경로 앞에 앰퍼샌드 작은따옴표로 묶어야 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-153">If the path to your script includes spaces, you need to enclose the file path in single quotes preceded by an ampersand.</span></span> <span data-ttu-id="06e36-154">명령을를 이미 사용 했습니다 때문에 큰따옴표를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-154">You can't use double quotes, because you've already used them to enclose the command:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]


<span data-ttu-id="06e36-155">MSBuild에서이 명령을 호출할 때 몇 가지 추가 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-155">There are a few additional considerations when you invoke this command from MSBuild.</span></span> <span data-ttu-id="06e36-156">먼저 포함 해야 합니다 **– NonInteractive** 스크립트 자동 모드로 실행 되도록 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-156">First, you should include the **–NonInteractive** flag to ensure that the script executes quietly.</span></span> <span data-ttu-id="06e36-157">다음을 포함 해야 합니다 **– ExecutionPolicy** 적절 한 인수 값을 사용 하 여 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-157">Next, you should include the **–ExecutionPolicy** flag with an appropriate argument value.</span></span> <span data-ttu-id="06e36-158">Windows PowerShell 스크립트에 적용 됩니다 하 여 스크립트 실행을 방해할 수 있는 기본 실행 정책을 재정의할 수 있습니다 실행 정책을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-158">This specifies the execution policy that Windows PowerShell will apply to your script and allows you to override the default execution policy, which may prevent execution of your script.</span></span> <span data-ttu-id="06e36-159">이러한 인수 값에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-159">You can choose from these argument values:</span></span>

- <span data-ttu-id="06e36-160">값이 **Unrestricted** 스크립트의 서명 여부에 관계 없이 스크립트를 실행 하려면 Windows PowerShell을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-160">A value of **Unrestricted** will allow Windows PowerShell to execute your script, regardless of whether the script is signed.</span></span>
- <span data-ttu-id="06e36-161">값이 **RemoteSigned** 로컬 컴퓨터에서 생성 된 서명 되지 않은 스크립트를 실행 하려면 Windows PowerShell을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-161">A value of **RemoteSigned** will allow Windows PowerShell to execute unsigned scripts that were created on the local machine.</span></span> <span data-ttu-id="06e36-162">그러나 다른 곳에서 생성 된 스크립트는 서명 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-162">However, scripts that were created elsewhere must be signed.</span></span> <span data-ttu-id="06e36-163">(실제로 모르는 만든 Windows PowerShell 스크립트를 로컬로 빌드 서버에서 거의)입니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-163">(In practice, you're very unlikely to have created a Windows PowerShell script locally on a build server).</span></span>
- <span data-ttu-id="06e36-164">값이 **AllSigned** 만 서명 된 스크립트를 실행 하려면 Windows PowerShell을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-164">A value of **AllSigned** will allow Windows PowerShell to execute signed scripts only.</span></span>

<span data-ttu-id="06e36-165">기본 실행 정책은 **Restricted**, Windows PowerShell 스크립트 파일 실행 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-165">The default execution policy is **Restricted**, which prevents Windows PowerShell from running any script files.</span></span>

<span data-ttu-id="06e36-166">마지막으로 Windows PowerShell 명령에서 발생 하는 모든 예약 된 XML 문자를 이스케이프 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-166">Finally, you need to escape any reserved XML characters that occur in your Windows PowerShell command:</span></span>

- <span data-ttu-id="06e36-167">사용 하 여 작은따옴표로 바꿉니다  **&amp;a p o s;**</span><span class="sxs-lookup"><span data-stu-id="06e36-167">Replace single quotes with **&amp;apos;**</span></span>
- <span data-ttu-id="06e36-168">대체 된 큰따옴표  **&amp;q u o t;**</span><span class="sxs-lookup"><span data-stu-id="06e36-168">Replace double quotes with **&amp;quot;**</span></span>
- <span data-ttu-id="06e36-169">앰퍼샌드를 사용 하 여 바꿉니다  **&amp;a m p;**</span><span class="sxs-lookup"><span data-stu-id="06e36-169">Replace ampersands with **&amp;amp;**</span></span>

- <span data-ttu-id="06e36-170">이러한 변경 하면이 명령 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-170">When you make these changes, your command will resemble this:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]


<span data-ttu-id="06e36-171">사용자 지정 MSBuild 프로젝트 파일 내에서 새 대상 만들기를 사용 합니다 **Exec** 이 명령을 실행 하는 작업:</span><span class="sxs-lookup"><span data-stu-id="06e36-171">Within your custom MSBuild project file, you can create a new target and use the **Exec** task to run this command:</span></span>


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]


<span data-ttu-id="06e36-172">이 예제는 note:</span><span class="sxs-lookup"><span data-stu-id="06e36-172">In this example, note that:</span></span>

- <span data-ttu-id="06e36-173">매개 변수 값 및 Windows PowerShell 실행 파일의 위치와 같은 변수를 MSBuild 속성으로 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-173">Any variables, like parameter values and the location of the Windows PowerShell executable, are declared as MSBuild properties.</span></span>
- <span data-ttu-id="06e36-174">사용자가 명령줄에서 이러한 값을 재정의할 수 있도록 조건이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-174">Conditions are included to enable users to override these values from the command line.</span></span>
- <span data-ttu-id="06e36-175">합니다 **MSDeployComputerName** 속성은 다른 곳에서 프로젝트 파일에서 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-175">The **MSDeployComputerName** property is declared elsewhere in the project file.</span></span>

<span data-ttu-id="06e36-176">이 대상은 빌드 프로세스의 일환으로를 실행 하면 Windows PowerShell 명령 실행 되 고 지정한 파일에 로그 항목을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-176">When you execute this target as part of your build process, Windows PowerShell will run your command and write a log entry to the file you specified.</span></span>

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a><span data-ttu-id="06e36-177">원격 컴퓨터에서 Windows PowerShell 스크립트를 실행</span><span class="sxs-lookup"><span data-stu-id="06e36-177">Executing a Windows PowerShell Script on a Remote Computer</span></span>

<span data-ttu-id="06e36-178">Windows PowerShell은 스크립트를 통해 원격 컴퓨터에서 실행할 수 있는 [Windows 원격 관리](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM).</span><span class="sxs-lookup"><span data-stu-id="06e36-178">Windows PowerShell is capable of running scripts on remote computers through [Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM).</span></span> <span data-ttu-id="06e36-179">이 위해 사용 해야 합니다 [Invoke-command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06e36-179">To do this, you need to use the [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet.</span></span> <span data-ttu-id="06e36-180">이렇게 하면 원격 컴퓨터에 스크립트를 복사 하지 않고 하나 이상의 원격 컴퓨터에 대해 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-180">This lets you execute your script against one or more remote computers without copying the script to the remote computers.</span></span> <span data-ttu-id="06e36-181">스크립트를 실행 하는 로컬 컴퓨터에 모든 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-181">Any results are returned to the local computer from which you ran the script.</span></span>

> [!NOTE]
> <span data-ttu-id="06e36-182">사용 하기 전에 합니다 **Invoke-command** 원격 컴퓨터에서 스크립트를 실행할 Windows PowerShell cmdlet, 원격 메시지를 수신 하도록 WinRM 수신기를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-182">Before you use the **Invoke-Command** cmdlet to execute Windows PowerShell scripts on a remote computer, you need to configure a WinRM listener to accept remote messages.</span></span> <span data-ttu-id="06e36-183">이 명령을 실행 하 여 수행할 수 있습니다 **winrm quickconfig** 원격 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="06e36-183">You can do this by running the command **winrm quickconfig** on the remote computer.</span></span> <span data-ttu-id="06e36-184">자세한 내용은 [설치 및 구성에 대 한 Windows 원격 관리](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-184">For more information, see [Installation and Configuration for Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).</span></span>


<span data-ttu-id="06e36-185">Windows PowerShell 창에서이 구문을 사용 하려고 합니다 **LogDeploy.ps1** 원격 컴퓨터에서 스크립트:</span><span class="sxs-lookup"><span data-stu-id="06e36-185">From a Windows PowerShell window, you'd use this syntax to run the **LogDeploy.ps1** script on a remote computer:</span></span>


[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]


> [!NOTE]
> <span data-ttu-id="06e36-186">가지 다른 다양 한 방법으로 사용 하 여 **Invoke-command** 스크립트를 실행 하려면 파일에 있지만이 방법은 가장 간단한 매개 변수 값을 제공 하 고 공백 사용 하 여 경로 관리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-186">There are various other ways of using **Invoke-Command** to run a script file, but this approach is the most straightforward when you need to provide parameter values and manage paths with spaces.</span></span>


<span data-ttu-id="06e36-187">이 명령 프롬프트에서를 실행 하면 Windows PowerShell 실행 파일을 호출 하 여 사용 해야 합니다 **– 명령** 사용자 지침을 제공 하는 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="06e36-187">When you run this from a command prompt, you need to invoke the Windows PowerShell executable and use the **–command** parameter to provide your instructions:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]


<span data-ttu-id="06e36-188">이전에 일부 추가 스위치를 제공 하 고 MSBuild에서 명령을 실행할 때 예약된 된 XML 문자를 이스케이프 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-188">As before, you need to provide some additional switches and escape any reserved XML characters when you run the command from MSBuild:</span></span>


[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]


<span data-ttu-id="06e36-189">마지막으로, 이전과 마찬가지로 사용할 수는 **Exec** 프로그램 명령을 실행 하려면 사용자 지정 MSBuild 대상 내의 태스크:</span><span class="sxs-lookup"><span data-stu-id="06e36-189">Finally, as before, you can use the **Exec** task within a custom MSBuild target to execute your command:</span></span>


[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]


<span data-ttu-id="06e36-190">이 대상은 빌드 프로세스의 일환으로를 실행 하면 Windows PowerShell에서 지정 된 컴퓨터에 스크립트를 실행 합니다는 **– computername** 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-190">When you execute this target as part of your build process, Windows PowerShell will run your script on the computer you specified in the **–computername** argument.</span></span>

## <a name="conclusion"></a><span data-ttu-id="06e36-191">결론</span><span class="sxs-lookup"><span data-stu-id="06e36-191">Conclusion</span></span>

<span data-ttu-id="06e36-192">이 항목에서는 MSBuild 프로젝트 파일에서 Windows PowerShell 스크립트를 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-192">This topic described how to run a Windows PowerShell script from an MSBuild project file.</span></span> <span data-ttu-id="06e36-193">자동화 하거나 단일 단계 빌드 및 배포 프로세스의 일부로 로컬 또는 원격 컴퓨터에서 Windows PowerShell 스크립트를 실행 하려면이 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-193">You can use this approach to run a Windows PowerShell script, either locally or on a remote computer, as part of an automated or single-step build and deployment process.</span></span>

## <a name="further-reading"></a><span data-ttu-id="06e36-194">추가 정보</span><span class="sxs-lookup"><span data-stu-id="06e36-194">Further Reading</span></span>

<span data-ttu-id="06e36-195">Windows PowerShell 스크립트에 서명 하 고 실행 정책을 관리에 대 한 지침을 참조 하세요 [Windows PowerShell 스크립트 실행](https://technet.microsoft.com/library/ee176949.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-195">For guidance on signing Windows PowerShell scripts and managing execution policies, see [Running Windows PowerShell Scripts](https://technet.microsoft.com/library/ee176949.aspx).</span></span> <span data-ttu-id="06e36-196">원격 컴퓨터에서 Windows PowerShell 명령을 실행에 대 한 지침을 참조 하세요 [원격 명령 실행](https://technet.microsoft.com/library/dd819505.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-196">For guidance on running Windows PowerShell commands from a remote computer, see [Running Remote Commands](https://technet.microsoft.com/library/dd819505.aspx).</span></span>

<span data-ttu-id="06e36-197">사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하에 대 한 자세한 내용은 참조 하세요. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06e36-197">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="06e36-198">[이전](taking-web-applications-offline-with-web-deploy.md)
> [다음](troubleshooting-the-packaging-process.md)</span><span class="sxs-lookup"><span data-stu-id="06e36-198">[Previous](taking-web-applications-offline-with-web-deploy.md)
[Next](troubleshooting-the-packaging-process.md)</span></span>
