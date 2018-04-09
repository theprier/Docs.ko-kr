---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: 경우에 기능을 수행 배포 | Microsoft Docs
author: jrjlee
description: 이 항목 ' 경우 어떻게 ' 수행 하는 방법에 설명 등의 시뮬레이션 된 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 V를 사용 하 여 배포...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: c1a13f38c8e629bcd615190b00104109e25fb289
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="performing-a-what-if-deployment"></a><span data-ttu-id="8698f-103">"경우 어떻게" 배포</span><span class="sxs-lookup"><span data-stu-id="8698f-103">Performing a "What If" Deployment</span></span>
====================
<span data-ttu-id="8698f-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="8698f-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="8698f-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="8698f-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="8698f-106">이 항목 "경우 어떻게" 수행 하는 방법에 설명 등의 시뮬레이션 된 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 및 VSDBCMD를 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="8698f-107">이렇게 하면 실제로 응용 프로그램을 배포 하기 전에 배포 논리는 특정 대상 환경에 미치는 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>


<span data-ttu-id="8698f-108">이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="8698f-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="8698f-109">이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에 빌드 및 배포 프로세스에 의해 제어 되는&#x2014;하나 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 빌드 명령이 포함 된입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="8698f-110">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="8698f-111">웹 패키지에 대 한 "경우 어떻게" 배포를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="8698f-112">"경우 어떻게"의 배포를 수행할 수 있는 기능 (또는 평가판)를 포함 하는 웹 배포 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="8698f-113">"경우 어떻게" 모드에서 아티팩트를 배포할 때 배포를 끝낸 있지만 대상 서버에 아무 것도 실제로 변경 되지 않은 로그 파일을 생성 웹 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="8698f-114">로그 파일을 검토 배포 갖습니다 대상 서버에 특히 어떤 영향을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="8698f-115">기능 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-115">What will get added.</span></span>
- <span data-ttu-id="8698f-116">어떤 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-116">What will get updated.</span></span>
- <span data-ttu-id="8698f-117">어떤 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-117">What will get deleted.</span></span>

<span data-ttu-id="8698f-118">"경우 어떻게" 배포 수행할 항상 수 없는 작업 대상 서버에 아무 것도 변경 실제로 되지 않으므로 배포는 성공 여부를 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="8698f-119">에 설명 된 대로 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md), 웹 배포를 사용 하 여 두 가지 방법으로 웹 패키지를 배포 하려면&#x2014;직접 또는 실행 하 여 MSDeploy.exe 명령줄 유틸리티를 사용 하 여는 *. deploy.cmd* 파일 빌드 프로세스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="8698f-120">MSDeploy.exe를 직접 사용 중인 경우 추가 하 여 "경우 어떻게" 배포를 실행할 수 있습니다는 **– whatif** 플래그를 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="8698f-121">예를 들어 스테이징 환경에 ContactManager.Mvc.zip 패키지를 배포 하는 경우 어떻게 되는지 평가 수행 하려면 MSDeploy 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]


