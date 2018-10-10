---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: '실습: Azure Websites 유지: 변경 및 확장 관리 | Microsoft Docs'
author: rick-anderson
description: 이 실습에서는 어떻게 Microsoft Azure를 쉽게 빌드하고 프로덕션으로 웹 사이트를 배포에 대해 알아봅니다.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: bc6de2f0c8b2cd958c198abb90fc4ad97613e973
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48913309"
---
<a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="ae33a-103">실습: Azure Websites 유지: 변경 및 규모 관리</span><span class="sxs-lookup"><span data-stu-id="ae33a-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>
====================
<span data-ttu-id="ae33a-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="ae33a-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="ae33a-105">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae33a-105">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="ae33a-106">Microsoft Azure를 통해 쉽게 빌드 및 프로덕션 환경에 웹 사이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="ae33a-107">응용 프로그램 라이브 되 면 완료 되지 않았음을 있습니다 하지만 하면 이제 막 시작!</span><span class="sxs-lookup"><span data-stu-id="ae33a-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="ae33a-108">변경 요구 사항, 데이터베이스 업데이트, 확장성 등을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="ae33a-109">다행 스럽게도 Azure App Service에서는 다양 한 원활 하 게 실행 하 여 사이트를 유지 하는 데 유용한 기능을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="ae33a-110">Azure는 안전 하 고 유연한 개발, 배포 및 확장 크기 웹 응용 프로그램에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="ae33a-111">만들기 및 배포 인프라를 관리 해야 하는 번거로움 없이 응용 프로그램에 기존 도구를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="ae33a-112">프로 비전 프로덕션 웹 응용 프로그램을 직접 몇 분 안에 쉽게 하므로 좋아하는 개발 도구를 사용 하 여 만든 콘텐츠를 배포 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="ae33a-113">에 대 한 지원과 함께 소스 제어에서 직접 기존 사이트를 배포할 수 있습니다 **Git**, **GitHub**합니다 **Bitbucket**를 **TFS**, 및도  **DropBox**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="ae33a-114">사용 하 여 스크립트 또는 즐겨 찾는 IDE에서 직접 배포할 **PowerShell** Windows에서 또는 **CLI** 모든 OS에서 실행 되는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="ae33a-115">을 배포한 후에 사이트를 연속 배포에 대 한 지원을 지속적으로 최신 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="ae33a-116">Azure 큰 또는 작은 모든 데이터에 대해 확장 가능한 지속형 클라우드 저장소, 백업 및 복구 솔루션 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="ae33a-117">프로덕션 환경에서 테이블, Blob 및 SQL Database와 같은 저장소 서비스를 응용 프로그램을 배포할 때 클라우드에서 응용 프로그램을 확장 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="ae33a-118">SQL Database를 사용 하 여 응용 프로그램의 새 버전을 배포 하는 경우 생산성 데이터베이스를 최신 상태로 유지 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="ae33a-119">에 감사 드립니다 **Entity Framework Code First 마이그레이션을**, 개발 및 데이터 모델의 배포 환경을 몇 분 안에 업데이트 간소화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="ae33a-120">이 실습 랩에서 Microsoft Azure에서 프로덕션 환경에 웹 앱을 배포할 때 발생할 수 있습니다 다른 항목에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="ae33a-121">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-121">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="ae33a-122">이 항목의 자세한 자세한 검사를 참조 하세요. 합니다 [전자책은 Azure를 사용 하 여 실제 클라우드 앱 빌드](building-real-world-cloud-apps-with-windows-azure/introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="ae33a-123">개요</span><span class="sxs-lookup"><span data-stu-id="ae33a-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="ae33a-124">목표</span><span class="sxs-lookup"><span data-stu-id="ae33a-124">Objectives</span></span>

<span data-ttu-id="ae33a-125">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="ae33a-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="ae33a-126">기존 모델을 사용 하 여 Entity Framework 마이그레이션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ae33a-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="ae33a-127">개체 모델 및 그에 따라 Entity Framework 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="ae33a-128">Git를 사용 하 여 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="ae33a-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="ae33a-129">Azure 관리 포털을 사용 하 여 이전 배포로 롤백</span><span class="sxs-lookup"><span data-stu-id="ae33a-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="ae33a-130">Azure Storage를 사용 하 여 웹 앱 확장</span><span class="sxs-lookup"><span data-stu-id="ae33a-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="ae33a-131">Azure 관리 포털을 사용 하 여 웹 앱에 대 한 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="ae33a-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="ae33a-132">만들기 및 Visual Studio에서 부하 테스트 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="ae33a-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="ae33a-133">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ae33a-133">Prerequisites</span></span>

