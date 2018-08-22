---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: What를 수행 하는 경우 배포 | Microsoft Docs
author: jrjlee
description: "' 경우 ' 수행 하는 방법에 설명 합니다 (또는 시뮬레이션)이 항목이에서는 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 V를 사용 하 여 배포 하는 중..."
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 054b15e1e58164ec7e85c77c39fb47bcb47879b9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826879"
---
<a name="performing-a-what-if-deployment"></a><span data-ttu-id="ddb88-103">"What If" 배포 수행</span><span class="sxs-lookup"><span data-stu-id="ddb88-103">Performing a "What If" Deployment</span></span>
====================
<span data-ttu-id="ddb88-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ddb88-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="ddb88-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ddb88-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ddb88-106">이 항목에서는 "what if"를 수행 하는 방법에 설명 합니다 (또는 시뮬레이션) VSDBCMD 고 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="ddb88-107">이렇게 하면 실제로 응용 프로그램을 배포 하기 전에 배포 논리를 특정 대상 환경에 미치는 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>


<span data-ttu-id="ddb88-108">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="ddb88-109">이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 및 배포 프로세스에 의해 제어 되는&#x2014;하나 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 빌드 명령이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="ddb88-110">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="ddb88-111">웹 패키지에 대 한 "What If" 배포 수행</span><span class="sxs-lookup"><span data-stu-id="ddb88-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="ddb88-112">"What if"에서 배포를 수행할 수 있는 기능 (또는 평가판)를 포함 하는 웹 배포 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="ddb88-113">"What if" 모드에서 아티팩트를 배포 하면 배포를 수행 해야 하지만 대상 서버에서 아무 것도 실제로 변경 되지 않은 것 처럼 로그 파일을 생성 웹 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="ddb88-114">로그 파일 검토 도움이 배포 해야 대상 서버에서 특히 어떤 영향을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="ddb88-115">새로운 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-115">What will get added.</span></span>
- <span data-ttu-id="ddb88-116">새로운 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-116">What will get updated.</span></span>
- <span data-ttu-id="ddb88-117">항목 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-117">What will get deleted.</span></span>

<span data-ttu-id="ddb88-118">"What if" 배포를 실제로 바뀌지 수행할 항상 수 없습니다. 작업 대상 서버에 있는 모든 것 이므로 배포 성공 여부를 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="ddb88-119">에 설명 된 대로 [웹 배포 패키지](../web-deployment-in-the-enterprise/deploying-web-packages.md), 두 가지 방법으로 웹 배포를 사용 하는 웹 패키지를 배포할 수 있습니다&#x2014;직접 또는 실행 하 여 MSDeploy.exe 명령줄 유틸리티를 사용 하 여는 *. deploy.cmd* 파일 빌드 프로세스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="ddb88-120">MSDeploy.exe를 직접 사용 하는 경우 추가 하 여 "what if" 배포를 실행할 수 있습니다 합니다 **– whatif** 플래그 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="ddb88-121">예를 들어 스테이징 환경에 ContactManager.Mvc.zip 패키지를 배포 하는 경우에 상황을 평가 하려면 MSDeploy 명령을 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]