<span data-ttu-id="8698f-122">"경우 어떻게" 배포 결과를 만족 하는 경우 제거할 수 있습니다는 **– whatif** 라이브 배포를 실행 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="8698f-123">MSDeploy.exe에 대 한 명령줄 옵션에 대 한 자세한 내용은 참조 하십시오. [웹 배포 작업이 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>


<span data-ttu-id="8698f-124">사용 중인 경우는 *. deploy.cmd* 파일을 포함 하 여 "경우 어떻게" 배포를 실행할 수 있습니다는 **/t** 대신 플래그 (평가판 모드) 플래그는 **/y** 의 플래그 ("yes" 또는 업데이트 모드) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="8698f-125">예를 들어, ContactManager.Mvc.zip 패키지를 실행 하 여 배포한 경우 어떻게 될 지를 평가 하는 *. deploy.cmd* 파일인 명령 다음과 유사 합니다:</span><span class="sxs-lookup"><span data-stu-id="8698f-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]


<span data-ttu-id="8698f-126">"평가 모드" 배포 결과를 만족 하는 경우 대체할 수 있습니다는 **/t** 와 플래그는 **/y** 라이브 배포를 실행 하는 플래그:</span><span class="sxs-lookup"><span data-stu-id="8698f-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="8698f-127">명령줄 옵션에 대 한 자세한 내용은 *. deploy.cmd* 파일, 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/library/ff356104.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="8698f-128">실행 하는 경우는 *. deploy.cmd* 파일 플래그를 지정 하지 않고 명령 프롬프트에는 사용 가능한 플래그의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>


## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="8698f-129">데이터베이스에 대 한 "경우 어떻게" 배포를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="8698f-130">이 섹션에서는 데이터베이스, 스키마 기반 증분 배포를 수행 하려면 VSDBCMD 유틸리티를 사용 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="8698f-131">이 방법은에서 더 자세하게 설명 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="8698f-132">잘 이해 하는이 항목을 여기에 설명 된 개념을 적용 하기 전에 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="8698f-133">VSDBCMD에서 사용 하는 경우 **배포** 사용할 수 있습니다 모드는 **d d** (또는 **/DeployToDatabase**) VSDBCMD 실제로 데이터베이스를 배포 하거나만 생성 하는지 여부를 제어 하는 플래그는 배포 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="8698f-134">.Dbschema 파일을 배포 하는 경우 이것은 동작:</span><span class="sxs-lookup"><span data-stu-id="8698f-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="8698f-135">지정 하는 경우 **/dd+** 또는 **d d**, VSDBCMD 배포 스크립트를 생성 하 고 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="8698f-136">지정 하는 경우 **/dd-** 이 스위치를 생략 하거나, VSDBCMD만 배포 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="8698f-137">동작은.dbschema 파일 대신.deploymanifest 파일을 배포할 경우에 **d d** 스위치는 훨씬 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="8698f-138">VSDBCMD의 값을 무시 합니다, 기본적으로 **d d** .deploymanifest 파일에 포함 된 경우 스위치는 **DeployToDatabase** 의 값을 가진 요소가 **True**합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="8698f-139">[데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md) 전체에서이 동작에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>


<span data-ttu-id="8698f-140">예를 들어에 대 한 배포 스크립트를 생성 하는 **ContactManager** 실제로 VSDBCMD 명령을 데이터베이스를 배포 하지 않고 데이터베이스는 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]


<span data-ttu-id="8698f-141">VSDBCMD, 차등 데이터베이스 배포 도구 이며 따라서 배포 스크립트를 동적으로 지정된 된 스키마에 있는 경우 현재 데이터베이스를 업데이트 하는 데 필요한 모든 SQL 명령이 포함 하도록 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="8698f-142">배포에 어떤 영향을 결정 하는 유용한 방법은 했을 경우에 현재 데이터베이스와 포함 된 데이터는 배포 스크립트를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="8698f-143">예를 들어 확인 하려는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="8698f-144">기존 테이블 없어지고 데이터 손실이 발생 하 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="8698f-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="8698f-145">여부 연산이 수행 하는 경우 데이터 손실의 위험 예를 들어 분할 하거나 테이블을 병합 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="8698f-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="8698f-146">배포 스크립트에 만족 하는 경우와 VSDBCMD 반복할 수 있습니다는 **/dd+** 플래그를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="8698f-147">또는 요구 사항에 맞게 선택한 다음 데이터베이스 서버에서 수동으로 실행 하는 배포 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="8698f-148">사용자 지정 프로젝트 파일에 "경우 어떻게" 기능 통합</span><span class="sxs-lookup"><span data-stu-id="8698f-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="8698f-149">더 복잡 한 배포 시나리오에서 사용 하 여 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 빌드 및 배포 논리를 캡슐화 하에 설명 된 대로 해야 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="8698f-150">예를 들어는 [않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션을는 *Publish.proj* 파일:</span><span class="sxs-lookup"><span data-stu-id="8698f-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="8698f-151">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-151">Builds the solution.</span></span>
- <span data-ttu-id="8698f-152">패키징 및 ContactManager.Mvc 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="8698f-153">패키징 및 ContactManager.Service 응용 프로그램을 배포 하는 웹 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="8698f-154">배포는 **ContactManager** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="8698f-155">이러한 방식으로 단일 단계 프로세스에 여러 웹 패키지 및/또는 데이터베이스의 배포를 통합 하는 경우 "경우 어떻게" 모드에서 전체 배포를 수행 하는 옵션이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="8698f-156">*Publish.proj* 파일이를 수행할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="8698f-157">먼저 "경우 어떻게" 값을 저장할 속성을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="8698f-157">First, you need to create a property to store the "what if" value:</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]


