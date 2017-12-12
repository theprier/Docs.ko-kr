---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: "실습 랩: Azure 웹 사이트를 유지 관리 가능한: 변경 및 크기 조정 관리 | Microsoft Docs"
author: rick-anderson
description: "Microsoft Azure를 사용 하면 쉽게 만들고 프로덕션 환경에 웹 사이트를 배포 합니다. 하지만 응용 프로그램은 라이브 때 완료 되지 않았습니다, 그리고 방금 시작! 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: 1d6d9265d93fbd32e2d9c22e2ac3db9b5ffd9776
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="e2fdd-105">실습 랩: Azure 웹 사이트를 유지 관리 가능한: 변경 및 크기 조정 관리</span><span class="sxs-lookup"><span data-stu-id="e2fdd-105">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>
====================
<span data-ttu-id="e2fdd-106">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="e2fdd-106">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="e2fdd-107">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-107">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="e2fdd-108">Microsoft Azure를 사용 하면 쉽게 만들고 프로덕션 환경에 웹 사이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-108">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="e2fdd-109">하지만 응용 프로그램은 라이브 때 완료 되지 않았습니다, 그리고 방금 시작!</span><span class="sxs-lookup"><span data-stu-id="e2fdd-109">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="e2fdd-110">변경 요구 사항, 데이터베이스 업데이트, 배율 등을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-110">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="e2fdd-111">다행히 Azure 앱 서비스에는 다량의 원활 하 게 실행 하 여 사이트를 유지 하는 데 유용한 기능을 거둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-111">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
> 
> <span data-ttu-id="e2fdd-112">Azure는 안전 하 고 유연한 개발, 배포 및 확장 크기는 웹 응용 프로그램에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-112">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="e2fdd-113">만들기 및 배포 인프라를 관리할 필요 없이 응용 프로그램에 기존 도구를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-113">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
> 
> <span data-ttu-id="e2fdd-114">프로 비전 프로덕션 웹 응용 프로그램 사용자가 직접 분에서 쉽게 즐겨 찾는 개발 도구를 사용 하 여 만든 콘텐츠를 배포 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-114">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="e2fdd-115">기존 사이트를 지 원하는 소스 제어에서 직접 배포할 수 있습니다 **Git**, **GitHub**, **Bitbucket**, **TFS**, 및에  **DropBox**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-115">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="e2fdd-116">즐겨 찾는 IDE에서 직접 또는 스크립트를 사용 하 여 배포 **PowerShell** windows에서 또는 **CLI** 모든 OS에서 실행 되는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-116">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="e2fdd-117">배포 된 후에 사이트를 연속 배포를 지 원하는 지속적으로 최신 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-117">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
> 
> <span data-ttu-id="e2fdd-118">Azure 큰 또는 작은 모든 데이터에 대 한 내구성이 있는 확장 가능한 클라우드 저장소, 백업 및 복구 솔루션 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-118">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="e2fdd-119">응용 프로그램을 프로덕션 환경, 테이블, Blob 및 SQL 데이터베이스와 같은 저장소 서비스를 배포할 때는 클라우드에서 응용 프로그램을 확장 하는 데 도움이.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-119">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
> 
> <span data-ttu-id="e2fdd-120">SQL 데이터베이스와 새 버전의 응용 프로그램을 배포 하는 경우 생산성 데이터베이스를 최신 상태로 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-120">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="e2fdd-121">에 감사 드립니다 **Entity Framework Code First 마이그레이션을**, 개발 및 배포 데이터 모델의 분에서 환경을 업데이트할 간소화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-121">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="e2fdd-122">이 실습 랩에서 Microsoft Azure에서 프로덕션 환경에 웹 앱을 배포할 때 발생할 수 있습니다 다른 항목에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-122">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
> 
> <span data-ttu-id="e2fdd-123">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-123">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>
> 
> <span data-ttu-id="e2fdd-124">이 항목의 깊이 있는 자세한 검사에 대 한 참조는 [Azure 전자책으로 실제 클라우드 응용 프로그램 빌딩](building-real-world-cloud-apps-with-windows-azure/introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-124">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="e2fdd-125">개요</span><span class="sxs-lookup"><span data-stu-id="e2fdd-125">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="e2fdd-126">목표</span><span class="sxs-lookup"><span data-stu-id="e2fdd-126">Objectives</span></span>

<span data-ttu-id="e2fdd-127">이 실습 랩에서 배웁니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="e2fdd-127">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="e2fdd-128">기존 모델과 함께 엔터티 프레임 워크 마이그레이션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e2fdd-128">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="e2fdd-129">개체 모델 및 그에 따라 엔터티 프레임 워크 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-129">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="e2fdd-130">Git를 사용 하 여 Azure 응용 프로그램 서비스에 배포</span><span class="sxs-lookup"><span data-stu-id="e2fdd-130">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="e2fdd-131">Azure 관리 포털을 사용 하 여 이전 배포 rollback</span><span class="sxs-lookup"><span data-stu-id="e2fdd-131">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="e2fdd-132">Azure 저장소를 사용 하 여 웹 앱의 크기를 조정 하려면</span><span class="sxs-lookup"><span data-stu-id="e2fdd-132">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="e2fdd-133">Azure 관리 포털을 사용 하 여 웹 응용 프로그램에 대 한 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="e2fdd-133">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="e2fdd-134">만들기 및 Visual Studio에서 부하 테스트 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="e2fdd-134">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="e2fdd-135">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="e2fdd-135">Prerequisites</span></span>

<span data-ttu-id="e2fdd-136">다음은이 실습 랩을 완료 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-136">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="e2fdd-137">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="e2fdd-137">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="e2fdd-138">Azure SDK for.NET 2.2</span><span class="sxs-lookup"><span data-stu-id="e2fdd-138">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="e2fdd-139">GIT 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-139">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="e2fdd-140">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="e2fdd-140">A Microsoft Azure subscription</span></span> 

    - <span data-ttu-id="e2fdd-141">에 등록 한 [무료 평가판](http://aka.ms/watk-freetrial)</span><span class="sxs-lookup"><span data-stu-id="e2fdd-141">Sign up for a [Free Trial](http://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="e2fdd-142">인 경우 Visual Studio Professional, Test Professional, Premium 또는 Ultimate MSDN 또는 MSDN 플랫폼 구독자와 활성화 프로그램 [MSDN 혜택](http://aka.ms/watk-msdn) Azure에서 개발 및 테스트를 시작 하려면 지금</span><span class="sxs-lookup"><span data-stu-id="e2fdd-142">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](http://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="e2fdd-143">[BizSpark](http://aka.ms/watk-bizspark) 멤버는 자동으로 Azure 수신 통해 자신의 Visual Studio Ultimate with MSDN 구독 혜택</span><span class="sxs-lookup"><span data-stu-id="e2fdd-143">[BizSpark](http://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="e2fdd-144">멤버는 [Microsoft 파트너 네트워크](http://aka.ms/watk-mpn) Cloud Essentials 프로그램 수신 비용 없이 월간 Azure 크레딧</span><span class="sxs-lookup"><span data-stu-id="e2fdd-144">Members of the [Microsoft Partner Network](http://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="e2fdd-145">설정</span><span class="sxs-lookup"><span data-stu-id="e2fdd-145">Setup</span></span>

<span data-ttu-id="e2fdd-146">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-146">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="e2fdd-147">Windows 탐색기를 열고에 랩 찾아보기 **소스** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-147">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="e2fdd-148">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택 **관리자 권한으로 실행** 환경을 구성 되며이 랩에 대 한 Visual Studio 코드 조각을 설치 하는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-148">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="e2fdd-149">사용자 계정 컨트롤 대화 상자가 표시 하 고, 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-149">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="e2fdd-150">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-150">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="e2fdd-151">코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e2fdd-151">Using the Code Snippets</span></span>

<span data-ttu-id="e2fdd-152">랩 문서를 통해 코드 블록을 삽입 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-152">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="e2fdd-153">사용자 편의 위해이 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-153">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="e2fdd-154">각 연습에는 시작 솔루션 동반 되는 **시작** 개별적으로 각 연습에 따라 할 수 있는 작업의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-154">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="e2fdd-155">주의 하십시오 연습 하는 동안 추가 된 코드 조각은 솔루션 시작이 항목에서 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-155">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="e2fdd-156">실행에 대 한 소스 코드에서 찾아볼 수 있습니다는 **끝** 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-156">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="e2fdd-157">이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-157">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="e2fdd-158">연습</span><span class="sxs-lookup"><span data-stu-id="e2fdd-158">Exercises</span></span>

<span data-ttu-id="e2fdd-159">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-159">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="e2fdd-160">Entity Framework 마이그레이션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e2fdd-160">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="e2fdd-161">스테이징 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e2fdd-161">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="e2fdd-162">프로덕션 환경에서 배포 Rollback을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-162">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="e2fdd-163">Azure 저장소를 사용 하 여 배율을</span><span class="sxs-lookup"><span data-stu-id="e2fdd-163">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="e2fdd-164">[웹 앱에 대 한 자동 크기 조정을 사용할](#Exercise5) (Visual Studio 2013 Ultimate edition에 대 한 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="e2fdd-164">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="e2fdd-165">예상 소요 시간: **75 분**</span><span class="sxs-lookup"><span data-stu-id="e2fdd-165">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="e2fdd-166">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-166">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="e2fdd-167">미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-167">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="e2fdd-168">이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-168">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="e2fdd-169">개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-169">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="e2fdd-170">연습 1: Entity Framework 마이그레이션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e2fdd-170">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="e2fdd-171">응용 프로그램을 개발 하는 데이터 모델에는 시간이 지남에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-171">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="e2fdd-172">(새 버전을 만드는) 하는 경우 이러한 변경 내용은 기존 모델 데이터베이스에 영향을 줄 수 및 데이터베이스를 오류를 방지 하려면 최신 상태로 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-172">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="e2fdd-173">사용자의 모델에 이러한 변경의 추적을 간소화 하기 위해 **Entity Framework Code First 마이그레이션을** 자동으로 데이터베이스 스키마를 사용 하 여 모델을 비교 하는 변경 내용을 검색 하 고 데이터베이스를 업데이트 하는 특정 코드를 생성 합니다. 새로 만들기 *버전* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-173">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="e2fdd-174">이 연습을 사용 하도록 설정 하는 방법을 보여 줍니다. **마이그레이션** 응용 프로그램을 쉽게 검색 하는 방법을 사용자 데이터베이스를 업데이트 하도록 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-174">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="e2fdd-175">작업 1-사용 하도록 설정 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e2fdd-175">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="e2fdd-176">사용 하도록 설정 하는 단계를 진행 합니다이 태스크에서는 **Entity Framework Code First 마이그레이션을** 에 **들은 퀴즈** 데이터베이스, 모델을 변경 하 고에서 이러한 변경 내용이 반영 하는 방법을 이해는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-176">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="e2fdd-177">Visual Studio를 열고 열기는 **GeekQuiz.sln** 에서 솔루션 파일 **Source\Ex1 UsingEntityFrameworkMigrations\Begin**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-177">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="e2fdd-178">다운로드 및 설치 하기 위해 솔루션을 빌드하는 **NuGet** 패키지 종속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-178">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="e2fdd-179">이렇게 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **솔루션 빌드** 하거나 키를 눌러 **Ctrl + Shift + B**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-179">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="e2fdd-180">**도구** 선택 Visual Studio에서 메뉴 **라이브러리 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-180">From the **Tools** menu in Visual Studio, select **Library Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="e2fdd-181">에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-181">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="e2fdd-182">기존 모델을 기반으로 하는 초기 마이그레이션 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-182">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="e2fdd-183">![마이그레이션을 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "마이그레이션을 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-183">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="e2fdd-184">*마이그레이션을 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-184">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-185">이 명령은 추가 **마이그레이션** 파일을 포함 하 게 퀴즈 프로젝트에이 폴더의 이름은 **Configuration.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-185">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="e2fdd-186">**구성** 클래스를 사용 하 여 컨텍스트에 대 한 마이그레이션 작동 하는 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-186">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="e2fdd-187">마이그레이션을 사용 하도록 설정, 업데이트 해야는 **구성** 초기 데이터에 데이터베이스를 채우는 클래스는 **들은 퀴즈** 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-187">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="e2fdd-188">아래 **마이그레이션**, 대체는 **Configuration.cs** 와 파일에 있는 **Source\Assets** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-188">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-189">이후 **마이그레이션** 호출 됩니다는 **시드** 레코드가 데이터베이스에 중복 되지 있는지 확인 해야 하는 모든 데이터베이스 업데이트 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-189">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="e2fdd-190">**AddOrUpdate** 방법은 중복 데이터 방지 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-190">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="e2fdd-191">초기 마이그레이션을 추가 하려면 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-191">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-192">명명 된 데이터베이스가 없습니다. 인지 확인 &quot;GeekQuizProd&quot; 여 LocalDB 인스턴스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-192">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="e2fdd-193">![기본 스키마 마이그레이션 추가](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "추가 기본 스키마 마이그레이션")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-193">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="e2fdd-194">*기본 스키마 마이그레이션 추가*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-194">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-195">**추가 마이그레이션** 마지막 마이그레이션 만들어진 후 모델에 대 한 변경 내용에 따라 다음 마이그레이션을 스 캐 폴드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-195">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="e2fdd-196">이 경우 프로젝트의 첫 번째 마이그레이션 이기에 정의 된 모든 테이블을 만드는 스크립트를 추가 되는 **TriviaContext** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-196">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="e2fdd-197">다음 명령을 실행 하 여 데이터베이스를 업데이트 하려면 마이그레이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-197">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="e2fdd-198">이 명령에 지정 합니다는 **Verbose** 플래그 대상 데이터베이스에 적용 중인 SQL 문을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-198">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="e2fdd-199">![초기 데이터베이스 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "초기 데이터베이스 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-199">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="e2fdd-200">*초기 데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-200">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-201">**데이터베이스 업데이트** 보류 중인 마이그레이션을 데이터베이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-201">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="e2fdd-202">이 경우 web.config 파일에 정의 된 연결 문자열을 사용 하 여 데이터베이스를 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-202">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="e2fdd-203">로 이동 **보기** 메뉴를 열고 다음 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-203">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="e2fdd-204">![SQL Server 개체 탐색기에서 열기](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server 개체 탐색기에서 열기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-204">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="e2fdd-205">*SQL Server 개체 탐색기에서 열기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-205">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="e2fdd-206">에 **SQL Server 개체 탐색기** 창에서 마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스를 연결할는 **SQL Server** 노드를 선택 하 고 **SQL Server 추가...**  옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-206">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="e2fdd-207">![SQL Server 인스턴스를 추가](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server 인스턴스를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-207">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="e2fdd-208">*SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-208">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="e2fdd-209">설정의 **서버 이름** 를 *(localdb) \v11.0* 둡니다 **Windows 인증** 인증 모드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-209">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="e2fdd-210">클릭 **연결** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-210">Click **Connect** to continue.</span></span>

    <span data-ttu-id="e2fdd-211">![LocalDB에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB에 연결")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-211">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="e2fdd-212">*LocalDB에 연결*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-212">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="e2fdd-213">열기는 **GeekQuizProd** 데이터베이스를 확장 하 고는 **테이블** 노드.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-213">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="e2fdd-214">볼 수 있듯이 **Update-database** 명령이 생성에 정의 된 모든 테이블의 **TriviaContext** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-214">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="e2fdd-215">찾기의 **dbo입니다. TriviaQuestions** 테이블 및 열 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-215">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="e2fdd-216">다음 태스크에서는이 테이블에 새 열 추가 사용 하 여 데이터베이스를 업데이트 **마이그레이션**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-216">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="e2fdd-217">![Trivia 질문 열](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia 질문 열")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-217">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="e2fdd-218">*Trivia 질문 열*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-218">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="e2fdd-219">작업 2-마이그레이션을 사용 하 여 데이터베이스 스키마를 업데이트</span><span class="sxs-lookup"><span data-stu-id="e2fdd-219">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="e2fdd-220">이 작업을 사용 하 여 **Entity Framework Code First 마이그레이션을** 하 모델 변경 사항을 검색 하 고 데이터베이스를 업데이트 하는 데 필요한 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-220">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="e2fdd-221">업데이트 하는 **TriviaQuestions** 새 속성을 추가 하 여 엔터티.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-221">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="e2fdd-222">다음 테이블에 새 열을 포함 하는 새 마이그레이션 만들려면 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-222">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="e2fdd-223">**솔루션 탐색기**, 두 번 클릭는 **TriviaQuestion.cs** 내에 있는 파일의 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-223">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="e2fdd-224">라는 새 속성이 추가 **힌트**다음 코드 조각에서와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-224">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="e2fdd-225">에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-225">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="e2fdd-226">새 마이그레이션 부문의 변경을 반영 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-226">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="e2fdd-227">![추가 마이그레이션](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "추가 마이그레이션")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-227">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="e2fdd-228">*추가 마이그레이션*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-228">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-229">두 가지 방법으로 구성 된 마이그레이션 파일 **를** 및 **아래로**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-229">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    > 
    > - <span data-ttu-id="e2fdd-230">**를** 메서드를 사용 하 여 현재 버전의 응용 프로그램 해야 데이터베이스에 적용할 변경 내용을 지정할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-230">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="e2fdd-231">**아래로** 에 추가한 변경 내용이 되돌리는 것 하는 데 사용 되는 **를** 메서드.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-231">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    > 
    > <span data-ttu-id="e2fdd-232">타임 스탬프 순서 및 마지막 업데이트 이후 사용 되지 않은 하는 항목만에서 모든 마이그레이션 데이터베이스 마이그레이션 데이터베이스를 업데이트할 때 실행 됩니다 (의 \_적용 된 마이그레이션이 어떤 MigrationHistory 테이블의 추적).</span><span class="sxs-lookup"><span data-stu-id="e2fdd-232">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="e2fdd-233">**를** 모든 마이그레이션의 메서드는 호출 되 고 데이터베이스에 앞서 지정한 같이 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-233">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="e2fdd-234">이전 마이그레이션이으로 다시 돌아가십시오 계속 사용 하려면 우리는 **아래로** 메서드를 호출 하 여 반대 순서로 변경 내용을 다시 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-234">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="e2fdd-235">에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-235">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="e2fdd-236">출력은 **Update-database** 생성 된 명령을 **Alter Table** SQL 문이 새 열을 추가 하는 **TriviaQuestions** 아래 이미지에 나와 있는 것 처럼 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-236">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="e2fdd-237">![열의 SQL 문을 생성 추가](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "열 SQL 문을 생성 된 추가")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-237">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="e2fdd-238">*추가 열 SQL 문 생성*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-238">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="e2fdd-239">**SQL Server 개체 탐색기**, 새로 고침의 **dbo입니다. TriviaQuestions** 테이블을 확인 하는 새 **힌트** 열이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-239">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="e2fdd-240">![새 힌트 열을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "새 힌트 열 표시")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-240">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="e2fdd-241">*새 힌트 열 표시*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-241">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="e2fdd-242">에 **TriviaQuestion.cs** 편집기를 추가 **StringLength** 제약 조건에는 *힌트* 속성을 다음 코드 조각에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-242">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="e2fdd-243">에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-243">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="e2fdd-244">에 **패키지 관리자 콘솔**다음 명령을 입력 한 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-244">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="e2fdd-245">출력은 **Update-database** 생성 된 명령을 **Alter Table** SQL 문을 업데이트 하는 *힌트* 열 유형의 **TriviaQuestions** 아래 이미지에 나와 있는 것 처럼 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-245">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="e2fdd-246">![Alter column SQL 문에서 생성 된](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 문에서 생성")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-246">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="e2fdd-247">*Alter column SQL 문에서 생성*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-247">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="e2fdd-248">**SQL Server 개체 탐색기**, 새로 고침의 **dbo입니다. TriviaQuestions** 테이블을 확인 하 고 **힌트** 열 형식이 **nvarchar(150)**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-248">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="e2fdd-249">![새 제약 조건을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "새 제약 조건을 보여 주는")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-249">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="e2fdd-250">*새 제약 조건을 보여 주는*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-250">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="e2fdd-251">스테이징 웹 앱을 배포 하는 연습 2:</span><span class="sxs-lookup"><span data-stu-id="e2fdd-251">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="e2fdd-252">**Azure 앱 서비스에서 앱을 웹** 준비 된 게시를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-252">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="e2fdd-253">준비 된 게시의 각 기본 프로덕션 사이트에 대 한 준비 사이트 슬롯을 만들고 작동 중단 시간 없이 이러한 슬롯을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-253">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="e2fdd-254">공개적으로 해제 하기 전에 변경 내용 유효성 검사, 점차 사이트 콘텐츠를 통합 하 고 변경 내용을 정상적으로 작업할 경우 롤백될에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-254">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="e2fdd-255">이 연습에서는 배포는 **들은 퀴즈** Git 소스 제어를 사용 하 여 웹 응용 프로그램의 스테이징 환경에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-255">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="e2fdd-256">이렇게 하려면 웹 앱 만들기 및 관리 포털에서 필수 구성 요소를 프로 비전를 하는 구성 된 **Git** 리포지토리 및 응용 프로그램을 푸시 하도록 소스 코드를 로컬 컴퓨터에서 스테이징 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-256">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="e2fdd-257">또한와 프로덕션 데이터베이스를 업데이트 합니다는 **Code First 마이그레이션을** 이전 연습에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-257">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="e2fdd-258">그런 다음 해당 작업을 확인 하려면이 테스트 환경에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-258">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="e2fdd-259">했으면 한다는 예상에 따라 작동, 프로덕션 환경에 응용 프로그램을 승격 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-259">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="e2fdd-260">준비 된 게시를 활성화 하려면 웹 응용 프로그램에 있어야 **표준 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-260">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="e2fdd-261">Note를 표준 모드로 웹 앱을 변경 하는 경우 추가 비용이 발생에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-261">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="e2fdd-262">가격에 대 한 자세한 내용은 참조 [앱 서비스 가격 책정](https://azure.microsoft.com/en-us/pricing/details/app-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-262">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span>


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="e2fdd-263">1 – Azure 앱 서비스에서 웹 앱을 만드는 작업</span><span class="sxs-lookup"><span data-stu-id="e2fdd-263">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="e2fdd-264">이 태스크에서는의 웹 앱을 만들 **Azure 앱 서비스** 관리 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-264">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="e2fdd-265">또한 구성한는 **SQL 데이터베이스** 응용 프로그램 데이터를 유지 하 고 소스 제어에 대 한 로컬 Git 리포지토리를 구성 하려면.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-265">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="e2fdd-266">이동 하 여 [Azure 관리 포털](https://manage.windowsazure.com) 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-266">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![Azure 관리 포털에 로그인](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="e2fdd-268">*Azure 관리 포털에 로그인*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-268">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="e2fdd-269">클릭 **새로** 페이지의 맨 아래에 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-269">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="e2fdd-270">![새 웹 앱을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "새 웹 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-270">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="e2fdd-271">*새 웹 앱 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-271">*Creating a new web app*</span></span>
3. <span data-ttu-id="e2fdd-272">클릭 **계산**, **웹 사이트** 차례로 **사용자 지정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-272">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="e2fdd-273">![사용자 지정 만들기를 사용 하 여 새 웹 앱을 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-273">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="e2fdd-274">*사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-274">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="e2fdd-275">에 **새 웹 사이트-사용자 지정 만들기** 대화 상자를 사용 가능한 제공 **URL** (예: *들은 퀴즈*), 위치를 선택는 **영역** 드롭다운 목록 및 선택 **새 SQL 데이터베이스 만들기** 에 **데이터베이스** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-275">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="e2fdd-276">마지막으로 선택 된 **소스 제어에서 게시** 확인란과 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-276">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![새 웹 앱을 사용자 지정](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="e2fdd-278">*새 웹 앱을 사용자 지정*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-278">*Customizing the new web app*</span></span>
5. <span data-ttu-id="e2fdd-279">데이터베이스 설정에 대 한 다음 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-279">Specify the following information for the database settings:</span></span>

    - <span data-ttu-id="e2fdd-280">에 **이름** 텍스트 상자에 데이터베이스 이름을 입력 합니다 (예: *geekquiz\_db*)</span><span class="sxs-lookup"><span data-stu-id="e2fdd-280">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
    - <span data-ttu-id="e2fdd-281">서버에서 **드롭 다운** 목록에서 **새 SQL 데이터베이스 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-281">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="e2fdd-282">또는 기존 서버를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-282">Alternatively, you can select an existing server.</span></span>
    - <span data-ttu-id="e2fdd-283">에 **데이터베이스 사용자 이름** 및 **데이터베이스 암호** 상자 SQL 데이터베이스 서버에 대 한 관리자 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-283">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="e2fdd-284">서버를 선택 하면 이미 만든 경우 암호를 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-284">If you select a server you have already created, you will be prompted for the password.</span></span>

    ![데이터베이스 설정 지정](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

    <span data-ttu-id="e2fdd-286">*데이터베이스 설정 지정*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-286">*Specifying the database settings*</span></span>
6. <span data-ttu-id="e2fdd-287">**다음** 을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-287">Click **Next** to continue.</span></span>
7. <span data-ttu-id="e2fdd-288">선택 **로컬 Git 리포지토리** 사용 하 고 클릭 하 여 소스 제어에 대 한 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-288">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-289">배포 자격 증명 (사용자 이름 및 암호)에 대 한 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-289">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![Git 리포지토리를 만드는 중](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="e2fdd-291">*Git 리포지토리를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-291">*Creating the Git repository*</span></span>
8. <span data-ttu-id="e2fdd-292">새 웹 앱을 만들 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-292">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-293">기본적으로 Azure에서 도메인을 제공 *azurewebsites.net* 아니지만 Azure 관리 포털을 사용 하 여 사용자 지정 도메인을 설정 하려면 가능성도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-293">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="e2fdd-294">그러나 특정 Azure 앱 서비스 모드를 사용 하는 경우 사용자 지정 도메인에 관리할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-294">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    > 
    > <span data-ttu-id="e2fdd-295">Azure 앱 서비스는 무료, 공유, Basic, Standard 및 Premium edition에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-295">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="e2fdd-296">무료 및 공유 모드에서는 모든 웹 앱 다중 테 넌 트 환경에서 실행 하 고 CPU, 메모리 및 네트워크 사용량에 대 한 할당량이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-296">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="e2fdd-297">무료 앱의 최대 수는 계획 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-297">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="e2fdd-298">표준 모드에서는 표준 Azure에 해당 하는 전용된 가상 컴퓨터에서 실행 되는 앱 리소스를 계산 하는 것이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-298">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="e2fdd-299">웹 응용 프로그램 모드 구성에서 찾을 수 있습니다는 **배율** 웹 응용 프로그램의 메뉴.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-299">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    > 
    > <span data-ttu-id="e2fdd-300">![Azure 앱 서비스 모드](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure 앱 서비스 모드")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-300">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    > 
    > <span data-ttu-id="e2fdd-301">사용 중인 경우 **Shared** 또는 **표준** 응용 프로그램으로 이동 하 여 웹 앱에 대 한 사용자 지정 도메인을 관리할 수 있는 모드 **구성** 를클릭하고메뉴**도메인 관리** 아래 *도메인 이름*합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-301">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    > 
    > <span data-ttu-id="e2fdd-302">![도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "도메인 관리")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-302">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    > 
    > <span data-ttu-id="e2fdd-303">![사용자 지정 도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "사용자 지정 도메인 관리")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-303">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="e2fdd-304">웹 응용 프로그램을 만든 후 아래의 링크를 클릭는 **URL** 열을 새 웹 응용 프로그램이 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-304">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![새 웹 앱을 검색합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="e2fdd-306">*새 웹 앱을 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-306">*Browsing to the new web app*</span></span>

    ![웹 앱이 실행 중인](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="e2fdd-308">*웹 앱이 실행 중인*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-308">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="e2fdd-309">작업 2-프로덕션 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e2fdd-309">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="e2fdd-310">이 작업을 사용 하 여는 **Entity Framework Code First 마이그레이션을** 를 대상으로 데이터베이스를 만들려면는 **Azure SQL 데이터베이스** 이전 태스크에서 만든 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-310">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="e2fdd-311">관리 포털에서 이전 태스크에서 만든 웹 앱으로 이동 하 고 이동 해당 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-311">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="e2fdd-312">에 **대시보드** 페이지 **연결 문자열 보기** 링크는 **눈에 보는** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-312">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="e2fdd-313">![연결 문자열 보기](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "연결 문자열 보기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-313">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="e2fdd-314">*연결 문자열을 봅니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-314">*View connection strings*</span></span>
3. <span data-ttu-id="e2fdd-315">복사는 **연결 문자열** 값 및 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-315">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="e2fdd-316">![Azure 관리 포털에서 연결 문자열](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 관리 포털에서 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-316">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="e2fdd-317">*Azure 관리 포털에서 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-317">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="e2fdd-318">클릭 **SQL 데이터베이스** Azure의 SQL 데이터베이스의 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="e2fdd-318">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="e2fdd-319">![SQL 데이터베이스 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL 데이터베이스 메뉴")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-319">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="e2fdd-320">*SQL 데이터베이스 메뉴*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-320">*SQL Database menu*</span></span>
5. <span data-ttu-id="e2fdd-321">이전 태스크에서 만든 데이터베이스를 찾아 서버의 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-321">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="e2fdd-322">![SQL 데이터베이스 서버](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL 데이터베이스 서버")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-322">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="e2fdd-323">*SQL 데이터베이스 서버*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-323">*SQL Database server*</span></span>
6. <span data-ttu-id="e2fdd-324">에 **빠른 시작** 페이지에서 클릭 하 고 서버의 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-324">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="e2fdd-325">![구성 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "구성 메뉴")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-325">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="e2fdd-326">*메뉴 구성*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-326">*Configure menu*</span></span>
7. <span data-ttu-id="e2fdd-327">에 **허용 IP 주소** 섹션에서 클릭 **허용된 IP 주소에 추가** 링크 IP SQL 데이터베이스 서버에 연결 하는 데 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-327">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="e2fdd-328">![허용 된 IP 주소](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "허용 IP 주소")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-328">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="e2fdd-329">*허용 된 IP 주소*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-329">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="e2fdd-330">클릭 **저장** 단계를 완료 하려면 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-330">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="e2fdd-331">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-331">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="e2fdd-332">에 **패키지 관리자 콘솔**, 대체 하는 다음 명령을 실행 *[귀하가 연결 문자열]* Azure에서 복사한 연결 문자열과 함께 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="e2fdd-332">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="e2fdd-333">![Windows Azure SQL 데이터베이스를 대상으로 지정 된 데이터베이스 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL 데이터베이스를 대상으로 지정 된 데이터베이스 업데이트")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-333">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="e2fdd-334">*Azure SQL 데이터베이스를 대상으로 하는 데이터베이스를 업데이트 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-334">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="e2fdd-335">작업 3 – Git를 사용 하 여 스테이징 배포 들은 퀴즈</span><span class="sxs-lookup"><span data-stu-id="e2fdd-335">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="e2fdd-336">이 태스크에서는 웹 응용 프로그램에서 준비 된 게시를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-336">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="e2fdd-337">그런 다음는 들은 퀴즈 응용 프로그램을 게시할 로컬 컴퓨터에서 직접 웹 응용 프로그램의 스테이징 환경에 Git를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-337">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="e2fdd-338">대상 웹 응용 프로그램의 이름을 클릭 하 고 다시 포털로 이동는 **이름** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-338">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![웹 응용 프로그램 관리 페이지 열기](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="e2fdd-340">*웹 응용 프로그램 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-340">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="e2fdd-341">로 이동 된 **배율** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-341">Navigate to the **Scale** page.</span></span> <span data-ttu-id="e2fdd-342">아래는 **일반** 섹션에서 **표준** 구성과 클릭에 대 한 **저장** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-342">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-343">현재 지역 및 구독에서 모든 웹 앱을 실행 하려면 **표준** 모드, 범위 밖의 **모두 선택** 확인란을 선택는 **사이트 선택** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-343">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="e2fdd-344">그렇지 않은 경우의 선택을 취소는 **모두 선택** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-344">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="e2fdd-345">![웹 앱을 표준 모드로 업그레이드](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "를 표준 모드로 웹 응용 프로그램 업그레이드")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-345">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="e2fdd-346">*웹 앱을 표준 모드로 업그레이드*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-346">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="e2fdd-347">클릭 **예** 하 여 변경 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-347">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="e2fdd-348">![표준 모드로 변경 내용을 확인](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "웹 응용 프로그램 모드를 변경 하 여 계속 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-348">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="e2fdd-349">*표준 모드에 대 한 변경 확인*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-349">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="e2fdd-350">이동 하는 **대시보드** 페이지 클릭 하 여 **사용 준비 게시** 아래는 **눈에 보는** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-350">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="e2fdd-351">![준비 된 게시를 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "사용 하도록 설정 하면 게시 준비")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-351">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="e2fdd-352">*준비 된 게시를 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-352">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="e2fdd-353">클릭 **예** 준비 된 게시를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-353">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="e2fdd-354">![준비 된 게시 확인](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "준비 된 게시를 사용 하도록 설정 하려면 예 클릭")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-354">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="e2fdd-355">*준비 된 게시를 확인합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-355">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="e2fdd-356">웹 응용 프로그램의 목록에서 준비 사이트 슬롯을 표시 하 여 웹 응용 프로그램 이름 왼쪽에 있는 표시를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-356">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="e2fdd-357">다음 웹 앱 이름이 ***(준비)***합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-357">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="e2fdd-358">준비 사이트 관리 페이지로 이동 하려면 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-358">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="e2fdd-359">![스테이징 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "스테이징 웹 앱으로 이동")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-359">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="e2fdd-360">*준비 응용 프로그램으로 이동*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-360">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="e2fdd-361">다른 모든 웹 앱의 관리 페이지 처럼 보이는 해당 그 관리 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-361">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="e2fdd-362">로 이동 된 **배포** 페이지 및 복사는 **Git URL** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-362">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="e2fdd-363">이 연습에서는 나중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-363">You will use it later in this exercise.</span></span>

    ![Git URL 값 복사](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="e2fdd-365">*Git URL 값 복사*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-365">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="e2fdd-366">새 **Git Bash** 콘솔을 통해 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-366">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="e2fdd-367">업데이트는 *[귀하가 응용 프로그램 경로]* 자리 표시자에 대 한 경로 **GeekQuiz** 에 있는 솔루션의 **Source\Ex1 DeployingWebSiteToStaging\Begin** 의 폴더 이 랩에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-367">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 초기화 및 첫 번째 커밋](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="e2fdd-369">*Git 초기화 및 첫 번째 커밋*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-369">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="e2fdd-370">원격 웹 앱 밀어 넣으려면 다음 명령을 실행 **Git** 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-370">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="e2fdd-371">관리 포털에서 가져온 URL 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-371">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="e2fdd-372">배포 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-372">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure에 강제 설치](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="e2fdd-374">*Azure에 강제 설치*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-374">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-375">FTP 호스트 또는 웹 응용 프로그램의 GIT 리포지토리에 콘텐츠를 배포할 때 사용 하 여 인증 해야 합니다는 **배포 자격 증명** 웹 앱에서 만든 **빠른 시작** 또는 **대시보드**  관리 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-375">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="e2fdd-376">배포 자격 증명을 사용 하 여 알 수 없는 경우 관리 포털을 사용 하 여 쉽게 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-376">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="e2fdd-377">웹 앱을 열고 **대시보드** 페이지를 클릭 하 고는 **배포 자격 증명 재설정** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-377">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="e2fdd-378">새 암호를 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-378">Provide a new password and click **OK**.</span></span> <span data-ttu-id="e2fdd-379">배포 자격 증명은 구독과 연결 된 모든 웹 앱과 함께 사용 하기에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-379">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="e2fdd-380">Azure에 성공적으로 푸시된 웹 앱을 확인 하기 위해 다시 관리 포털로 이동 하 고 클릭 **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-380">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="e2fdd-381">웹 앱을 찾아 준비 사이트 슬롯을 표시 하려면 항목을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-381">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="e2fdd-382">클릭 하 여 해당 **이름** 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-382">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="e2fdd-383">클릭 **배포** 볼 수는 **배포 기록을**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-383">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="e2fdd-384">되는지 확인 한 **활성 배포** 와 프로그램  *&quot;초기 커밋&quot;*합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-384">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![활성 배포](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="e2fdd-386">*활성 배포*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-386">*Active deployment*</span></span>
13. <span data-ttu-id="e2fdd-387">마지막으로, 클릭 **찾아보기** 웹 앱으로 이동 하려면 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-387">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![웹 앱을 찾아보기](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="e2fdd-389">*웹 앱을 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-389">*Browse web app*</span></span>
14. <span data-ttu-id="e2fdd-390">응용 프로그램을 성공적으로 배포한 경우 들은 퀴즈 로그인 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-390">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-391">배포 응용 프로그램의 주소 URL 뒤 웹 응용 프로그램의 이름을 포함 *-준비*합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-391">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![스테이징 환경에서 실행 중인 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="e2fdd-393">*스테이징 환경에서 실행 중인 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-393">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="e2fdd-394">클릭 하 여 응용 프로그램을 탐색 하려면 **등록** 에 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-394">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="e2fdd-395">사용자 이름, 전자 메일 주소 및 암호를 입력 하 여 계정 세부 정보를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-395">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="e2fdd-396">다음으로 응용 프로그램에서는 퀴즈의 첫 번째 질문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-396">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="e2fdd-397">예상 대로 작동 하는지 확인 하는 몇 가지 질문에 답변 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-397">Answer a few questions to make sure it is working as expected.</span></span>

    ![응용 프로그램을 사용할 준비가 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="e2fdd-399">*응용 프로그램을 사용할 준비가 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-399">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="e2fdd-400">작업 4-프로덕션 환경에 웹 응용 프로그램을 승격 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-400">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="e2fdd-401">스테이징 환경에서 웹 응용 프로그램이 제대로 작동 하는지 확인 하 고 이제 프로덕션으로 승격할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-401">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="e2fdd-402">이 태스크에서는 됩니다 프로덕션 사이트 슬롯으로 준비 사이트 슬롯을 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-402">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="e2fdd-403">관리 포털에 다시 이동 하 고 준비 사이트 슬롯을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-403">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="e2fdd-404">클릭 **교체** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-404">Click **Swap** in the command bar.</span></span>

    ![프로덕션 환경으로 교체 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="e2fdd-406">*프로덕션 환경으로 교체 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-406">*Swap to production*</span></span>
2. <span data-ttu-id="e2fdd-407">클릭 **예** 확인 대화 상자에서는 스왑 작업을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-407">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="e2fdd-408">Azure 됩니다 즉시 준비 사이트의 내용 사용 하 여 프로덕션 사이트의 콘텐츠를 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-408">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-409">준비 된 버전에서 일부 설정이 고 (예: 연결 문자열 재정의 처리기 매핑, 등), 프로덕션 버전에 자동으로 복사 될 수 있지만 (예: DNS 끝점, SSL 바인딩을 등)에 다른 설정은 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-409">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![스왑 작업을 확인합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="e2fdd-411">*스왑 작업을 확인합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-411">*Confirming swap operation*</span></span>
3. <span data-ttu-id="e2fdd-412">스왑 완료 되 면 프로덕션 슬롯을 선택 하 고 클릭 **찾아보기** 프로덕션 사이트를 열려면 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-412">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="e2fdd-413">주소 표시줄에 URL을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-413">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-414">캐시를 지우려면 브라우저를 새로 고쳐야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-414">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="e2fdd-415">Internet Explorer에서 할 수 있는이 키를 눌러 **CTRL + R**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-415">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![프로덕션 환경에서 실행 되는 웹 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="e2fdd-417">에 **GitBash** 콘솔에서 프로덕션 슬롯을 대상으로 로컬 Git 리포지토리에 대 한 원격 URL을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-417">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="e2fdd-418">이 위해 웹 응용 프로그램의 이름 및 프로그램 배포 사용자 이름 자리 표시자를 바꾸는 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-418">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-419">다음 실습에서 랩의 단순성에 대 한 스테이징 대신 프로덕션 사이트에 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-419">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="e2fdd-420">실제 시나리오에서 프로덕션으로 승격 하기 전에 스테이징 환경에 변경 내용을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-420">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="e2fdd-421">연습 3: 프로덕션 환경에서 배포 Rollback 수행</span><span class="sxs-lookup"><span data-stu-id="e2fdd-421">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="e2fdd-422">여기서 없는 핫 스왑 스테이징 및 프로덕션, 예를 들어 간에 수행 하려면 스테이징 슬롯으로 작업 하는 경우 시나리오 **무료** 또는 **Shared** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-422">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="e2fdd-423">이러한 시나리오에서 테스트 해야 테스트 환경에서 응용 프로그램-로컬 또는 원격 사이트에서-프로덕션 환경에 배포 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-423">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="e2fdd-424">그러나 있기 테스트 단계에서 검색 되지 문제가 프로덕션 사이트에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-424">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="e2fdd-425">이 경우 중요 한지 쉽게 응용 프로그램의 이전 및 더 안정 된 버전으로 최대한 빠르게 전환할 수 있는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-425">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="e2fdd-426">**Azure 앱 서비스**, 소스 제어에서 연속 배포 수 가능한 덕분에이 기술을 사용 하면는 **재배포** 관리 포털에서 사용할 수 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-426">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="e2fdd-427">Azure는 커밋이 리포지토리에 푸시와 관련 된 배포를 추적 하 고 이전 배포를 사용 하 여 언제 든 지 응용 프로그램을 다시 배포 하는 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-427">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="e2fdd-428">이 연습에서 코드에 대 한 변경 수행는 **들은 퀴즈** 가 의도적으로 삽입 하는 응용 프로그램을 *버그*합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-428">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="e2fdd-429">오류를 확인 하려면 프로덕션 환경에 응용 프로그램을 배포 합니다 및 다음의 이전 상태로 돌아가는 재배포 기능 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-429">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="e2fdd-430">작업 1-들은 퀴즈 응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="e2fdd-430">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="e2fdd-431">이 태스크의 코드의 작은 부분 리팩터링 됩니다는 **TriviaController** 클래스 새 메서드로 선택한 퀴즈 옵션은 데이터베이스에서 검색 하는 논리의 일부를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-431">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="e2fdd-432">사용 하 여 Visual Studio 인스턴스를 전환할는 **GeekQuiz** , 이전 연습에서 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-432">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="e2fdd-433">**솔루션 탐색기**열고는 **TriviaController.cs** 내 파일의 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-433">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="e2fdd-434">찾을 **StoreAsync** 메서드와 코드는 다음 그림에 강조 표시 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-434">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![코드를 선택합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="e2fdd-436">*코드를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-436">*Selecting the code*</span></span>
4. <span data-ttu-id="e2fdd-437">확장 하 고, 선택한 코드를 마우스 오른쪽 단추로 클릭는 **리팩터링** 메뉴와 선택 **메서드 추출...** .</span><span class="sxs-lookup"><span data-stu-id="e2fdd-437">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![새 메서드는 코드를 추출 하는 중](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="e2fdd-439">*추출 방법 선택*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-439">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="e2fdd-440">에 **메서드 추출** 대화 상자에 새 메서드 이름 *MatchesOption* 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-440">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![메서드 이름 지정](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="e2fdd-442">*추출 된 메서드에 대 한 이름 지정*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-442">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="e2fdd-443">그런 다음 선택한 코드 추출 되는 **MatchesOption** 메서드.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-443">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="e2fdd-444">결과 코드는 다음 코드 조각에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-444">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="e2fdd-445">키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-445">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="e2fdd-446">작업 2-들은 퀴즈 응용 프로그램을 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e2fdd-446">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="e2fdd-447">이제 프로덕션 환경에 새 배포를 트리거하는 리포지토리가 이전 태스크에서 변경한 내용을 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-447">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="e2fdd-448">사용 하 여 문제가 문제 해결은 그런 다음는 **F12 개발 도구** Internet Explorer에서 제공 하 고 다음 Azure 관리 포털에서 롤백 이전 배포를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-448">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="e2fdd-449">새 **Git Bash** Azure 앱 서비스에 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-449">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="e2fdd-450">Azure에 변경 내용을 푸시 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-450">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="e2fdd-451">업데이트는 *[귀하가 응용 프로그램 경로]* 자리 표시자에 대 한 경로 **GeekQuiz** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-451">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="e2fdd-452">배포 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-452">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Azure에 리팩터링된 코드를 강제 설치](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="e2fdd-454">*Azure에 리팩터링된 코드를 강제 설치*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-454">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="e2fdd-455">Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="e2fdd-455">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="e2fdd-456">이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-456">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="e2fdd-457">키를 눌러 **F12** 개발 도구를 시작 하려면는 **네트워크** 탭을 클릭는 **재생** 기록을 시작 하려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-457">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="e2fdd-458">![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "네트워크 기록 시작")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-458">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="e2fdd-459">*네트워크 기록 시작*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-459">*Starting network recording*</span></span>
5. <span data-ttu-id="e2fdd-460">퀴즈의 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-460">Select any option of the quiz.</span></span> <span data-ttu-id="e2fdd-461">아무 작업도 수행 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-461">You will see that nothing happens.</span></span>
6. <span data-ttu-id="e2fdd-462">에 **F12** 창, 해당 POST HTTP 요청 하는 항목 표시 HTTP **500** 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-462">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 오류](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="e2fdd-464">*HTTP 500 오류*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-464">*HTTP 500 error*</span></span>
7. <span data-ttu-id="e2fdd-465">선택 된 **콘솔** 탭 합니다. 오류 원인 세부 정보와 함께 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-465">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![기록 된 오류](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="e2fdd-467">*기록 된 오류*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-467">*Logged error*</span></span>
8. <span data-ttu-id="e2fdd-468">오류 세부 정보 부분을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-468">Locate the details part of the error.</span></span> <span data-ttu-id="e2fdd-469">명확 하 게,이 오류는 이전 단계에서 커밋된 하면 리팩터링 코드에 의해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-469">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="e2fdd-470">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-470">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="e2fdd-471">브라우저를 닫지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-471">Do not close the browser.</span></span>
10. <span data-ttu-id="e2fdd-472">로 이동 하는 새 브라우저 인스턴스에서 [Azure 관리 포털](https://manage.windowsazure.com) 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-472">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="e2fdd-473">선택 **웹 사이트** 연습 2에서 만든 웹 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-473">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="e2fdd-474">탐색 하 고 **배포** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-474">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="e2fdd-475">배포 기록에 모든 커밋을 수행에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-475">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![기존 배포의 목록](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="e2fdd-477">*기존 배포의 목록*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-477">*List of existing deployments*</span></span>
13. <span data-ttu-id="e2fdd-478">이전의 커밋을 선택 하 고 클릭 **재배포** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-478">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![이전의 커밋 다시 배포](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="e2fdd-480">*이전의 커밋 다시 배포*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-480">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="e2fdd-481">를 확인 하 라는 메시지가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-481">When prompted to confirm, click **Yes**.</span></span>

    ![재배포를 확인합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="e2fdd-483">웹 앱 및 키를 눌러 브라우저 인스턴스를 다시 배포 완료 되 면 전환 **CTRL + f 5를 눌러**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-483">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="e2fdd-484">옵션 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-484">Click any of the options.</span></span> <span data-ttu-id="e2fdd-485">전체 및 결과 이제 플립 애니메이션 걸립니다 (*/오*) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-485">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="e2fdd-486">(선택 사항) 전환 하는 **Git Bash** 콘솔을 이전 커밋을로 되돌리려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-486">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-487">이러한 명령에 잘못 된 커밋의 Git 리포지토리 모든 변경 내용을 실행 취소 하는 새 커밋이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-487">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="e2fdd-488">다음 azure에는 새 커밋을 사용 하 여 응용 프로그램 다시 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-488">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="e2fdd-489">연습 4: Azure 저장소를 사용 하 여 배율을</span><span class="sxs-lookup"><span data-stu-id="e2fdd-489">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="e2fdd-490">**Blob** 은 대량의 구조화 되지 않은 텍스트 또는 비디오, 오디오 및 이미지와 같은 이진 데이터를 저장 하는 가장 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-490">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="e2fdd-491">저장소에 응용 프로그램의 정적 콘텐츠를 이동, 이미지 또는 브라우저에 직접 문서를 이용 하 여 응용 프로그램을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-491">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="e2fdd-492">이 연습에서는 Blob 컨테이너에 응용 프로그램의 정적 콘텐츠를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-492">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="e2fdd-493">다음 추가 하려면 응용 프로그램을 구성 합니다는 **ASP.NET URL 재작성 규칙** 에 **Web.config** Blob 컨테이너에 콘텐츠를 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-493">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="e2fdd-494">작업 1 – Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e2fdd-494">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="e2fdd-495">이 작업을 관리 포털을 사용 하 여 새 저장소 계정을 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-495">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="e2fdd-496">로 이동 된 [Azure 관리 포털](https://manage.windowsazure.com) 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-496">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="e2fdd-497">선택 **새로 만들기 | 데이터 서비스 | 저장소 | 빠른 생성** 새 저장소 계정 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-497">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="e2fdd-498">선택한 계정에 대 한 고유한 이름을 입력 한 **지역** 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-498">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="e2fdd-499">클릭 **저장소 계정 만들기** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-499">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="e2fdd-500">![새 저장소 계정을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "새 저장소 계정 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-500">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="e2fdd-501">*새 저장소 계정 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-501">*Creating a new storage account*</span></span>
3. <span data-ttu-id="e2fdd-502">에 **저장소** 섹션에서 새 저장소 계정의 상태 바뀔 때까지 기다렸다가 *온라인* 다음 단계를 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-502">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="e2fdd-503">![만든 저장소 계정](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "만든 저장소 계정")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-503">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="e2fdd-504">*만든 저장소 계정*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-504">*Storage Account created*</span></span>
4. <span data-ttu-id="e2fdd-505">저장소 계정 이름을 클릭 한 다음 클릭는 **대시보드** 페이지 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-505">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="e2fdd-506">**대시보드** 페이지에서 계정과 응용 프로그램 내에서 사용할 수 있는 서비스 끝점의 상태에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-506">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="e2fdd-507">![저장소 계정 대시보드에 표시](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "저장소 계정 대시보드를 표시 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-507">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="e2fdd-508">*저장소 계정 대시보드를 표시합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-508">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="e2fdd-509">클릭는 **액세스 키 관리** 탐색 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-509">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="e2fdd-510">![선택 키 [관리] 단추](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "액세스 키 관리 단추")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-510">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="e2fdd-511">*관리 액세스 키 단추*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-511">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="e2fdd-512">에 **액세스 키 관리** 대화 상자, 복사는 **저장소 계정 이름** 및 **기본 액세스 키** 다음 연습에 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-512">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="e2fdd-513">그런 다음 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-513">Then, close the dialog box.</span></span>

    <span data-ttu-id="e2fdd-514">![관리 액세스 키 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "액세스 키 관리 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-514">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="e2fdd-515">*관리 액세스 키 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-515">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="e2fdd-516">작업 2-Azure Blob 저장소로 자산을 업로드 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-516">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="e2fdd-517">이 작업에서는 저장소 계정에 연결 하는 데 Visual Studio에서 서버 탐색기 창을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-517">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="e2fdd-518">그런 다음 blob 컨테이너를 만들고 들은 퀴즈 로고 파일을 컨테이너에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-518">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="e2fdd-519">사용 하 여 Visual Studio 인스턴스를 전환할는 **GeekQuiz** , 이전 연습에서 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-519">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="e2fdd-520">메뉴 모음에서 선택 **보기** 클릭 하 고 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-520">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="e2fdd-521">**서버 탐색기**를 마우스 오른쪽 단추로 클릭는 **Azure** 노드 선택한 **Azure에 연결...** . 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-521">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![Windows Azure에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="e2fdd-523">*Azure에 연결*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-523">*Connect to Azure*</span></span>
4. <span data-ttu-id="e2fdd-524">확장 된 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **저장소** 선택 **외부 저장소 연결...** .</span><span class="sxs-lookup"><span data-stu-id="e2fdd-524">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="e2fdd-525">에 **새 저장소 계정 추가** 대화 상자에 입력에서 **계정 이름** 및 **계정 키** 클릭 확인 하 고 이전 작업에서 얻은 **확인**.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-525">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![새 저장소 계정 대화 상자를 추가 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="e2fdd-527">*새 저장소 계정 대화 상자를 추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-527">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="e2fdd-528">저장소 계정 아래에 나타나야 합니다.는 **저장소** 노드.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-528">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="e2fdd-529">저장소 계정의 확장 하 고 마우스 오른쪽 단추로 클릭 **Blob** 선택 **Blob 컨테이너 만들기...** .</span><span class="sxs-lookup"><span data-stu-id="e2fdd-529">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="e2fdd-530">![Blob 컨테이너 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob 컨테이너 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-530">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="e2fdd-531">*Blob 컨테이너 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-531">*Create Blob Container*</span></span>
7. <span data-ttu-id="e2fdd-532">에 **Create Blob Container** 대화 상자, blob 컨테이너에 대 한 이름을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-532">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="e2fdd-533">![Blob 컨테이너 대화 상자 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob 컨테이너 만들기 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-533">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="e2fdd-534">*Blob 컨테이너 대화 상자 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-534">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="e2fdd-535">새 blob 컨테이너에 추가 해야는 **Blob** 노드.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-535">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="e2fdd-536">컨테이너를 공용 컨테이너에서 액세스 권한을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-536">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="e2fdd-537">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **이미지** 컨테이너와 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-537">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="e2fdd-538">![컨테이너 속성 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "컨테이너 속성 이미지")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-538">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="e2fdd-539">*컨테이너 속성 이미지*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-539">*Images container properties*</span></span>
9. <span data-ttu-id="e2fdd-540">에 **속성** 창의 설정는 **공용 읽기 액세스 권한을** 를 **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-540">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="e2fdd-541">![공용 읽기 권한 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "공용 읽기 권한 속성을 변경")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-541">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="e2fdd-542">*변경 되는 공용 읽기 권한 속성*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-542">*Changing public read access property*</span></span>
10. <span data-ttu-id="e2fdd-543">공용 액세스 속성을 변경 하려면 대화 상자가 나타나면 확실치 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-543">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="e2fdd-544">![Microsoft Visual Studio 경고](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 경고")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-544">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="e2fdd-545">*Microsoft Visual Studio 경고*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-545">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="e2fdd-546">**서버 탐색기**를 마우스 오른쪽 단추로 클릭는 **이미지** blob 컨테이너 및 선택 **Blob 컨테이너 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-546">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="e2fdd-547">![Blob 컨테이너 보기](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob 컨테이너 보기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-547">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="e2fdd-548">*Blob 컨테이너 보기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-548">*View Blob Container*</span></span>
12. <span data-ttu-id="e2fdd-549">이미지 컨테이너가 해야 새 창에서 열고는 항목이 없으면 범례가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-549">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="e2fdd-550">클릭는 **업로드** 아이콘 blob 컨테이너에 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-550">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="e2fdd-551">![항목이 없는 이미지 컨테이너가](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "항목이 없는 컨테이너 이미지")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-551">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="e2fdd-552">*항목이 없는 컨테이너 이미지*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-552">*Images container with no entries*</span></span>
13. <span data-ttu-id="e2fdd-553">에 **Blob 업로드** 대화 상자에서 이동 하는 **자산** 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-553">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="e2fdd-554">선택 된 **로고 big.png** 파일을 클릭 하 여 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-554">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="e2fdd-555">파일을 업로드할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-555">Wait until the file is uploaded.</span></span> <span data-ttu-id="e2fdd-556">업로드가 완료 되 면 이미지 컨테이너에 파일을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-556">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="e2fdd-557">파일 항목을 마우스 오른쪽 단추로 클릭 하 고 선택 **URL 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-557">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="e2fdd-558">![Blob URL을 복사](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "blob 파일 URL 복사")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-558">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="e2fdd-559">*Blob URL 복사*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-559">*Copy blob URL*</span></span>
15. <span data-ttu-id="e2fdd-560">Internet Explorer를 열고 URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-560">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="e2fdd-561">다음 이미지는 브라우저에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-561">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="e2fdd-562">![Windows Blob 저장소에서 big.png 로고 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "저장소에서 big.png 로고 이미지")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-562">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="e2fdd-563">*Azure Blob 저장소에서 big.png 로고 이미지*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-563">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="e2fdd-564">작업 3 – Azure Blob 저장소에서 정적 콘텐츠를 사용할 솔루션을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-564">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="e2fdd-565">이 태스크에서는 구성에서 **GeekQuiz** 이미지를 사용 하는 솔루션 Azure Blob 저장소에 업로드 (대신 웹 앱에 있는 이미지)에 ASP.NET URL 다시 쓰기 규칙을 추가 하 여는 **web.config**파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-565">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="e2fdd-566">Visual Studio에서 엽니다는 **Web.config** 내 파일의 **GeekQuiz** 프로젝트를 찾습니다는  **&lt;system.webServer&gt;**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-566">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="e2fdd-567">URL 재작성을 저장소 계정 이름 자리 표시자 업데이트 규칙을 추가 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-567">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="e2fdd-568">(코드 조각- *WebSitesInProduction-Ex4-UrlRewriteRule*)</span><span class="sxs-lookup"><span data-stu-id="e2fdd-568">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="e2fdd-569">URL 다시 쓰기는 들어오는 웹 요청을 가로채 고 다른 리소스에 요청을 리디렉션하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-569">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="e2fdd-570">규칙을 다시 작성 하는 URL 다시 쓰기 엔진은 리디렉션해야 하 고 요청을 리디렉션할 수 필요로 하는 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-570">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="e2fdd-571">두 문자열의 다시 쓰기 규칙이 구성 됩니다: 요청한 URL에서 찾을 패턴 (일반적으로 사용 정규식) 하는 경우, 사용 하 여 패턴을 바꿀 문자열을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-571">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="e2fdd-572">자세한 내용은 참조 [ASP.NET의 URL 다시 쓰기](https://msdn.microsoft.com/en-us/library/ms972974.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-572">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/en-us/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="e2fdd-573">키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-573">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="e2fdd-574">새 **Git Bash** Azure 앱 서비스에 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-574">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="e2fdd-575">Azure에 변경 내용을 푸시 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-575">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="e2fdd-576">업데이트는 *[귀하가 응용 프로그램 경로]* 자리 표시자에 대 한 경로 **GeekQuiz** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-576">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="e2fdd-577">배포 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-577">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure에 업데이트 배포](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="e2fdd-579">*Azure에 업데이트 배포*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-579">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="e2fdd-580">작업 4-확인</span><span class="sxs-lookup"><span data-stu-id="e2fdd-580">Task 4 – Verification</span></span>

<span data-ttu-id="e2fdd-581">이 작업을 사용 하 여 **Internet Explorer** 검색 하는 **들은 퀴즈** URL 재작성 이미지 작동 하 고에 대 한 규칙을 확인 하 고 응용 프로그램에 호스팅된 이미지 리디렉션됩니다 **Azure Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-581">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="e2fdd-582">Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="e2fdd-582">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="e2fdd-583">이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-583">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="e2fdd-584">![이미지와 들은 퀴즈 웹 앱을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "들은 퀴즈 웹 응용 프로그램을 이미지를 표시 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-584">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="e2fdd-585">*이미지와 들은 퀴즈 웹 앱을 표시합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-585">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="e2fdd-586">키를 눌러 **F12** 개발 도구를 시작 하려면는 **네트워크** 탭 하 고 기록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-586">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="e2fdd-587">![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "네트워크 기록 시작")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-587">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="e2fdd-588">*네트워크 기록 시작*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-588">*Starting network recording*</span></span>
3. <span data-ttu-id="e2fdd-589">키를 눌러 **CTRL + f 5를 눌러** 웹 페이지를 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-589">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="e2fdd-590">HTTP 요청에 대 한 페이지 로드가 완료 되 면 나타납니다는 **/img/logo-big.png** HTTP URL **301** (리디렉션) 결과 및 다른 요청에 대 한 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` http URL**200** 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-590">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="e2fdd-591">![URL 리디렉션 확인](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "리디렉션 개발 도구에 표시")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-591">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="e2fdd-592">*URL 리디렉션을 확인 하는 중*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-592">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="e2fdd-593">연습 5: 웹 앱에 대 한 자동 크기 조정 사용</span><span class="sxs-lookup"><span data-stu-id="e2fdd-593">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="e2fdd-594">이 연습은 선택 사항이 웹 부하에 대 한 지원 하므로 &amp; 성능 테스트 에서만 사용할 수 있는 **Visual Studio 2013 Ultimate Edition**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-594">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="e2fdd-595">대 한 자세한 내용은 특정 Visual Studio 2013 기능, 버전 비교 [여기](https://www.microsoft.com/visualstudio/eng/products/compare)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-595">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>


<span data-ttu-id="e2fdd-596">**Azure 앱 서비스 웹 앱** 실행 되는 웹 앱에 대 한 자동 크기 조정 기능을 제공 **표준 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-596">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="e2fdd-597">자동 크기 조정에는 부하에 따라 웹 응용 프로그램의 인스턴스 수를 자동으로 조정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-597">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="e2fdd-598">자동 크기 조정을 사용 하는 Azure 웹 앱의 CPU가 5 분 마다 한 번 확인 하 고 해당 시점에 필요한 만큼 인스턴스가 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-598">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="e2fdd-599">CPU 사용량이 낮은 경우 인스턴스가 제거 됩니다 두 시간 마다 한 번씩 웹 앱의 성능이 저하 되지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-599">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="e2fdd-600">구성 하는 데 필요한 단계를 진행 합니다이 연습에서는 **자동 크기 조정** 에 대 한 기능는 **들은 퀴즈** 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-600">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="e2fdd-601">인스턴스 업그레이드를 트리거할 응용 프로그램에서 충분 한 CPU 부하를 생성 하는 Visual Studio 부하 테스트를 실행 하 여이 기능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-601">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="e2fdd-602">작업 1-CPU 메트릭을 기반 구성 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e2fdd-602">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="e2fdd-603">이 작업에서는 연습 2에서 만든 웹 응용 프로그램에 대 한 자동 크기 조정 기능을 사용 하도록 설정 하려면 Azure 관리 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-603">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="e2fdd-604">에 [Azure 관리 포털](https://manage.windowsazure.com/)선택, **웹 사이트** 연습 2에서 만든 웹 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-604">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="e2fdd-605">로 이동 된 **배율** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-605">Navigate to the **Scale** page.</span></span> <span data-ttu-id="e2fdd-606">아래는 **용량** 섹션에서 **CPU** 에 대 한는 **메트릭 별 크기 조정** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-606">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-607">CPU 별 크기 조정, Azure 응용 프로그램 CPU 사용량을 변경 하는 경우 사용 하는 인스턴스 수를 동적으로 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-607">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="e2fdd-608">![CPU 별 크기 조정 하도록 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "자동 크기 조정에 대 한 CPU 메트릭을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-608">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="e2fdd-609">*CPU 별 크기 조정 선택*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-609">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="e2fdd-610">변경 된 **대상 CPU** 구성을 **20**-**40** %입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-610">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-611">이 범위는 웹 앱에 대 한 평균 CPU 사용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-611">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="e2fdd-612">Azure는 추가 하거나이 범위에 웹 앱을 유지 하도록 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-612">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="e2fdd-613">에 지정 된 최소 및 최대 크기 조정 시 사용 하는 인스턴스 수는 **인스턴스 수** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-613">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="e2fdd-614">위 또는 해당 제한을 벗어나서 azure 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-614">Azure will never go above or beyond that limit.</span></span>
    > 
    > <span data-ttu-id="e2fdd-615">기본 **대상 CPU** 값은이 랩의 목적에 대해서만 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-615">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="e2fdd-616">작은 값으로 CPU 범위를 구성 하 여 적당 한 로드 응용 프로그램에 배치 되 면 자동 크기 조정 트리거로 기회를 늘리고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-616">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="e2fdd-617">![대상 CPU 20%에서 40% 사이의 변경](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "20%에서 40% 사이의 CPU 대상 변경")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-617">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="e2fdd-618">*대상 CPU 20%에서 40% 사이의 변경*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-618">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="e2fdd-619">클릭 **저장** 변경 내용을 저장 하려면 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-619">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="e2fdd-620">작업 2-부하 테스트를 Visual Studio와 함께</span><span class="sxs-lookup"><span data-stu-id="e2fdd-620">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="e2fdd-621">이제 **자동 크기 조정** 되었습니다 구성 만듭니다는 **웹 성능 및 부하 테스트 프로젝트** 웹 앱에서 일부 CPU 부하를 생성 하기 위해 Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-621">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="e2fdd-622">열기 **Visual Studio Ultimate 2013** 선택 **파일 | 새로 만들기 | 프로젝트...**  새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-622">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="e2fdd-623">![새 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-623">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="e2fdd-624">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-624">*Creating a new project*</span></span>
2. <span data-ttu-id="e2fdd-625">에 **새 프로젝트** 대화 상자에서 **웹 성능 및 부하 테스트 프로젝트** 아래는 **Visual C# | 테스트** 탭 합니다. 있는지 확인 **.NET Framework 4.5** 은 프로젝트의 이름을 선택 하면 *WebAndLoadTestProject*, 선택는 **위치** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-625">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="e2fdd-626">![새 웹과 부하 테스트 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "새 웹과 부하 테스트 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-626">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="e2fdd-627">*새 웹과 부하 테스트 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-627">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="e2fdd-628">에 **WebTest1.webtest** 마우스 오른쪽 단추로 클릭는 **WebTest1** 노드와 클릭 **요청 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-628">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="e2fdd-629">![WebTest1에 요청 추가](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "WebTest1에 요청 추가")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-629">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="e2fdd-630">*WebTest1에 요청 추가*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-630">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="e2fdd-631">에 **속성** 창 새 요청 노드의 업데이트는 **Url** 웹 앱의 URL을 가리키도록 속성 (예:  *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ).</span><span class="sxs-lookup"><span data-stu-id="e2fdd-631">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="e2fdd-632">![Url 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url 속성을 변경")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-632">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="e2fdd-633">*Url 속성을 변경*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-633">*Changing the Url property*</span></span>
5. <span data-ttu-id="e2fdd-634">에 **WebTest1.webtest** 창을 마우스 오른쪽 단추로 클릭 **WebTest1** 클릭 **루프 추가...** .</span><span class="sxs-lookup"><span data-stu-id="e2fdd-634">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="e2fdd-635">![WebTest1에 루프 추가](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "WebTest1에 루프 추가")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-635">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="e2fdd-636">*WebTest1에 루프 추가*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-636">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="e2fdd-637">에 **루프에 조건부 규칙 추가 및 항목** 대화 상자는 **For 루프** 규칙 및 다음과 같은 속성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-637">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

    1. <span data-ttu-id="e2fdd-638">**종료 하는 값:** 1000</span><span class="sxs-lookup"><span data-stu-id="e2fdd-638">**Terminating value:** 1000</span></span>
    2. <span data-ttu-id="e2fdd-639">**컨텍스트 매개 변수 이름:** 반복기</span><span class="sxs-lookup"><span data-stu-id="e2fdd-639">**Context Parameter Name:** Iterator</span></span>
    3. <span data-ttu-id="e2fdd-640">**증분 값:** 1</span><span class="sxs-lookup"><span data-stu-id="e2fdd-640">**Increment Value:** 1</span></span>

    <span data-ttu-id="e2fdd-641">![For 루프 규칙을 선택 하 고 속성 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For 루프 규칙을 선택 하 고 속성 업데이트")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-641">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

    <span data-ttu-id="e2fdd-642">*For 루프 규칙을 선택 하 고 속성 업데이트*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-642">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="e2fdd-643">아래는 **루프의 항목** 섹션에서 루프에 대 한 첫 번째 및 마지막 항목 하기 위해 이전에 만든 요청을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-643">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="e2fdd-644">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-644">Click **OK** to continue.</span></span>

    <span data-ttu-id="e2fdd-645">![루프에 대 한 첫 번째 및 마지막 항목을 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "루프에 대 한 첫 번째 및 마지막 항목 선택")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-645">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="e2fdd-646">*루프에 대 한 첫 번째 및 마지막 항목 선택*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-646">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="e2fdd-647">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **WebAndLoadTestProject** 프로젝트를 확장 하 고는 **추가** 메뉴와 선택 **부하 테스트 중...** .</span><span class="sxs-lookup"><span data-stu-id="e2fdd-647">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="e2fdd-648">![부하 테스트 프로젝트에 추가 WebAndLoadTestProject](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject 프로젝트에 부하 테스트를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-648">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="e2fdd-649">*WebAndLoadTestProject 프로젝트에 부하 테스트를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-649">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="e2fdd-650">에 **부하 테스트 새로 만들기 마법사** 대화 상자를 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-650">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="e2fdd-651">![새 부하 테스트 마법사](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "부하 테스트 새로 만들기 마법사")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-651">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="e2fdd-652">*부하 테스트 새로 만들기 마법사*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-652">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="e2fdd-653">에 **시나리오** 페이지에서 **대기 시간을 사용 하지 않는** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-653">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="e2fdd-654">![대기 시간을 사용 하지 않는 Selecting](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "를 대기 시간을 사용 하지 않는 선택")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-654">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="e2fdd-655">*인지 시간 사용을 선택 하면*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-655">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="e2fdd-656">에 **부하 패턴** 페이지에서 다음 사항을 확인는 **일정 부하** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-656">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="e2fdd-657">변경의 **사용자 수** 설정을 **250** 사용자 및 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-657">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="e2fdd-658">![사용자 수가 250으로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "250 사용자 수를 변경 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-658">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="e2fdd-659">*사용자 수가 250으로 변경*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-659">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="e2fdd-660">에 **테스트 조합 모델** 페이지에서 **순차적 테스트 순서 기반** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-660">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="e2fdd-661">![테스트 조합 모델을 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "테스트 조합 모델 선택")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-661">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="e2fdd-662">*테스트 조합 모델 선택*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-662">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="e2fdd-663">에 **테스트 조합 모델** 페이지 **추가 중...**  조합에 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-663">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="e2fdd-664">![테스트 조합에 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "테스트 조합에 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-664">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="e2fdd-665">*테스트 조합에 테스트 추가*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-665">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="e2fdd-666">에 **테스트 추가** 대화 상자를 두 번 클릭 **WebTest1** 테스트를 추가 하는 **선택한 테스트** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-666">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="e2fdd-667">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-667">Click **OK** to continue.</span></span>

    <span data-ttu-id="e2fdd-668">![WebTest1 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "WebTest1 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-668">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="e2fdd-669">*WebTest1 테스트 추가*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-669">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="e2fdd-670">에 **테스트 조합** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-670">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="e2fdd-671">![완료 테스트 조합 페이지](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "완료 테스트 조합 페이지")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-671">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="e2fdd-672">*완료 테스트 조합 페이지*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-672">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="e2fdd-673">에 **네트워크 조합** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-673">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="e2fdd-674">![네트워크 조합 페이지에서 다음 클릭 하면](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "네트워크 조합 페이지에서 다음 클릭")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-674">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="e2fdd-675">*네트워크 조합 페이지에서 다음을 클릭 하면*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-675">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="e2fdd-676">에 **브라우저 조합** 페이지에서 **Internet Explorer 10.0** 브라우저의 종류와 클릭으로 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-676">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="e2fdd-677">![브라우저 종류를 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "브라우저 종류를 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-677">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="e2fdd-678">*브라우저 종류를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-678">*Selecting the browser type*</span></span>
18. <span data-ttu-id="e2fdd-679">에 **카운터 집합** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-679">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="e2fdd-680">![카운터 집합 페이지에서 다음을 클릭 하](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "카운터 집합 페이지에서 다음 클릭")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-680">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="e2fdd-681">*카운터 집합 페이지에서 다음을 클릭 하면*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-681">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="e2fdd-682">에 **실행 설정** 페이지에서 설정는 **부하 테스트 지속 시간** 를 **5 분** 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-682">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="e2fdd-683">![부하 테스트 지속 시간을 5 분으로 설정](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "부하 테스트 지속 시간을 5 분으로 설정")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-683">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="e2fdd-684">*부하 테스트 지속 시간을 5 분으로 설정*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-684">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="e2fdd-685">**솔루션 탐색기**, 두 번 클릭은 **Local.settings** 테스트 설정을 탐색 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-685">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="e2fdd-686">기본적으로 Visual Studio 테스트를 실행 하려면 로컬 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-686">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-687">또는 테스트 프로젝트를 사용 하 여 클라우드 부하 테스트 실행을 구성할 수 **온라인 VSO (Visual Studio)**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-687">Alternatively, you can configure your test project to run the load tests in the cloud using **Visual Studio Online (VSO)**.</span></span> <span data-ttu-id="e2fdd-688">VSO는 클라우드 기반 부하 테스트 좀 더 현실적인 부하를 시뮬레이션 하는 서비스, 보다 큰 CPU 용량, 사용 가능한 메모리 및 네트워크 대역폭을 같은 로컬 환경 제약 조건은 방지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-688">VSO provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory and network bandwidth.</span></span> <span data-ttu-id="e2fdd-689">VSO를 사용 하 여 부하 테스트를 실행 하는 방법에 대 한 자세한 내용은 참조 [이 여기서](https://www.visualstudio.com/get-started/load-test-your-app-vs)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-689">For more information about using VSO to run load tests, see [this article](https://www.visualstudio.com/get-started/load-test-your-app-vs).</span></span>

    ![테스트 설정](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="e2fdd-691">작업 3-자동 크기 조정 확인</span><span class="sxs-lookup"><span data-stu-id="e2fdd-691">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="e2fdd-692">이제 이전 태스크에서 만든 부하 테스트를 실행 하 고 웹 앱 부하 상태에서 어떻게 적용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-692">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="e2fdd-693">**솔루션 탐색기**를 두 번 클릭 **LoadTest1.loadtest** 를 부하 테스트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-693">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="e2fdd-694">![LoadTest1.loadtest 열기](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "LoadTest1.loadtest 열기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-694">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="e2fdd-695">*LoadTest1.loadtest 열기*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-695">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="e2fdd-696">에 **LoadTest1.loadtest** 창에서 부하 테스트를 실행 하려면 도구 상자에서 첫 번째 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-696">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="e2fdd-697">![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "부하 테스트 실행")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-697">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="e2fdd-698">*부하 테스트 실행*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-698">*Running the load test*</span></span>
3. <span data-ttu-id="e2fdd-699">부하 테스트가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-699">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-700">부하 테스트 요청을 보내는 웹 앱에 동시에 여러 사용자가 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-700">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="e2fdd-701">테스트가 실행 되는 경우에 모든 오류, 경고 또는 부하 테스트 실행에 관련 된 기타 정보를 검색 하는 사용 가능한 카운터를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-701">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="e2fdd-702">![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "부하 테스트가 완료 될 때까지 대기")</span><span class="sxs-lookup"><span data-stu-id="e2fdd-702">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="e2fdd-703">*부하 테스트 실행*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-703">*Load test running*</span></span>
4. <span data-ttu-id="e2fdd-704">테스트가 완료 되 면 관리 포털으로 돌아가서를 탐색 하는 **배율** 웹 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-704">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="e2fdd-705">아래는 **용량** 섹션을 표시 되어야 그래프의 새 인스턴스를 자동으로 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-705">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![새 인스턴스를 자동으로 배포](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="e2fdd-707">*새 인스턴스를 자동으로 배포*</span><span class="sxs-lookup"><span data-stu-id="e2fdd-707">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2fdd-708">변경 내용을 그래프에 표시 하려면 몇 분 정도 걸릴 수 있습니다 (키를 눌러 **CTRL + f 5를 눌러** 주기적으로 페이지를 새로).</span><span class="sxs-lookup"><span data-stu-id="e2fdd-708">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="e2fdd-709">변경 내용을 표시 되지 않으면 다음을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-709">If you do not see any changes, you can try the following:</span></span>
    > 
    > - <span data-ttu-id="e2fdd-710">부하 테스트의 기간을 늘려야 (예: **10 분**)</span><span class="sxs-lookup"><span data-stu-id="e2fdd-710">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="e2fdd-711">최대값과 최소값을 줄이려면는 **대상 CPU** 웹 응용 프로그램의 자동 크기 조정 구성에 대 한 범위</span><span class="sxs-lookup"><span data-stu-id="e2fdd-711">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="e2fdd-712">부하 테스트와 클라우드에서 실행 **Visual Studio Online**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-712">Run the load test in the cloud with **Visual Studio Online**.</span></span> <span data-ttu-id="e2fdd-713">자세한 내용은 [여기](https://www.visualstudio.com/en-us/get-started/load-test-your-app-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="e2fdd-713">More information [here](https://www.visualstudio.com/en-us/get-started/load-test-your-app-vs.aspx)</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="e2fdd-714">요약</span><span class="sxs-lookup"><span data-stu-id="e2fdd-714">Summary</span></span>

<span data-ttu-id="e2fdd-715">이 실습 랩에서 설정 하 고 프로덕션 웹 앱을 Azure에 응용 프로그램을 배포 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-715">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="e2fdd-716">검색 하 고 사용 하 여 데이터베이스를 업데이트 하 여 시작 **Entity Framework Code First 마이그레이션을**, 새 버전을 사용 하 여 사이트를 배포 하 여 계속 **Git** 롤백 수행 하는 안정적인 최신 버전의 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-716">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="e2fdd-717">또한 Blob 컨테이너에 정적 콘텐츠를 이동 하려면 저장소를 사용 하 여 앱의 크기를 조정 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fdd-717">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