<span data-ttu-id="ddb88-122">"What if" 배포의 결과 만족 하는 경우 제거할 수 있습니다 합니다 **– whatif** 라이브 배포를 실행 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="ddb88-123">MSDeploy.exe에 대 한 명령줄 옵션에 대 한 자세한 내용은 참조 하세요. [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>


<span data-ttu-id="ddb88-124">사용 중인 경우는 *. deploy.cmd* 파일을 포함 하 여 "what if" 배포를 실행할 수 있습니다 합니다 **/t** 플래그 대신 (평가판 모드) 플래그를 **/y** 플래그 ("yes" 또는 업데이트 모드)에서 사용자 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="ddb88-125">예를 들어, 실행 하 여 ContactManager.Mvc.zip 패키지를 배포 하는 경우에 상황을 평가 하는 *. deploy.cmd* 파일인 명령은 다음과 유사 합니다:</span><span class="sxs-lookup"><span data-stu-id="ddb88-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]


<span data-ttu-id="ddb88-126">바꿀 수 있습니다 "평가판 모드" 배포의 결과 만족 하면 합니다 **/t** 사용 하 여 플래그를 **/y** 라이브 배포를 실행 하는 플래그:</span><span class="sxs-lookup"><span data-stu-id="ddb88-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="ddb88-127">명령줄 옵션에 대 한 자세한 내용은 *. deploy.cmd* 파일을 참조 하세요 [방법: 설치 된 배포 패키지를 사용 하 여 deploy.cmd 파일](https://msdn.microsoft.com/library/ff356104.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddb88-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="ddb88-128">실행 하는 경우는 *. deploy.cmd* 파일 플래그를 지정 하지 않고 명령 프롬프트에는 사용 가능한 플래그의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>


## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="ddb88-129">데이터베이스에 대 한 "What If" 배포 수행</span><span class="sxs-lookup"><span data-stu-id="ddb88-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="ddb88-130">이 섹션에서는 증분, 스키마 기반 데이터베이스를 배포 하는 데 VSDBCMD 유틸리티를 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="ddb88-131">이 방법은에서 더 자세히 설명 되어 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="ddb88-132">잘 이해 하는이 항목에서는 사용 하 여 여기에 설명 된 개념을 적용 하기 전에 유지 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="ddb88-133">VSDBCMD를 사용 하는 경우 **배포** 모드를 사용할 수는 **/dd** (또는 **/DeployToDatabase**) VSDBCMD 실제로 데이터베이스를 배포 하거나만 생성 하는지 여부를 제어 하는 플래그를 배포 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="ddb88-134">.Dbschema 파일에 배포 하는 경우이 동작은:</span><span class="sxs-lookup"><span data-stu-id="ddb88-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="ddb88-135">지정 하는 경우 **/dd+** 하거나 **/dd**, VSDBCMD 배포 스크립트를 생성 되며 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="ddb88-136">지정 하는 경우 **/dd-** 스위치를 생략 하거나, VSDBCMD만 배포 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="ddb88-137">동작을.dbschema 파일이 아닌.deploymanifest 파일을 배포 하는 경우는 **/dd** 스위치는 훨씬 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="ddb88-138">VSDBCMD는 값을 무시 하는 기본적으로 **/dd** .deploymanifest 파일에 포함 된 경우 스위치를 **DeployToDatabase** 의 값을 가진 요소가 **True**.</span><span class="sxs-lookup"><span data-stu-id="ddb88-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="ddb88-139">[데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md) 전체에서이 동작을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>


<span data-ttu-id="ddb88-140">예를 들어에 대 한 배포 스크립트를 생성 하는 **ContactManager** VSDBCMD 명령을 데이터베이스에 실제로 배포 하지 않고 데이터베이스는 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]