<span data-ttu-id="8698f-158">이 경우 라는 속성이 만든 **WhatIf** 의 기본값은 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="8698f-159">사용자가 속성을 설정 하 여이 값을 재정의할 수 **true** 명령줄 매개 변수, 살펴보겠지만 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="8698f-160">다음 단계는 모든 웹 배포 매개 변수화 하는 및 VSDBCMD 명령 플래그를 나타내도록는 **WhatIf** 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="8698f-161">예를 들어 다음 대상 (에서 가져온는 *Publish.proj* 파일 및 간소화 된) 실행 되는 *. deploy.cmd* 웹 패키지를 배포 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="8698f-162">명령에 포함 된 기본적으로는 **/Y** 스위치 ("yes" 또는 업데이트 모드).</span><span class="sxs-lookup"><span data-stu-id="8698f-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="8698f-163">경우 **WhatIf** 로 설정 된 **true**,이으로 대체 되는 **/T** 스위치 (평가판, 또는 "경우 어떻게" 모드).</span><span class="sxs-lookup"><span data-stu-id="8698f-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]


<span data-ttu-id="8698f-164">마찬가지로, 다음 대상 VSDBCMD 유틸리티를 사용 하 여 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="8698f-165">기본적으로는 **d d** 스위치는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="8698f-166">즉, VSDBCMD 배포 스크립트를 생성 하는 있지만 데이터베이스를 배포 하지 것입니다&#x2014;즉, "what-if" 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="8698f-167">경우는 **WhatIf** 속성으로 설정 되지 않은 **true**, **d d** 스위치 추가 되 고 VSDBCMD 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>


[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]


<span data-ttu-id="8698f-168">프로젝트 파일의 모든 관련 명령을 매개 변수화 하 같은 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="8698f-169">"경우 어떻게" 배포를 실행 하려는 경우 수 다음 제공 하기만 하면는 **WhatIf** 명령줄에서 속성 값:</span><span class="sxs-lookup"><span data-stu-id="8698f-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>


[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]


<span data-ttu-id="8698f-170">이러한 방식으로 한 번에 모든 프로젝트 구성 요소에 대 한 "경우 어떻게" 배포를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8698f-171">결론</span><span class="sxs-lookup"><span data-stu-id="8698f-171">Conclusion</span></span>

<span data-ttu-id="8698f-172">이 항목에는 웹 배포, VSDBCMD, 및 MSBuild를 사용 하 여 배포 "경우 어떻게"를 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="8698f-173">"경우 어떻게" 배포를 사용 하면 대상 환경에 실제로 변경을 수행 하기 전에 제안 된 배포의 영향을 평가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="8698f-174">추가 정보</span><span class="sxs-lookup"><span data-stu-id="8698f-174">Further Reading</span></span>

<span data-ttu-id="8698f-175">웹 배포 명령줄 구문에 대 한 자세한 내용은 참조 하십시오. [웹 배포 작업이 설정](https://technet.microsoft.com/library/dd569089(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="8698f-176">사용 하는 경우 명령줄 옵션에 대 한 지침은 *. deploy.cmd* 파일에서 참조 [하는 방법: 설치는 배포 패키지를 사용 하 여 파일 deploy.cmd](https://msdn.microsoft.com/library/ff356104.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="8698f-177">VSDBCMD 명령줄 구문에 대 한 지침을 참조 하십시오. [VSDBCMD에 대 한 명령줄 참조 합니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8698f-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8698f-178">[이전](advanced-enterprise-web-deployment.md)
> [다음](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="8698f-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>