<span data-ttu-id="ae33a-134">다음는이 실습을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="ae33a-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="ae33a-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="ae33a-136">Azure SDK for.NET 2.2</span><span class="sxs-lookup"><span data-stu-id="ae33a-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="ae33a-137">GIT 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="ae33a-138">Microsoft Azure 구독</span><span class="sxs-lookup"><span data-stu-id="ae33a-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="ae33a-139">등록을 [무료 평가판](http://aka.ms/watk-freetrial)</span><span class="sxs-lookup"><span data-stu-id="ae33a-139">Sign up for a [Free Trial](http://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="ae33a-140">인 경우 Visual Studio Professional, Test Professional, Premium 또는 Ultimate with MSDN 또는 MSDN 플랫폼 구독자를 활성화 하 [MSDN 혜택](http://aka.ms/watk-msdn) 개발 및 Azure에서 테스트를 시작 하려면 지금</span><span class="sxs-lookup"><span data-stu-id="ae33a-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](http://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="ae33a-141">[BizSpark](http://aka.ms/watk-bizspark) Azure를 자동으로 수신 하는 멤버는 Visual Studio Ultimate with MSDN subscription을 통해 혜택</span><span class="sxs-lookup"><span data-stu-id="ae33a-141">[BizSpark](http://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="ae33a-142">멤버는 [Microsoft Partner Network](http://aka.ms/watk-mpn) Cloud Essentials 프로그램에는 무료로 월간 Azure 크레딧 수신</span><span class="sxs-lookup"><span data-stu-id="ae33a-142">Members of the [Microsoft Partner Network](http://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="ae33a-143">설정</span><span class="sxs-lookup"><span data-stu-id="ae33a-143">Setup</span></span>

<span data-ttu-id="ae33a-144">이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="ae33a-145">Windows 탐색기를 열고 실습용 **원본** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="ae33a-146">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택한 **관리자 권한으로 실행** 환경을 구성 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="ae33a-147">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="ae33a-148">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="ae33a-149">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="ae33a-149">Using the Code Snippets</span></span>

<span data-ttu-id="ae33a-150">랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="ae33a-151">사용자 편의 위해이 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="ae33a-152">각 실습에 시작 솔루션을 함께 표시 됩니다는 **시작** 다른 독립적으로 각 연습에 따라 할 수 있는 연습 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="ae33a-153">주의 하십시오 연습 하는 동안 추가 되는 코드 조각은 솔루션부터 이러한 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="ae33a-154">연습에 대 한 소스 코드 안에 있습니다.는 **최종** 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="ae33a-155">이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="ae33a-156">연습</span><span class="sxs-lookup"><span data-stu-id="ae33a-156">Exercises</span></span>

<span data-ttu-id="ae33a-157">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="ae33a-158">Entity Framework 마이그레이션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ae33a-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="ae33a-159">스테이징 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ae33a-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="ae33a-160">프로덕션 환경에서 배포 롤백 수행</span><span class="sxs-lookup"><span data-stu-id="ae33a-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="ae33a-161">Azure Storage를 사용 하 여 확장</span><span class="sxs-lookup"><span data-stu-id="ae33a-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="ae33a-162">[웹 앱에 대 한 자동 크기 조정을 사용할](#Exercise5) (Visual Studio 2013 Ultimate edition에 대 한 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="ae33a-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="ae33a-163">이 랩을 완료 하기 위한 예상 시간: **75 분**</span><span class="sxs-lookup"><span data-stu-id="ae33a-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="ae33a-164">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="ae33a-165">미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="ae33a-166">이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="ae33a-167">개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="ae33a-168">연습 1: Entity Framework 마이그레이션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ae33a-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="ae33a-169">응용 프로그램을 개발 하는 경우 데이터 모델에는 시간이 지남에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="ae33a-170">(새 버전을 만들면) 하는 경우 이러한 변경 내용은 기존 모델 데이터베이스에 영향을 줄 수 및 데이터베이스를 오류를 방지 하려면 최신 상태로 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="ae33a-171">이러한 변경 내용 모델에 대 한 추적을 간소화 하기 위해 **Entity Framework Code First 마이그레이션을** 자동으로 데이터베이스 스키마를 사용 하 여 모델을 비교 하는 변경 내용을 검색 하 고 데이터베이스를 업데이트 하는 특정 코드를 생성 합니다. 새로 만들기 *버전* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="ae33a-172">이 연습을 사용 하도록 설정 하는 방법을 보여 줍니다. **마이그레이션을** 응용 프로그램에 쉽게 검색 하는 방법에 데이터베이스를 업데이트 하려면 변경 내용을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="ae33a-173">작업 1-마이그레이션 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ae33a-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="ae33a-174">이 태스크를 사용 하도록 설정 하는 단계를 이동 **Entity Framework Code First 마이그레이션을** 에 **Geek 퀴즈** 데이터베이스, 모델을 변경 하 고에서 이러한 변경 내용이 반영 하는 방법을 이해 합니다 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="ae33a-175">Visual Studio를 열고 엽니다는 **GeekQuiz.sln** 에서 솔루션 파일 **Source\Ex1 UsingEntityFrameworkMigrations\Begin**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="ae33a-176">다운로드 및 설치 하기 위해 솔루션을 구축 합니다 **NuGet** 종속성 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="ae33a-177">이렇게 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **솔루션 빌드** 누르거나 **Ctrl + Shift + B**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="ae33a-178">**도구** Visual Studio에서 메뉴 **NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-178">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="ae33a-179">에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="ae33a-180">기존 모델을 기반으로 하는 초기 마이그레이션 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="ae33a-181">![마이그레이션을 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "마이그레이션을 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="ae33a-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="ae33a-182">*마이그레이션을 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="ae33a-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-183">이 명령은 추가 **마이그레이션을** Geek 퀴즈 프로젝트 파일이 포함 된 폴더의 이름은 **Configuration.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="ae33a-184">합니다 **구성** 클래스를 사용 하면 마이그레이션에 대해 동작 하는 방식을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="ae33a-185">마이그레이션을 사용 하도록 설정 된 업데이트 해야 합니다 **구성** 초기 데이터를 사용 하 여 데이터베이스를 채우는 데 클래스는 **Geek 퀴즈** 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="ae33a-186">아래 **마이그레이션을**, 대체를 **Configuration.cs** 것을 사용 하 여 파일에는 **Source\Assets** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-187">이후 **마이그레이션을** 를 호출 합니다를 **초기값** 레코드가 데이터베이스에서 중복 되지 않았는지 확인 해야 하는 모든 데이터베이스 업데이트를 사용 하 여 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="ae33a-188">합니다 **AddOrUpdate** 메서드 중복 데이터 방지 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="ae33a-189">초기 마이그레이션에 추가 하려면 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-190">라는 데이터베이스가 있는지 확인 하십시오 &quot;GeekQuizProd&quot; LocalDB 인스턴스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="ae33a-191">![기본 스키마 마이그레이션 추가](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "추가 기본 스키마 마이그레이션")</span><span class="sxs-lookup"><span data-stu-id="ae33a-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="ae33a-192">*기본 스키마 마이그레이션 추가*</span><span class="sxs-lookup"><span data-stu-id="ae33a-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-193">**Add-migration** 마지막 마이그레이션을 만든 후 모델에 대 한 변경 내용에 따라 다음 마이그레이션을 스 캐 폴딩 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="ae33a-194">이 경우 첫 번째 마이그레이션 프로젝트의 경우 스크립트에 정의 된 모든 테이블을 만들려면 추가 됩니다는 **TriviaContext** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="ae33a-195">다음 명령을 실행 하 여 데이터베이스를 업데이트 하려면 마이그레이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="ae33a-196">이 명령에 대 한 지정 된 **Verbose** 대상 데이터베이스에 적용 되 고 SQL 문을 보려면 플래그 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="ae33a-197">![초기 데이터베이스 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "초기 데이터베이스 만들기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="ae33a-198">*초기 데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-199">**Update-database** 마이그레이션을 보류 중인 데이터베이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="ae33a-200">이 경우 web.config 파일에 정의 된 연결 문자열을 사용 하 여 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="ae33a-201">로 이동 **뷰** 메뉴를 열고 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="ae33a-202">![SQL Server 개체 탐색기에서 열기](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server 개체 탐색기에서 열기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="ae33a-203">*SQL Server 개체 탐색기에서 열기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="ae33a-204">에 **SQL Server 개체 탐색기** 창 마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스에 연결 합니다 **SQL Server** 노드와 선택 **SQL Server 추가...**  옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="ae33a-205">![SQL Server 인스턴스를 추가](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server 인스턴스를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="ae33a-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="ae33a-206">*SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*</span><span class="sxs-lookup"><span data-stu-id="ae33a-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="ae33a-207">설정 합니다 **서버 이름** 하 *(localdb) \v11.0* 두고 **Windows 인증** 을 인증 모드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="ae33a-208">클릭 **Connect** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="ae33a-209">![LocalDB에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB에 연결")</span><span class="sxs-lookup"><span data-stu-id="ae33a-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="ae33a-210">*LocalDB에 연결*</span><span class="sxs-lookup"><span data-stu-id="ae33a-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="ae33a-211">엽니다는 **GeekQuizProd** 데이터베이스 및 확장을 **테이블** 노드.</span><span class="sxs-lookup"><span data-stu-id="ae33a-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="ae33a-212">알 수 있듯이 합니다 **Update-database** 명령에 정의 된 모든 테이블을 생성 합니다 **TriviaContext** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="ae33a-213">찾을 **dbo입니다. TriviaQuestions** 테이블 및 열 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="ae33a-214">다음 태스크에서는이 테이블에 새 열을 추가 사용 하 여 데이터베이스를 업데이트할 **마이그레이션을**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="ae33a-215">![기타 정보 열 질문](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "퀴즈 질문 열")</span><span class="sxs-lookup"><span data-stu-id="ae33a-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="ae33a-216">*기타 정보 열 질문*</span><span class="sxs-lookup"><span data-stu-id="ae33a-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="ae33a-217">작업 2-마이그레이션을 사용 하 여 데이터베이스 스키마를 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae33a-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="ae33a-218">이 태스크에서는 사용할지 **Entity Framework Code First 마이그레이션을** 모델에서 변경을 감지 하 여 데이터베이스를 업데이트 하는 데 필요한 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="ae33a-219">업데이트를 **TriviaQuestions** 새 속성을 추가 하 여 엔터티.</span><span class="sxs-lookup"><span data-stu-id="ae33a-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="ae33a-220">다음 표에 새 열을 포함할 새 마이그레이션을 만들려면 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="ae33a-221">**솔루션 탐색기**를 두 번 클릭 합니다 **TriviaQuestion.cs** 내에 있는 파일을 **모델** 폴더.</span><span class="sxs-lookup"><span data-stu-id="ae33a-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="ae33a-222">라는 새 속성을 추가할 **힌트**다음 코드 조각에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="ae33a-223">에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="ae33a-224">모델의 변경을 반영 새 마이그레이션을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="ae33a-225">![Add-migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-migration")</span><span class="sxs-lookup"><span data-stu-id="ae33a-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="ae33a-226">*추가 마이그레이션*</span><span class="sxs-lookup"><span data-stu-id="ae33a-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-227">두 가지 방법으로 구성 된 마이그레이션 파일 **위로** 하 고 **아래로**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="ae33a-228">합니다 **등록** 메서드를 사용 하 여 현재 버전의 데이터베이스에 적용 하는 응용 프로그램 요구 변경 내용 지정할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="ae33a-229">**아래로** 에 추가 변경을 하는 데 사용 되는 **위로** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ae33a-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="ae33a-230">타임 스탬프 순서 및 해당 하는 마지막 업데이트 이후 사용 되지 않은 모든 마이그레이션을 데이터베이스 마이그레이션은 데이터베이스를 업데이트할 때 실행 됩니다 (의 \_마이그레이션을 적용 된 MigrationHistory 테이블의 추적).</span><span class="sxs-lookup"><span data-stu-id="ae33a-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="ae33a-231">합니다 **등록** 모든 마이그레이션 메서드의 호출 되며 지정한 데이터베이스에 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="ae33a-232">마이그레이션 이전으로 돌아가서 하기로 하는 경우는 **다운** 메서드를 호출 하 여 역순으로 변경 내용을 다시 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="ae33a-233">에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="ae33a-234">출력을 **Update-database** 생성 된 명령을 **Alter Table** SQL 문을 새 열을 추가 하는 **TriviaQuestions** 아래 이미지에 표시 된 대로 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="ae33a-235">![추가 열 SQL 문을 생성](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "열 SQL 문을 생성 추가")</span><span class="sxs-lookup"><span data-stu-id="ae33a-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="ae33a-236">*추가 열 SQL 문 생성*</span><span class="sxs-lookup"><span data-stu-id="ae33a-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="ae33a-237">**SQL Server 개체 탐색기**, 새로 고침을 **dbo입니다. TriviaQuestions** 테이블 및 확인 하는 새 **힌트** 열이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="ae33a-238">![새 힌트 열을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "새 힌트 열 표시")</span><span class="sxs-lookup"><span data-stu-id="ae33a-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="ae33a-239">*새 힌트 열 표시*</span><span class="sxs-lookup"><span data-stu-id="ae33a-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="ae33a-240">다시 합니다 **TriviaQuestion.cs** 편집기를 추가 **StringLength** 제약 조건을 *힌트* 속성을 다음 코드 조각에 표시 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="ae33a-241">에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="ae33a-242">에 **패키지 관리자 콘솔**, 다음 명령을 입력 하 고 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="ae33a-243">출력을 **Update-database** 생성 된 명령을 **Alter Table** SQL 문을 업데이트를 *힌트* 열 유형의 **TriviaQuestions** 테이블을 아래 그림과에서 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="ae33a-244">![Alter column SQL 문 생성](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 문 생성")</span><span class="sxs-lookup"><span data-stu-id="ae33a-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="ae33a-245">*Alter column SQL 문 생성*</span><span class="sxs-lookup"><span data-stu-id="ae33a-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="ae33a-246">**SQL Server 개체 탐색기**, 새로 고침을 **dbo입니다. TriviaQuestions** 테이블 및 있는지 여부를 확인 합니다 **힌트** 열 형식이 **nvarchar(150)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="ae33a-247">![새 제약 조건을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "새 제약 조건을 보여 주는")</span><span class="sxs-lookup"><span data-stu-id="ae33a-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="ae33a-248">*새 제약 조건을 보여 주는*</span><span class="sxs-lookup"><span data-stu-id="ae33a-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="ae33a-249">연습 2: 스테이징 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ae33a-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="ae33a-250">**Azure App Service의 웹 앱** 스테이징 된 게시를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="ae33a-251">스테이징 된 게시 각 기본 프로덕션 사이트에 대 한 스테이징 사이트 슬롯을 만들고 중단 시간 없이 이러한 슬롯을 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="ae33a-252">공개적으로 해제 하기 전에 변경 내용 유효성 검사, 증분 방식으로 사이트 콘텐츠를 통합 하 고 변경 내용이 예상 대로 작동 하지 않는 경우 롤백하지 데 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="ae33a-253">이 연습에서는 배포 합니다 **Geek 퀴즈** Git 소스 제어를 사용 하 여 웹 앱의 스테이징 환경에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="ae33a-254">이 위해 하면 웹 앱 만들기 및 관리 포털에서 필수 구성 요소를 프로 비전을 구성 된 **Git** 리포지토리 및 강제 응용 프로그램에서에서 소스 코드를 로컬 컴퓨터에서 스테이징 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="ae33a-255">또한 사용 하 여 프로덕션 데이터베이스를 업데이트 합니다 **Code First 마이그레이션을** 이전 연습에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="ae33a-256">그런 다음 해당 작업을 확인 하려면이 테스트 환경에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="ae33a-257">만족 한다면 기대치에 따라 작동 하, 프로덕션 응용 프로그램을 승격 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="ae33a-258">스테이징 된 게시를 사용 하려면 웹 앱에 있어야 **표준 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="ae33a-259">표준 모드에 웹 앱을 변경 하면 추가 요금이 발생는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="ae33a-260">가격 책정에 대 한 자세한 내용은 참조 하세요. [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="ae33a-261">작업 1-Azure App Service에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ae33a-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="ae33a-262">이 작업에서 웹 앱을 만듭니다 **Azure App Service** 관리 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="ae33a-263">구성도 **SQL Database** 응용 프로그램 데이터를 유지 하 고 소스 제어에 대 한 로컬 Git 리포지토리를 구성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="ae33a-264">로 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com) 구독과 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![Azure 관리 포털에 로그인](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="ae33a-266">*Azure 관리 포털에 로그인*</span><span class="sxs-lookup"><span data-stu-id="ae33a-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="ae33a-267">클릭 **새로 만들기** 페이지의 맨 위에 있는 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="ae33a-268">![새 웹 앱을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "새 웹 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="ae33a-269">*새 웹 앱 만들기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="ae33a-270">클릭 **계산**하십시오 **웹 사이트** 차례로 **사용자 지정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="ae33a-271">![사용자 지정 만들기를 사용 하 여 새 웹 앱을 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="ae33a-272">*사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="ae33a-273">에 **새 웹 사이트-사용자 지정 만들기** 대화 상자에서 사용할 수 있는 제공 **URL** (예: *geek 퀴즈*), 위치를 선택 합니다 **지역** 드롭다운 목록에서 선택한 **새 SQL 데이터베이스를 만듭니다** 에 **데이터베이스** 드롭 다운 목록.</span><span class="sxs-lookup"><span data-stu-id="ae33a-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="ae33a-274">마지막으로 선택 합니다 **소스 제어에서 게시** 확인란을 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![새 웹 앱을 사용자 지정](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="ae33a-276">*새 웹 앱을 사용자 지정*</span><span class="sxs-lookup"><span data-stu-id="ae33a-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="ae33a-277">데이터베이스 설정에 대 한 다음 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="ae33a-278">에 **이름을** 텍스트 상자에 데이터베이스 이름을 입력 합니다 (예: *geekquiz\_db*)</span><span class="sxs-lookup"><span data-stu-id="ae33a-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="ae33a-279">서버에서 **드롭 다운** 목록에서 **새 SQL 데이터베이스 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="ae33a-280">또는 기존 서버를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="ae33a-281">에 **데이터베이스 사용자 이름** 하 고 **데이터베이스 암호** SQL database 서버에 대 한 관리자 사용자 이름 및 암호를 입력 하는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="ae33a-282">서버를 선택 하면 이미 만든 경우 암호를 묻는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![데이터베이스 설정 지정](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="ae33a-284">*데이터베이스 설정 지정*</span><span class="sxs-lookup"><span data-stu-id="ae33a-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="ae33a-285">**다음** 을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="ae33a-286">선택 **로컬 Git 리포지토리** 클릭 하 여 사용 하 여 소스 제어에 대 한 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-287">배포 자격 증명 (사용자 이름 및 암호) 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![Git 리포지토리를 만드는 중](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="ae33a-289">*Git 리포지토리를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="ae33a-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="ae33a-290">새 웹 앱을 만들 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-291">기본적으로 Azure에서 도메인을 제공 *azurewebsites.net* 를 Azure 관리 포털을 사용 하 여 사용자 지정 도메인을 설정할 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="ae33a-292">그러나 특정 Azure App Service 모드를 사용 하는 경우 사용자 지정 도메인에 관리할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="ae33a-293">Azure App Service는 Free, Shared, Basic, Standard 및 Premium edition에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="ae33a-294">무료 및 공유 모드에서 모든 web apps 다중 테 넌 트 환경에서 실행 되며 CPU, 메모리 및 네트워크 사용량에 대 한 할당량을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="ae33a-295">무료 앱의 최대 수는 계획을 사용 하 여 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="ae33a-296">표준 모드에서 표준 Azure에 해당 하는 전용 가상 머신에서 실행 되는 앱 리소스를 계산 하는 것이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="ae33a-297">웹 앱 모드 구성에서 찾을 수 있습니다 합니다 **확장** 웹 앱의 메뉴.</span><span class="sxs-lookup"><span data-stu-id="ae33a-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="ae33a-298">![Azure App Service 모드](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 모드")</span><span class="sxs-lookup"><span data-stu-id="ae33a-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="ae33a-299">사용 중인 경우 **Shared** 또는 **표준** 앱으로 이동 하 여 웹 앱에 대 한 사용자 지정 도메인을 관리할 수 있는 모드 **구성** 메뉴와 클릭**도메인 관리** 아래에서 *도메인 이름*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="ae33a-300">![도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "도메인 관리")</span><span class="sxs-lookup"><span data-stu-id="ae33a-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="ae33a-301">![사용자 지정 도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "사용자 지정 도메인 관리")</span><span class="sxs-lookup"><span data-stu-id="ae33a-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="ae33a-302">웹 앱이 만들어지면 아래에 있는 링크를 클릭 합니다 **URL** 열을 새 웹 앱이 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![새 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="ae33a-304">*새 웹 앱으로 이동*</span><span class="sxs-lookup"><span data-stu-id="ae33a-304">*Browsing to the new web app*</span></span>

    ![웹 앱 실행](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="ae33a-306">*웹 앱 실행*</span><span class="sxs-lookup"><span data-stu-id="ae33a-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="ae33a-307">작업 2-프로덕션 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="ae33a-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="ae33a-308">이 작업을 사용 하 여 합니다 **Entity Framework Code First 마이그레이션을** 대상으로 하는 데이터베이스를 만들려면 합니다 **Azure SQL Database** 이전 태스크에서 만든 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="ae33a-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="ae33a-309">관리 포털에서 이전 태스크에서 만든 웹 앱으로 이동 하 고 이동할 해당 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="ae33a-310">에 **대시보드** 페이지에서 **연결 문자열 보기** 링크를 **눈** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="ae33a-311">![연결 문자열 보기](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "연결 문자열 보기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="ae33a-312">*연결 문자열 보기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-312">*View connection strings*</span></span>
3. <span data-ttu-id="ae33a-313">복사 합니다 **연결 문자열** 값 및 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="ae33a-314">![Azure 관리 포털에서 연결 문자열](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 관리 포털에서 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="ae33a-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="ae33a-315">*Azure 관리 포털에서 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="ae33a-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="ae33a-316">클릭 **SQL Database** Azure에서 SQL 데이터베이스의 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="ae33a-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="ae33a-317">![SQL Database 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database 메뉴")</span><span class="sxs-lookup"><span data-stu-id="ae33a-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="ae33a-318">*SQL Database 메뉴*</span><span class="sxs-lookup"><span data-stu-id="ae33a-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="ae33a-319">이전 태스크에서 만든 데이터베이스를 찾아서 서버를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="ae33a-320">![SQL Database 서버](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database 서버")</span><span class="sxs-lookup"><span data-stu-id="ae33a-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="ae33a-321">*SQL Database 서버*</span><span class="sxs-lookup"><span data-stu-id="ae33a-321">*SQL Database server*</span></span>
6. <span data-ttu-id="ae33a-322">에 **빠른 시작** 페이지에서 서버를 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="ae33a-323">![구성 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "구성 메뉴")</span><span class="sxs-lookup"><span data-stu-id="ae33a-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="ae33a-324">*메뉴를 구성 합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-324">*Configure menu*</span></span>
7. <span data-ttu-id="ae33a-325">에 **허용 된 IP 주소** 섹션을 클릭 **허용 되는 IP 주소를 추가할** IP SQL Database 서버에 연결할 수 있도록 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="ae33a-326">![허용 된 IP 주소](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "허용 된 IP 주소")</span><span class="sxs-lookup"><span data-stu-id="ae33a-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="ae33a-327">*허용 된 IP 주소*</span><span class="sxs-lookup"><span data-stu-id="ae33a-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="ae33a-328">클릭 **저장할** 단계를 완료 하려면 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="ae33a-329">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="ae33a-330">에 **패키지 관리자 콘솔**을 대체 하는 다음 명령을 실행 *[YOUR CONNECTION STRING]* 자리 표시자를 Azure에서 복사한 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="ae33a-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="ae33a-331">![Windows Azure SQL Database를 대상으로 하는 데이터베이스 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL Database를 대상으로 하는 데이터베이스 업데이트")</span><span class="sxs-lookup"><span data-stu-id="ae33a-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="ae33a-332">*Azure SQL Database를 대상으로 하는 데이터베이스 업데이트*</span><span class="sxs-lookup"><span data-stu-id="ae33a-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="ae33a-333">작업 3 – Git를 사용 하 여 스테이징 배포 Geek 퀴즈</span><span class="sxs-lookup"><span data-stu-id="ae33a-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="ae33a-334">이 작업에서는 웹 앱의 스테이징 된 게시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="ae33a-335">그런 다음 Geek 퀴즈 응용 프로그램 로컬 컴퓨터에서 직접 웹 앱의 스테이징 환경에 게시 하는 Git을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="ae33a-336">포털로 돌아가서 웹 응용 프로그램의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![웹 앱 관리 페이지 열기](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="ae33a-338">*웹 앱 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="ae33a-339">로 이동 합니다 **확장** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="ae33a-340">아래는 **일반** 섹션에서 **표준** 구성 및 클릭 **저장** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-341">현재 지역 및 구독에서 모든 웹 앱을 실행 하 **표준** 모드를 두고 합니다 **모두 선택** 확인란을 선택 합니다 **사이트 선택** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="ae33a-342">그렇지 않으면 선택을 취소 합니다 **모두 선택** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="ae33a-343">![웹 앱을 표준 모드로 업그레이드](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "를 표준 모드로 업그레이드 하는 웹 앱")</span><span class="sxs-lookup"><span data-stu-id="ae33a-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="ae33a-344">*웹 앱을 표준 모드로 업그레이드*</span><span class="sxs-lookup"><span data-stu-id="ae33a-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="ae33a-345">클릭 **예** 변경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="ae33a-346">![표준 모드로 변경 확인](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "웹 앱 모드를 변경 하는 계속")</span><span class="sxs-lookup"><span data-stu-id="ae33a-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="ae33a-347">*표준 모드로 변경 확인*</span><span class="sxs-lookup"><span data-stu-id="ae33a-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="ae33a-348">로 이동 합니다 **대시보드** 페이지를 클릭 **스테이징 된 게시를 사용 하도록 설정** 아래에서 **간략 상태** 섹션.</span><span class="sxs-lookup"><span data-stu-id="ae33a-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="ae33a-349">![스테이징 된 게시를 사용 하도록 설정](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "스테이징 된 게시를 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="ae33a-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="ae33a-350">*스테이징 된 게시를 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="ae33a-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="ae33a-351">클릭 **예** 스테이징 된 게시를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="ae33a-352">![스테이징 된 게시를 확인](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "스테이징 된 게시를 사용 하도록 설정 하려면 예 클릭")</span><span class="sxs-lookup"><span data-stu-id="ae33a-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="ae33a-353">*스테이징 된 게시를 확인합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="ae33a-354">웹 앱의 목록에서 스테이징 사이트 슬롯을 표시 하려면 웹 앱 이름 왼쪽에 표시를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="ae33a-355">뒤에 웹 앱의 이름이 ***(준비)*** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="ae33a-356">관리 페이지로 이동 하려면 스테이징 사이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="ae33a-357">![스테이징 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "스테이징 웹 앱으로 이동")</span><span class="sxs-lookup"><span data-stu-id="ae33a-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="ae33a-358">*스테이징 앱으로 이동*</span><span class="sxs-lookup"><span data-stu-id="ae33a-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="ae33a-359">해당 그 관리 페이지가 다른 웹 앱의 관리 페이지와 같은 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="ae33a-360">로 이동 합니다 **배포** 페이지 및 복사 합니다 **Git URL** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="ae33a-361">이 연습 뒷부분에서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-361">You will use it later in this exercise.</span></span>

    ![Git URL 값을 복사합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="ae33a-363">*Git URL 값을 복사합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="ae33a-364">새 **Git Bash** 콘솔 및 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="ae33a-365">업데이트를 *[YOUR 응용 프로그램 경로]* 자리 표시자에 대 한 경로를 합니다 **GeekQuiz** 솔루션에는 **Source\Ex1 DeployingWebSiteToStaging\Begin** 의 폴더 이 실습 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 초기화 및 첫 번째 커밋](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="ae33a-367">*Git 초기화 및 첫 번째 커밋*</span><span class="sxs-lookup"><span data-stu-id="ae33a-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="ae33a-368">원격 웹 앱을 푸시 하려면 다음 명령을 실행 **Git** 리포지토리.</span><span class="sxs-lookup"><span data-stu-id="ae33a-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="ae33a-369">관리 포털에서 가져온 URL을 사용 하 여 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="ae33a-370">배포 암호에 대 한 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure에 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="ae33a-372">*Azure에 푸시*</span><span class="sxs-lookup"><span data-stu-id="ae33a-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-373">FTP 호스트 또는 웹 앱의 GIT 리포지토리에 콘텐츠를 배포할 때 사용 하 여 인증 해야 합니다 **배포 자격 증명** 웹 앱에서 만든 **퀵스타트** 또는 **대시보드**  관리 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="ae33a-374">배포 자격 증명을 알 수 없는 경우 관리 포털을 사용 하 여 쉽게 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="ae33a-375">웹 앱을 엽니다 **대시보드** 페이지를 클릭 합니다 **배포 자격 증명 재설정** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="ae33a-376">새 암호를 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="ae33a-377">배포 자격 증명은 구독과 연결 된 모든 web apps를 사용 하 여 사용 하기에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="ae33a-378">Azure에 성공적으로 푸시된 웹 앱을 확인 하기 위해 다시 관리 포털로 이동 하 고 클릭 **Websites**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="ae33a-379">웹 앱을 찾아 스테이징 사이트 슬롯을 표시 하려면 항목을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="ae33a-380">클릭 해당 **이름을** 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="ae33a-381">클릭 **배포** 보려는 합니다 **배포 기록**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="ae33a-382">있는지 확인 하십시오는 **활성 배포가** 사용 하 여 프로그램  *&quot;초기 커밋&quot;* 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![활성 배포](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="ae33a-384">*활성 배포*</span><span class="sxs-lookup"><span data-stu-id="ae33a-384">*Active deployment*</span></span>
13. <span data-ttu-id="ae33a-385">마지막으로, 클릭 **찾아보기** 웹 앱으로 이동 하려면 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![웹 앱 찾아보기](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="ae33a-387">*웹 앱 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-387">*Browse web app*</span></span>
14. <span data-ttu-id="ae33a-388">응용 프로그램을 성공적으로 배포한 경우 Geek 퀴즈 로그인 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-389">배포 된 응용 프로그램의 주소 URL은 뒤에 웹 앱의 이름을 포함 *-스테이징*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![스테이징 환경에서 실행 중인 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="ae33a-391">*스테이징 환경에서 실행 중인 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="ae33a-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="ae33a-392">응용 프로그램을 탐색 하려는 경우 클릭 **등록** 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="ae33a-393">사용자 이름, 전자 메일 주소 및 암호를 입력 하 여 계정 세부 정보를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="ae33a-394">다음으로, 응용 프로그램에서는 퀴즈의 첫 번째 질문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="ae33a-395">이 예상 대로 작동 하는지 확인 하려면 몇 가지 질문에 답변 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![응용 프로그램을 사용할 준비가 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="ae33a-397">*응용 프로그램을 사용할 준비가 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="ae33a-398">작업 4-프로덕션 웹 앱을 승격 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="ae33a-399">웹 앱 스테이징 환경에서 제대로 작동 하는지 확인 했으므로 프로덕션으로 승격할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="ae33a-400">이 태스크에서는 프로덕션 사이트 슬롯을 사용 하 여 스테이징 사이트 슬롯을 교환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="ae33a-401">관리 포털에 다시 이동 하 고 스테이징 사이트 슬롯을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="ae33a-402">클릭 **교환** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-402">Click **Swap** in the command bar.</span></span>

    ![프로덕션으로 교환](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="ae33a-404">*프로덕션으로 교환*</span><span class="sxs-lookup"><span data-stu-id="ae33a-404">*Swap to production*</span></span>
2. <span data-ttu-id="ae33a-405">클릭 **예** 스왑 작업을 계속 하려면 확인 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="ae33a-406">Azure가 즉시 스테이징 사이트의 콘텐츠를 사용 하 여 프로덕션 사이트의 콘텐츠를 교환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-407">일부 설정은 준비 된 버전에서 프로덕션 버전 (예: 연결 문자열 재정의 처리기 매핑 등)에 자동으로 복사 됩니다 있지만 (예: DNS 끝점, SSL 바인딩 등)에 다른 설정은 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![교환 작업 확인](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="ae33a-409">*교환 작업 확인*</span><span class="sxs-lookup"><span data-stu-id="ae33a-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="ae33a-410">교체가 완료 되 면 프로덕션 슬롯을 선택 하 고 클릭 **찾아보기** 프로덕션 사이트를 열려면 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="ae33a-411">주소 표시줄에 URL을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-412">캐시의 선택을 취소 하려면 브라우저를 새로 고침 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="ae33a-413">Internet Explorer에서 하면이 키를 눌러 **CTRL + R**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![프로덕션 환경에서 실행 중인 웹 앱](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="ae33a-415">에 **GitBash** 콘솔에서 프로덕션 슬롯을 대상으로 로컬 Git 리포지토리에 대 한 원격 URL을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="ae33a-416">이 위해 배포 사용자 이름을 웹 앱의 이름을 사용 하 여 자리 표시자를 대체 하는 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-417">다음 실습에서 랩의 단순성에 대 한 스테이징 대신 프로덕션 사이트에 변경 내용을 푸시할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="ae33a-418">실제 시나리오에서 프로덕션으로 수준을 올리기 전에 스테이징 환경에서 변경 내용을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="ae33a-419">연습 3: 프로덕션 환경에서 배포 롤백 수행</span><span class="sxs-lookup"><span data-stu-id="ae33a-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="ae33a-420">시나리오가 없는 없는 스테이징과 프로덕션, 예를 들어 간에 핫 스왑 하는 데 스테이징 슬롯을 사용 하는 경우 **무료** 하거나 **공유** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="ae33a-421">이러한 시나리오에서는 테스트 해야 테스트 환경에서 응용 프로그램-로컬 또는 원격 사이트에 – 프로덕션에 배포 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="ae33a-422">그러나 가능성이 프로덕션 사이트에서 테스트 단계 중에 검색 되지 문제가 발생할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="ae33a-423">이 예제의 경우 쉽게 응용 프로그램의 이전 및 더 안정적인 버전으로 가능한 한 빨리 전환 하는 메커니즘을 마련해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="ae33a-424">**Azure App Service**, 소스 제어의 연속 배포를 통해이 가능한 감사 인사를 전 합니다 **재배포** 관리 포털에서 사용할 수 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="ae33a-425">Azure 연결 된 리포지토리에 푸시된 커밋과 배포를 추적 하 고 이전 배포를 사용 하 여 언제 든 지 응용 프로그램을 다시 배포 하는 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="ae33a-426">이 연습에서는 코드에 대 한 변경 수행 합니다 **Geek 퀴즈** 의도적으로 삽입 하는 응용 프로그램을 *버그*합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="ae33a-427">오류를 확인 하려면 프로덕션 환경에 응용 프로그램 배포 및 다음 있습니다 이용 하는 이전 상태로 다시 이동 하는 재배포 기능.</span><span class="sxs-lookup"><span data-stu-id="ae33a-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="ae33a-428">작업 1-Geek 퀴즈 응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae33a-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="ae33a-429">이 태스크에서는 코드의 작은 조각을 리팩터링 합니다 **TriviaController** 클래스의 새 메서드로 데이터베이스에서 선택한 퀴즈 옵션을 검색 하는 논리 부분을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="ae33a-430">사용 하 여 Visual Studio 인스턴스를 전환 합니다 **GeekQuiz** 이전 연습에서 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="ae33a-431">**솔루션 탐색기**오픈를 **TriviaController.cs** 파일을 **컨트롤러** 폴더.</span><span class="sxs-lookup"><span data-stu-id="ae33a-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="ae33a-432">찾을 합니다 **StoreAsync** 메서드와 다음 그림에 강조 표시 된 코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![코드를 선택합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="ae33a-434">*코드를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-434">*Selecting the code*</span></span>
4. <span data-ttu-id="ae33a-435">확장 하 고, 선택한 코드를 마우스 오른쪽 단추로 클릭 합니다 **리팩터링** 선택한 메뉴 **메서드 추출...** .</span><span class="sxs-lookup"><span data-stu-id="ae33a-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![새 메서드로 코드를 추출합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="ae33a-437">*Extract 메서드를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="ae33a-438">에 **메서드 추출** 대화 상자에서 새 메서드 이름 *MatchesOption* 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![메서드 이름을 지정합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="ae33a-440">*추출한 메서드에 대 한 이름을 지정합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="ae33a-441">선택한 코드를 다음으로 추출 합니다 **MatchesOption** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ae33a-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="ae33a-442">결과 코드는 다음 코드 조각에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="ae33a-443">키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="ae33a-444">작업 2-Geek 퀴즈 응용 프로그램을 재배포</span><span class="sxs-lookup"><span data-stu-id="ae33a-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="ae33a-445">이제 프로덕션 환경에 새 배포를 트리거할 리포지토리에 이전 태스크에서 수행한 변경 내용을 푸시할가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="ae33a-446">사용 하 여 문제를 트러블 슈팅는 그런 다음 합니다 **F12 개발 도구** Internet Explorer에서 제공 하 고 Azure 관리 포털에서 롤백 이전 배포를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="ae33a-447">새 **Git Bash** Azure App Service에 대 한 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="ae33a-448">Azure에 변경 내용을 적용 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="ae33a-449">업데이트를 *[YOUR 응용 프로그램 경로]* 에 대 한 경로 사용 하 여 자리 표시자를 **GeekQuiz** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="ae33a-450">배포 암호에 대 한 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![리팩터링된 코드에서 Azure로 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="ae33a-452">*리팩터링된 코드에서 Azure로 푸시*</span><span class="sxs-lookup"><span data-stu-id="ae33a-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="ae33a-453">Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="ae33a-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="ae33a-454">이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="ae33a-455">키를 눌러 **F12** 개발 도구를 시작 하려면 합니다 **네트워크** 탭을 클릭 합니다 **재생** 기록을 시작 하려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="ae33a-456">![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "네트워크 녹음/녹화 시작")</span><span class="sxs-lookup"><span data-stu-id="ae33a-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="ae33a-457">*네트워크 녹음/녹화 시작*</span><span class="sxs-lookup"><span data-stu-id="ae33a-457">*Starting network recording*</span></span>
5. <span data-ttu-id="ae33a-458">퀴즈의 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-458">Select any option of the quiz.</span></span> <span data-ttu-id="ae33a-459">아무 작업도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="ae33a-460">에 **F12** 창에서 POST HTTP 요청에 해당 항목은 HTTP를 보여 줍니다 **500** 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 오류](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="ae33a-462">*HTTP 500 오류*</span><span class="sxs-lookup"><span data-stu-id="ae33a-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="ae33a-463">선택 된 **콘솔** 탭 합니다. 오류 원인의 세부 정보를 사용 하 여 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![로그인된 오류](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="ae33a-465">*로그인된 오류*</span><span class="sxs-lookup"><span data-stu-id="ae33a-465">*Logged error*</span></span>
8. <span data-ttu-id="ae33a-466">오류 세부 정보 부분을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-466">Locate the details part of the error.</span></span> <span data-ttu-id="ae33a-467">물론이 오류는 이전 단계에서 커밋된 있습니다 리팩터링 코드에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="ae33a-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span><span class="sxs-lookup"><span data-stu-id="ae33a-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="ae33a-469">브라우저를 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ae33a-469">Do not close the browser.</span></span>
10. <span data-ttu-id="ae33a-470">새 브라우저 인스턴스를 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com) 구독과 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="ae33a-471">선택 **Websites** 연습 2에서 만든 웹 앱을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="ae33a-472">로 이동 합니다 **배포** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="ae33a-473">모든 커밋을 수행 하는 배포 기록에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![기존 배포의 목록](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="ae33a-475">*기존 배포의 목록*</span><span class="sxs-lookup"><span data-stu-id="ae33a-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="ae33a-476">이전 커밋을 선택 하 고 클릭 **재배포** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![이전 커밋 재배포](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="ae33a-478">*이전 커밋 재배포*</span><span class="sxs-lookup"><span data-stu-id="ae33a-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="ae33a-479">확인 대화 상자가 나타나면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-479">When prompted to confirm, click **Yes**.</span></span>

    ![재배포를 확인합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="ae33a-481">배포가 완료 되 면 웹 앱 및 키를 눌러 브라우저 인스턴스를 다시 전환 **ctrl+f5**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="ae33a-482">옵션 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-482">Click any of the options.</span></span> <span data-ttu-id="ae33a-483">위치 및 결과 플립 애니메이션이 수행 됩니다 (*수정/잘못 된*) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="ae33a-484">(선택 사항) 으로 전환 합니다 **Git Bash** 콘솔 및 이전 커밋으로 되돌리려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-485">이러한 명령에 잘못 된 커밋의 Git 리포지토리에 모든 변경 내용을 실행 취소 하는 새 커밋이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="ae33a-486">Azure 새 커밋을 사용 하 여 응용 프로그램을 재배포 후 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="ae33a-487">실습 4: Azure Storage를 사용 하 여 확장</span><span class="sxs-lookup"><span data-stu-id="ae33a-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="ae33a-488">**Blob** 많은 양의 구조화 되지 않은 텍스트 또는 비디오, 오디오 및 이미지와 같은 이진 데이터를 저장 하는 가장 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="ae33a-489">저장소에 응용 프로그램의 정적 콘텐츠를 이동, 브라우저에 직접 이미지 또는 문서를 제공 함으로써 응용 프로그램을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="ae33a-490">이 연습에서는 Blob 컨테이너에 응용 프로그램의 정적 콘텐츠를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="ae33a-491">추가할 응용 프로그램을 구성 하는 다음을 **ASP.NET URL 재작성 규칙** 에 **Web.config** Blob 컨테이너에 콘텐츠를 리디렉션할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="ae33a-492">작업 1-Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ae33a-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="ae33a-493">이 작업을 관리 포털을 사용 하 여 새 저장소 계정을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="ae33a-494">로 이동 합니다 [Azure 관리 포털](https://manage.windowsazure.com) 구독과 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="ae33a-495">선택 **새 | Data Services | 저장소 | 빠른 생성** 새 저장소 계정 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="ae33a-496">선택한 계정에 대 한 고유한 이름을 입력 한 **지역** 목록에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="ae33a-497">클릭 **Storage 계정 만들기** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="ae33a-498">![새 저장소 계정을 만들](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "새 저장소 계정 만들기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="ae33a-499">*새 저장소 계정 만들기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="ae33a-500">에 **저장소** 섹션에서 새 저장소 계정의 상태가으로 변경 될 때까지 기다립니다 *Online* 다음 단계를 진행 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="ae33a-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="ae33a-501">![만든 저장소 계정](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "만든 저장소 계정")</span><span class="sxs-lookup"><span data-stu-id="ae33a-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="ae33a-502">*만든 저장소 계정*</span><span class="sxs-lookup"><span data-stu-id="ae33a-502">*Storage Account created*</span></span>
4. <span data-ttu-id="ae33a-503">저장소 계정 이름을 클릭 한 다음 클릭 합니다 **대시보드** 페이지의 맨 위에 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="ae33a-504">합니다 **대시보드** 페이지 계정과 응용 프로그램 내에서 사용할 수 있는 서비스 끝점의 상태에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="ae33a-505">![저장소 계정 대시보드 표시](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "저장소 계정 대시보드를 표시 합니다.")</span><span class="sxs-lookup"><span data-stu-id="ae33a-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="ae33a-506">*저장소 계정 대시보드를 표시합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="ae33a-507">클릭 합니다 **액세스 키 관리** 탐색 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="ae33a-508">![관리 액세스 키 단추](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "액세스 키 관리 단추")</span><span class="sxs-lookup"><span data-stu-id="ae33a-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="ae33a-509">*관리 액세스 키 단추*</span><span class="sxs-lookup"><span data-stu-id="ae33a-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="ae33a-510">에 **액세스 키 관리** 대화 상자에서 복사를 **저장소 계정 이름** 및 **기본 액세스 키** 다음 예에서는 해당 필요 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="ae33a-511">그런 다음 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="ae33a-512">![관리 액세스 키 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "액세스 키 관리 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="ae33a-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="ae33a-513">*관리 액세스 키 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="ae33a-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="ae33a-514">작업 2-Azure Blob Storage에 자산 업로드</span><span class="sxs-lookup"><span data-stu-id="ae33a-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="ae33a-515">이 태스크에서는 저장소 계정에 연결 하려면 Visual Studio에서 서버 탐색기 창을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="ae33a-516">다음 blob 컨테이너를 만들고 컨테이너에 도전할 퀴즈 로고를 사용 하 여 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="ae33a-517">사용 하 여 Visual Studio 인스턴스를 전환 합니다 **GeekQuiz** 이전 연습에서 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="ae33a-518">메뉴 모음에서 선택 **뷰** 을 클릭 한 다음 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="ae33a-519">**서버 탐색기**, 마우스 오른쪽 단추로 클릭 합니다 **Azure** 노드와 선택 **Azure에 연결 하는 중...** . 구독에 연결 된 Microsoft 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![Windows Azure에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="ae33a-521">*Azure에 연결*</span><span class="sxs-lookup"><span data-stu-id="ae33a-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="ae33a-522">확장 된 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **저장소** 선택한 **외부 저장소 연결 하는 중...** .</span><span class="sxs-lookup"><span data-stu-id="ae33a-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="ae33a-523">에 **새 저장소 계정 추가** 대화 상자에 입력를 **계정 이름** 및 **계정 키** 고 이전 작업에서 가져온 **확인**.</span><span class="sxs-lookup"><span data-stu-id="ae33a-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![새 저장소 계정 대화 상자를 추가 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="ae33a-525">*새 저장소 계정 대화 상자를 추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="ae33a-526">저장소 계정 아래에 표시 해야 합니다 **저장소** 노드.</span><span class="sxs-lookup"><span data-stu-id="ae33a-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="ae33a-527">저장소 계정을 확장 하 고 마우스 오른쪽 단추로 클릭 **Blob** 선택한 **Blob 컨테이너 만들기...** .</span><span class="sxs-lookup"><span data-stu-id="ae33a-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="ae33a-528">![Blob 컨테이너 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob 컨테이너 만들기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="ae33a-529">*Blob 컨테이너 만들기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="ae33a-530">에 **Blob 컨테이너 만들기** 대화 상자, blob 컨테이너에 대 한 이름을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="ae33a-531">![Create Blob Container 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob 컨테이너 만들기 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="ae33a-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="ae33a-532">*Blob 컨테이너 만들기 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="ae33a-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="ae33a-533">새 blob 컨테이너에 추가 해야 합니다 **Blob** 노드.</span><span class="sxs-lookup"><span data-stu-id="ae33a-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="ae33a-534">컨테이너가 공개 되도록 컨테이너에 액세스 권한을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="ae33a-535">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **이미지** 선택한 컨테이너 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="ae33a-536">![컨테이너 속성을 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "컨테이너 속성 이미지")</span><span class="sxs-lookup"><span data-stu-id="ae33a-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="ae33a-537">*이미지 컨테이너 속성*</span><span class="sxs-lookup"><span data-stu-id="ae33a-537">*Images container properties*</span></span>
9. <span data-ttu-id="ae33a-538">에 **속성** 창에서 **공용 읽기 액세스** 에 **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="ae33a-539">![공용 읽기 액세스 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "공용 읽기 액세스 속성 변경")</span><span class="sxs-lookup"><span data-stu-id="ae33a-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="ae33a-540">*공용 읽기 액세스 속성 변경*</span><span class="sxs-lookup"><span data-stu-id="ae33a-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="ae33a-541">공용 액세스 속성을 변경 하려는 경우 메시지가 표시 되 면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="ae33a-542">![Microsoft Visual Studio 경고](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 경고")</span><span class="sxs-lookup"><span data-stu-id="ae33a-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="ae33a-543">*Microsoft Visual Studio 경고*</span><span class="sxs-lookup"><span data-stu-id="ae33a-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="ae33a-544">**서버 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **이미지** blob 컨테이너 및 선택 **Blob 컨테이너 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="ae33a-545">![Blob 컨테이너를 볼](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob 컨테이너 보기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="ae33a-546">*Blob 컨테이너 보기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-546">*View Blob Container*</span></span>
12. <span data-ttu-id="ae33a-547">이미지 컨테이너 새 창에서 열고는 항목이 없으면 범례가 표시 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="ae33a-548">클릭 합니다 **업로드** 아이콘 파일을 blob 컨테이너에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="ae33a-549">![항목이 없는 이미지 컨테이너가](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "항목이 없는 이미지 컨테이너")</span><span class="sxs-lookup"><span data-stu-id="ae33a-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="ae33a-550">*항목이 없는 이미지 컨테이너*</span><span class="sxs-lookup"><span data-stu-id="ae33a-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="ae33a-551">에 **Blob 업로드** 대화 상자에서 **자산** 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="ae33a-552">선택 된 **로고 big.png** 파일을 클릭 **오픈**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="ae33a-553">파일을 업로드할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="ae33a-554">업로드가 완료 되 면 이미지 컨테이너에 파일을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="ae33a-555">파일 항목을 마우스 오른쪽 단추로 누르고 **URL 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="ae33a-556">![Blob URL을 복사](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "blob 파일 URL 복사")</span><span class="sxs-lookup"><span data-stu-id="ae33a-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="ae33a-557">*Blob URL 복사*</span><span class="sxs-lookup"><span data-stu-id="ae33a-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="ae33a-558">Internet Explorer를 열고 URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="ae33a-559">다음 이미지는 브라우저에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="ae33a-560">![Windows Blob Storage에서 이미지 로고 big.png](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "저장소에서 big.png 로고 이미지")</span><span class="sxs-lookup"><span data-stu-id="ae33a-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="ae33a-561">*Azure Blob Storage에서 big.png 로고 이미지*</span><span class="sxs-lookup"><span data-stu-id="ae33a-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="ae33a-562">작업 3 – Azure Blob Storage에서 정적 콘텐츠를 사용 하는 솔루션 업데이트</span><span class="sxs-lookup"><span data-stu-id="ae33a-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="ae33a-563">이 태스크에서는 구성 된 **GeekQuiz** 이미지를 사용 하는 솔루션 Azure Blob Storage에 업로드 (대신 웹 앱에 있는 이미지)에서 ASP.NET URL 다시 쓰기 규칙을 추가 하 여는 **web.config**파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="ae33a-564">Visual Studio에서 엽니다는 **Web.config** 파일을 **GeekQuiz** 찾아서 프로젝트를 **&lt;system.webServer&gt;** 요소.</span><span class="sxs-lookup"><span data-stu-id="ae33a-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="ae33a-565">저장소 계정 이름을 사용 하 여 자리 표시자를 업데이트는 URL 재작성 규칙을 추가 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="ae33a-566">(코드 조각- *WebSitesInProduction-Ex4-UrlRewriteRule*)</span><span class="sxs-lookup"><span data-stu-id="ae33a-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="ae33a-567">URL 재작성은 들어오는 웹 요청을 가로채 고 다른 리소스에 요청을 리디렉션하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="ae33a-568">URL 재작성 규칙에 요청을 필요로 하는 경우가 이러한 리디렉션되는 재작성 엔진을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="ae33a-569">재작성 규칙을 두 개의 문자열로 구성 되기: 요청한 URL에서 찾을 패턴 (일반적으로 사용 하 여 정규식)을 하는 경우를 사용 하 여 패턴을 바꿀 문자열을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="ae33a-570">자세한 내용은 [ASP.NET의 URL 재작성](https://msdn.microsoft.com/library/ms972974.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="ae33a-571">키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="ae33a-572">새 **Git Bash** Azure App Service에 대 한 업데이트 된 응용 프로그램을 배포 하는 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="ae33a-573">Azure에 변경 내용을 적용 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="ae33a-574">업데이트를 *[YOUR 응용 프로그램 경로]* 에 대 한 경로 사용 하 여 자리 표시자를 **GeekQuiz** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="ae33a-575">배포 암호에 대 한 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure에 배포 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="ae33a-577">*Azure에 배포 업데이트*</span><span class="sxs-lookup"><span data-stu-id="ae33a-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="ae33a-578">작업 4-확인</span><span class="sxs-lookup"><span data-stu-id="ae33a-578">Task 4 – Verification</span></span>

<span data-ttu-id="ae33a-579">이 작업에서는 사용 하 여 **Internet Explorer** 이동할 합니다 **매니아 퀴즈** 응용 프로그램 및 확인을 URL 재작성 규칙 이미지 작동 하는 사용자가 리디렉션됩니다에서 호스팅되는 이미지가 **Azure Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="ae33a-580">Internet Explorer를 열고 웹 앱으로 이동 (예: `http://<your-web-site>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="ae33a-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="ae33a-581">이전에 만든된 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="ae33a-582">![이미지를 사용 하 여 Geek 퀴즈 웹 앱을 보여 주는](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "이미지로 Geek 퀴즈 웹 앱을 표시")</span><span class="sxs-lookup"><span data-stu-id="ae33a-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="ae33a-583">*이미지를 사용 하 여 Geek 퀴즈 웹 앱을 표시*</span><span class="sxs-lookup"><span data-stu-id="ae33a-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="ae33a-584">키를 눌러 **F12** 개발 도구를 시작 하려면 선택 합니다 **네트워크** 탭 및 기록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="ae33a-585">![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "네트워크 녹음/녹화 시작")</span><span class="sxs-lookup"><span data-stu-id="ae33a-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="ae33a-586">*네트워크 녹음/녹화 시작*</span><span class="sxs-lookup"><span data-stu-id="ae33a-586">*Starting network recording*</span></span>
3. <span data-ttu-id="ae33a-587">키를 눌러 **ctrl+f5** 웹 페이지를 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="ae33a-588">HTTP 요청에 대 한 페이지 로드가 완료 되 면 표시 합니다 **/img/logo-big.png** HTTP 사용 하 여 URL **301** (리디렉션) 결과 및 다른 요청을 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` HTTP사용하여URL**200** 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="ae33a-589">![확인 URL 리디렉션](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "리디렉션 개발 도구에 표시")</span><span class="sxs-lookup"><span data-stu-id="ae33a-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="ae33a-590">*URL 리디렉션 확인*</span><span class="sxs-lookup"><span data-stu-id="ae33a-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="ae33a-591">실습 5: 웹 앱에 대 한 자동 크기 조정 사용</span><span class="sxs-lookup"><span data-stu-id="ae33a-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="ae33a-592">웹 부하에 대 한 지원이 필요 하므로이 실습은 선택 사항 &amp; 에서만 사용할 수 있는 성능 테스트 **Visual Studio 2013 Ultimate Edition**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="ae33a-593">Visual Studio 2013의 특정 기능에 대 한 자세한 내용은 버전 비교 [여기](https://www.microsoft.com/visualstudio/eng/products/compare)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>


<span data-ttu-id="ae33a-594">**Azure App Service Web Apps** 에서 실행 중인 웹 앱에 대 한 자동 크기 조정 기능을 제공 **표준 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="ae33a-595">자동 크기 조정에 Azure를 부하에 따라 웹 앱의 인스턴스 수를 자동으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="ae33a-596">자동 크기 조정 설정 되 면 Azure 웹 앱의 CPU가 5 분 마다 한 번 확인 하 고 해당 시점에 필요한 만큼 인스턴스가 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="ae33a-597">CPU 사용량이 낮은 경우 인스턴스가 제거 됩니다 두 시간 마다 한 번씩 웹 앱의 성능을 성능이 저하 되었음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="ae33a-598">이 연습에서 구성 하는 데 필요한 단계를 통해 이동 합니다 **자동 크기 조정** 에 대 한 기능을 **Geek 퀴즈** 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="ae33a-599">인스턴스를 업그레이드 하는 트리거를 응용 프로그램에서 충분 한 CPU 부하를 생성 하는 Visual Studio 부하 테스트를 실행 하 여이 기능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="ae33a-600">작업 1-CPU 메트릭을 기반으로 구성 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="ae33a-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="ae33a-601">이 태스크에서는 연습 2에서 만든 웹 앱에 대 한 자동 크기 조정 기능을 사용 하려면 Azure 관리 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="ae33a-602">에 [Azure 관리 포털](https://manage.windowsazure.com/)를 선택 **웹 사이트** 연습 2에서 만든 웹 앱을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="ae33a-603">로 이동 합니다 **확장** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="ae33a-604">아래는 **용량** 섹션에서 **CPU** 에 대 한 합니다 **메트릭 별 크기 조정** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-605">CPU 별 크기 조정 하는 경우 Azure CPU 사용량을 변경 하는 경우 앱을 사용 하는 인스턴스 수를 동적으로 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="ae33a-606">![CPU 별 크기 조정 하도록 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "자동 크기 조정에 대 한 CPU 메트릭 선택")</span><span class="sxs-lookup"><span data-stu-id="ae33a-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="ae33a-607">*CPU 별 크기 조정 하도록 선택*</span><span class="sxs-lookup"><span data-stu-id="ae33a-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="ae33a-608">변경 된 **대상 CPU** 구성을 **20**-**40** 백분율입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-609">이 범위는 웹 앱에 대 한 평균 CPU 사용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="ae33a-610">Azure을 추가 하거나이 범위에서 웹 앱을 유지 하도록 인스턴스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="ae33a-611">에 지정 된 크기 조정 시 사용 되는 인스턴스의 최소 및 최대 수를 **인스턴스 수** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="ae33a-612">Azure 위나 제한을 벗어나서 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="ae33a-613">기본값 **대상 CPU** 값은이 랩의 목적에 대해서만 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="ae33a-614">작은 값을 사용 하 여 CPU 범위를 구성 하 여 보통 수준의 부하는 응용 프로그램에 배치 되 면 자동 크기 조정 트리거와 가능성은 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="ae33a-615">![변경 대상 CPU 20%에서 40% 사이 여야](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "20%에서 40% 사이 여야 CPU 대상 변경")</span><span class="sxs-lookup"><span data-stu-id="ae33a-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="ae33a-616">*변경 대상 CPU 20%에서 40% 사이 여야*</span><span class="sxs-lookup"><span data-stu-id="ae33a-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="ae33a-617">클릭 **저장할** 변경 내용을 저장 하려면 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="ae33a-618">작업 2-부하 테스트를 Visual Studio를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ae33a-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="ae33a-619">이제 **자동 크기 조정** 되었습니다 구성 만듭니다는 **웹 성능 및 부하 테스트 프로젝트** 웹 앱에서 일부 CPU 부하를 생성 하는 Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="ae33a-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="ae33a-620">오픈 **Visual Studio Ultimate 2013** 선택한 **파일 | 새 | 프로젝트...**  새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="ae33a-621">![새 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="ae33a-622">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-622">*Creating a new project*</span></span>
2. <span data-ttu-id="ae33a-623">에 **새 프로젝트** 대화 상자에서 **웹 성능 및 부하 테스트 프로젝트** 아래에서 **Visual C# | 테스트** 탭 합니다. 했는지 **.NET Framework 4.5** 는 프로젝트의 이름을 선택 *WebAndLoadTestProject*, 선택는 **위치** 클릭 **확인**.</span><span class="sxs-lookup"><span data-stu-id="ae33a-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="ae33a-624">![새 웹 및 부하 테스트 프로젝트를 만드는](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "새 웹 및 부하 테스트 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="ae33a-625">*새 웹 및 부하 테스트 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="ae33a-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="ae33a-626">에 **WebTest1.webtest** 마우스 오른쪽 단추로 클릭 합니다 **WebTest1** 노드와 클릭 **요청 추가**.</span><span class="sxs-lookup"><span data-stu-id="ae33a-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="ae33a-627">![요청 WebTest1 추가할](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "WebTest1 요청 추가")</span><span class="sxs-lookup"><span data-stu-id="ae33a-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="ae33a-628">*WebTest1 요청 추가*</span><span class="sxs-lookup"><span data-stu-id="ae33a-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="ae33a-629">에 **속성** 창 새 요청 노드의 업데이트는 **Url** 웹 앱의 URL을 가리키도록 속성 (예: *[ http://geek-quiz.azurewebsites.net/ ](http://geek-quiz.azurewebsites.net/)*).</span><span class="sxs-lookup"><span data-stu-id="ae33a-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="ae33a-630">![Url 속성을 변경](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url 속성 변경")</span><span class="sxs-lookup"><span data-stu-id="ae33a-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="ae33a-631">*Url 속성 변경*</span><span class="sxs-lookup"><span data-stu-id="ae33a-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="ae33a-632">에 **WebTest1.webtest** 창에서 마우스 오른쪽 단추로 클릭 **WebTest1** 클릭 하 고 **루프 추가...** .</span><span class="sxs-lookup"><span data-stu-id="ae33a-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="ae33a-633">![WebTest1에 루프 추가](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "WebTest1에 루프 추가")</span><span class="sxs-lookup"><span data-stu-id="ae33a-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="ae33a-634">*WebTest1에 루프 추가*</span><span class="sxs-lookup"><span data-stu-id="ae33a-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="ae33a-635">에 **루프에 조건부 규칙 추가 및 항목** 대화 상자에서를 **For 루프** 규칙 및 다음 속성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="ae33a-636">**종료 값:** 1000</span><span class="sxs-lookup"><span data-stu-id="ae33a-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="ae33a-637">**컨텍스트 매개 변수 이름:** 반복기</span><span class="sxs-lookup"><span data-stu-id="ae33a-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="ae33a-638">**증가값:** 1</span><span class="sxs-lookup"><span data-stu-id="ae33a-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="ae33a-639">![루프에 대 한 규칙을 선택 하 고 속성을 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "루프에 대 한 규칙을 선택 하 고 속성 업데이트")</span><span class="sxs-lookup"><span data-stu-id="ae33a-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="ae33a-640">*루프에 대 한 규칙을 선택 하 고 속성 업데이트*</span><span class="sxs-lookup"><span data-stu-id="ae33a-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="ae33a-641">아래는 **루프의 항목** 섹션 루프에 대 한 첫 번째 및 마지막 항목이 이전에 만든 요청을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="ae33a-642">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="ae33a-643">![루프에 대 한 첫 번째 및 마지막 항목 선택](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "루프에 대 한 첫 번째 및 마지막 항목 선택")</span><span class="sxs-lookup"><span data-stu-id="ae33a-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="ae33a-644">*루프에 대 한 첫 번째 및 마지막 항목 선택*</span><span class="sxs-lookup"><span data-stu-id="ae33a-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="ae33a-645">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **WebAndLoadTestProject** 프로젝트를 확장 하 고는 **추가** 메뉴를 선택 **부하 테스트...** .</span><span class="sxs-lookup"><span data-stu-id="ae33a-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="ae33a-646">![부하 테스트 프로젝트에 추가 WebAndLoadTestProject](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject 프로젝트에 부하 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="ae33a-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="ae33a-647">*부하 테스트 프로젝트에 추가 WebAndLoadTestProject*</span><span class="sxs-lookup"><span data-stu-id="ae33a-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="ae33a-648">에 **부하 테스트 새로 만들기 마법사** 대화 상자, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="ae33a-649">![부하 테스트 새로 만들기 마법사](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "부하 테스트 새로 만들기 마법사")</span><span class="sxs-lookup"><span data-stu-id="ae33a-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="ae33a-650">*부하 테스트 새로 만들기 마법사*</span><span class="sxs-lookup"><span data-stu-id="ae33a-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="ae33a-651">에 **시나리오** 페이지에서 **인지 시간을 사용 하지 마십시오** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="ae33a-652">![선택 하면 대기 시간을 사용할 수 없습니다](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "를 인지 시간을 사용 하지 않도록 선택 하면")</span><span class="sxs-lookup"><span data-stu-id="ae33a-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="ae33a-653">*인지 시간을 사용 하 여 선택 하지 않음*</span><span class="sxs-lookup"><span data-stu-id="ae33a-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="ae33a-654">에 **부하 패턴** 페이지에서 확인 합니다 **일정 부하** 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="ae33a-655">변경 합니다 **사용자 수** 설정을 **250** 사용자 및 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="ae33a-656">![사용자 수가 250으로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "250 사용자 수를 변경 합니다.")</span><span class="sxs-lookup"><span data-stu-id="ae33a-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="ae33a-657">*사용자 수가 250으로 변경*</span><span class="sxs-lookup"><span data-stu-id="ae33a-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="ae33a-658">에 **테스트 조합 모델** 페이지에서 **순차적 테스트 순서 기반** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="ae33a-659">![테스트 조합 모델 선택](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "테스트 조합 모델 선택")</span><span class="sxs-lookup"><span data-stu-id="ae33a-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="ae33a-660">*테스트 조합 모델 선택*</span><span class="sxs-lookup"><span data-stu-id="ae33a-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="ae33a-661">에 **테스트 조합 모델** 페이지에서 **추가...**  조합에 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="ae33a-662">![테스트 조합에 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "테스트 조합에 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="ae33a-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="ae33a-663">*테스트 조합에 테스트 추가*</span><span class="sxs-lookup"><span data-stu-id="ae33a-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="ae33a-664">에 **테스트 추가** 대화 상자에서 두 번 클릭 **WebTest1** 테스트를 추가 합니다 **선택한 테스트** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="ae33a-665">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="ae33a-666">![WebTest1 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "WebTest1 테스트 추가")</span><span class="sxs-lookup"><span data-stu-id="ae33a-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="ae33a-667">*WebTest1 테스트 추가*</span><span class="sxs-lookup"><span data-stu-id="ae33a-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="ae33a-668">다시 합니다 **테스트 조합** 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="ae33a-669">![완료 테스트 조합 페이지](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "완료 테스트 조합 페이지")</span><span class="sxs-lookup"><span data-stu-id="ae33a-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="ae33a-670">*완료 테스트 조합 페이지*</span><span class="sxs-lookup"><span data-stu-id="ae33a-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="ae33a-671">에 **네트워크 조합** 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="ae33a-672">![네트워크 조합 페이지에서 다음을 클릭 하면](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "네트워크 조합 페이지에서 다음을 클릭 하면")</span><span class="sxs-lookup"><span data-stu-id="ae33a-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="ae33a-673">*네트워크 조합 페이지에서 다음을 클릭*</span><span class="sxs-lookup"><span data-stu-id="ae33a-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="ae33a-674">에 **브라우저 조합** 페이지에서 **Internet Explorer 10.0** 브라우저 종류와 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="ae33a-675">![브라우저 종류를 선택 하면](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "브라우저 종류를 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="ae33a-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="ae33a-676">*브라우저 종류를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="ae33a-677">에 **카운터 집합** 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="ae33a-678">![카운터 집합 페이지에서 다음을 클릭](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "카운터 집합 페이지에서 다음 클릭")</span><span class="sxs-lookup"><span data-stu-id="ae33a-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="ae33a-679">*카운터 집합 페이지에서 다음을 클릭합니다.*</span><span class="sxs-lookup"><span data-stu-id="ae33a-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="ae33a-680">에 **실행 설정** 페이지에서 설정 합니다 **부하 테스트 지속 시간** 를 **5 분** 클릭 **완료**.</span><span class="sxs-lookup"><span data-stu-id="ae33a-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="ae33a-681">![부하 테스트 지속 시간을 5 분으로 설정](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "부하 테스트 지속 시간을 5 분으로 설정")</span><span class="sxs-lookup"><span data-stu-id="ae33a-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="ae33a-682">*부하 테스트 지속 시간을 5 분으로 설정*</span><span class="sxs-lookup"><span data-stu-id="ae33a-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="ae33a-683">**솔루션 탐색기**를 두 번 클릭 합니다 **Local.settings** 테스트 설정을 탐색 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="ae33a-684">기본적으로 Visual Studio는 테스트를 실행 하려면 로컬 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-685">또는 사용 하 여 클라우드 부하 테스트를 실행 하려면 테스트 프로젝트를 구성할 수 있습니다 **Azure 테스트 계획**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="ae33a-686">테스트 계획을 azure 클라우드 기반 부하 테스트를 좀 더 현실적인 로드를 시뮬레이션 하는 서비스, CPU 용량, 사용 가능한 메모리 및 네트워크 대역폭과 같은 로컬 환경 제약 조건을 방지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="ae33a-687">Azure 테스트 계획을 사용 하 여 부하 테스트를 실행 하는 방법에 대 한 자세한 내용은 참조 하십시오 [부하 테스트 시나리오](/azure/devops/test/load-test/overview?view=vsts)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![테스트 설정](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="ae33a-689">작업 3 – 자동 크기 조정 확인</span><span class="sxs-lookup"><span data-stu-id="ae33a-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="ae33a-690">이제 이전 태스크에서 만든 부하 테스트를 실행 하 고 웹 앱 부하 상태에서 어떻게 동작 하는지 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="ae33a-691">**솔루션 탐색기**를 두 번 클릭 **LoadTest1.loadtest** 를 부하 테스트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="ae33a-692">![LoadTest1.loadtest 열기](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "LoadTest1.loadtest 열기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="ae33a-693">*열기 LoadTest1.loadtest*</span><span class="sxs-lookup"><span data-stu-id="ae33a-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="ae33a-694">에 **LoadTest1.loadtest** 창에서 부하 테스트를 실행 하려면 도구 상자에서 첫 번째 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="ae33a-695">![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "부하 테스트 실행")</span><span class="sxs-lookup"><span data-stu-id="ae33a-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="ae33a-696">*부하 테스트 실행*</span><span class="sxs-lookup"><span data-stu-id="ae33a-696">*Running the load test*</span></span>
3. <span data-ttu-id="ae33a-697">부하 테스트가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-698">부하 테스트는 동시에 웹 앱에 요청을 전송 하는 여러 사용자를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="ae33a-699">테스트를 실행 하는 경우에 모든 오류, 경고 또는 부하 테스트 실행에 관련 된 기타 정보를 검색 하려면 사용 가능한 카운터를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="ae33a-700">![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "부하 테스트가 완료 될 때까지 대기")</span><span class="sxs-lookup"><span data-stu-id="ae33a-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="ae33a-701">*부하 테스트 실행*</span><span class="sxs-lookup"><span data-stu-id="ae33a-701">*Load test running*</span></span>
4. <span data-ttu-id="ae33a-702">테스트가 완료 되 면 관리 포털로 돌아가서로 이동 합니다 **확장** 웹 앱의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="ae33a-703">아래는 **용량** 섹션인 표시 그래프의 새 인스턴스를 자동으로 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![새 인스턴스를 자동으로 배포](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="ae33a-705">*새 인스턴스를 자동으로 배포*</span><span class="sxs-lookup"><span data-stu-id="ae33a-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae33a-706">변경 내용을 그래프에 표시 하려면 몇 분 정도 걸릴 수 있습니다 (키를 눌러 **ctrl+f5** 주기적으로 페이지를 새로).</span><span class="sxs-lookup"><span data-stu-id="ae33a-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="ae33a-707">모든 변경 내용이 표시 되지 않으면, 다음을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="ae33a-708">부하 테스트 시간을 증가 시킬 (예: **10 분**)</span><span class="sxs-lookup"><span data-stu-id="ae33a-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="ae33a-709">최대값과 최소값을 줄일 합니다 **대상 CPU** 웹 앱의 자동 크기 조정 구성의 범위</span><span class="sxs-lookup"><span data-stu-id="ae33a-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="ae33a-710">사용 하 여 클라우드에서 부하 테스트 실행 **Azure 테스트 계획**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="ae33a-711">자세한 내용은 [여기](/azure/devops/test/load-test/index?view=vsts)</span><span class="sxs-lookup"><span data-stu-id="ae33a-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="ae33a-712">요약</span><span class="sxs-lookup"><span data-stu-id="ae33a-712">Summary</span></span>

<span data-ttu-id="ae33a-713">이 실습에서는 설정 하 고 응용 프로그램 Azure에서 프로덕션 웹 앱을 배포 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="ae33a-714">검색 하 고 사용 하 여 데이터베이스를 업데이트 하 여 시작 **Entity Framework Code First 마이그레이션을**를 사용 하 여 사이트의 새 버전을 배포 하 여 계속 **Git** 롤백 수행 하는 안정적인 최신 버전의 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="ae33a-715">또한 Blob 컨테이너에 정적 콘텐츠를 이동 하려면 저장소를 사용 하 여 앱의 크기를 조정 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ae33a-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