<span data-ttu-id="ddb88-141">VSDBCMD 차등 데이터베이스 배포 도구를 이며 따라서 배포 스크립트를 동적으로 생성 지정한 스키마에 있는 경우 현재 데이터베이스를 업데이트 하는 데 필요한 모든 SQL 명령이 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="ddb88-142">배포 스크립트를 검토는 배포에 영향을 줄 내용을 결정 하는 유용한 방법을 현재 데이터베이스에 포함 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="ddb88-143">예를 들어, 다음 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="ddb88-144">기존 테이블 없어지고 여부는 결과를 데이터 손실 여부.</span><span class="sxs-lookup"><span data-stu-id="ddb88-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="ddb88-145">작업 순서 예를 들어 데이터 손실의 위험을 전달 하는지 여부를, 테이블을 병합 하거나 분할 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ddb88-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="ddb88-146">배포 스크립트에 만족할 경우 사용 하 여 VSDBCMD 반복할 수 있습니다는 **/dd+** 플래그 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="ddb88-147">또는 요구 사항을 충족 하 고 데이터베이스 서버에서 수동으로 실행 하려면 배포 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="ddb88-148">사용자 지정 프로젝트 파일에서 "What If" 기능 통합</span><span class="sxs-lookup"><span data-stu-id="ddb88-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="ddb88-149">더 복잡 한 배포 시나리오에서 사용 하 여 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 빌드 및 배포 논리를 캡슐화 하에 설명 된 대로 해야 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="ddb88-150">예를 들어, 합니다 [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션에는 *Publish.proj* 파일:</span><span class="sxs-lookup"><span data-stu-id="ddb88-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="ddb88-151">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-151">Builds the solution.</span></span>
- <span data-ttu-id="ddb88-152">패키지 ContactManager.Mvc 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="ddb88-153">패키지 ContactManager.Service 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="ddb88-154">배포 된 **ContactManager** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="ddb88-155">이러한 방식으로 단일 단계 프로세스를 여러 웹 패키지 및/또는 데이터베이스의 배포를 통합 하면 "what if" 모드에서 전체 배포를 수행 하는 옵션을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="ddb88-156">합니다 *Publish.proj* 파일이를 수행할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="ddb88-157">첫째, "what-if" 값을 저장 하는 속성을 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-157">First, you need to create a property to store the "what if" value:</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]


<span data-ttu-id="ddb88-158">이 경우 명명 된 속성을 만들었습니다 **WhatIf** 이며 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="ddb88-159">사용자 속성을 설정 하 여이 값을 재정의할 수 있습니다 **true** 명령줄 매개 변수에서 살펴보겠지만 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="ddb88-160">다음 단계는 모든 웹 배포 매개 변수화 및 VSDBCMD 명령 플래그를 나타내도록 합니다 **WhatIf** 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="ddb88-161">예를 들어, 다음 대상 (에서 가져온를 *Publish.proj* 파일 및 간소화 된) 실행 합니다 *. deploy.cmd* 웹 패키지를 배포 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="ddb88-162">기본적으로 명령에 포함 된 **/Y** ("yes" 또는 업데이트 모드) 스위치.</span><span class="sxs-lookup"><span data-stu-id="ddb88-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="ddb88-163">경우 **WhatIf** 로 설정 된 **true**, 바뀝니다이 **/T** 스위치 (평가판 또는 "what if" 모드).</span><span class="sxs-lookup"><span data-stu-id="ddb88-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]


<span data-ttu-id="ddb88-164">마찬가지로, 다음 대상 데이터베이스를 배포 하는 VSDBCMD 유틸리티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="ddb88-165">기본적으로 **/dd** 스위치 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="ddb88-166">즉, VSDBCMD 배포 스크립트를 생성 하는 있지만 데이터베이스를 배포 하지 것입니다&#x2014;즉, "what-if" 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="ddb88-167">경우는 **WhatIf** 속성으로 설정 되지 않은 **true**, **/dd** 스위치 추가 되 고 VSDBCMD 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]


<span data-ttu-id="ddb88-168">프로젝트 파일의 모든 관련 명령을 매개 변수화 하려면 동일한 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="ddb88-169">"What if" 배포를 실행 하려는 경우 단순히 제공할 수는 **WhatIf** 명령줄에서 속성 값:</span><span class="sxs-lookup"><span data-stu-id="ddb88-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]


<span data-ttu-id="ddb88-170">이러한 방식으로 한 단계로 모든 프로젝트 구성 요소에 대 한 "what if" 배포를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ddb88-171">결론</span><span class="sxs-lookup"><span data-stu-id="ddb88-171">Conclusion</span></span>

<span data-ttu-id="ddb88-172">이 항목에서는 웹 배포, VSDBCMD, 및 MSBuild를 사용 하 여 배포 "what if"를 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="ddb88-173">"What if" 배포를 사용 하면 대상 환경에 변경 내용을 실제로 만들기 전에 제안 된 배포의 영향을 평가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="ddb88-174">추가 정보</span><span class="sxs-lookup"><span data-stu-id="ddb88-174">Further Reading</span></span>

<span data-ttu-id="ddb88-175">웹 배포 명령줄 구문에 대 한 자세한 내용은 참조 하세요. [웹 배포 작업 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="ddb88-176">사용 하는 경우 명령줄 옵션에 대 한 지침은 합니다 *. deploy.cmd* 파일을 참조 하세요 [방법:는 배포 패키지를 사용 하 여 deploy.cmd 파일 설치](https://msdn.microsoft.com/library/ff356104.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddb88-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="ddb88-177">VSDBCMD 명령줄 구문에 대 한 지침을 참조 하세요. [VSDBCMD에 대 한 명령줄 참조 합니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddb88-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ddb88-178">[이전](advanced-enterprise-web-deployment.md)
> [다음](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="ddb88-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>
