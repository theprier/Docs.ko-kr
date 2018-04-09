---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 웹 배포에 대 한 서버 환경 구성 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 한 번 클릭 하거나 자동화 된 지원, 웹 사이트 배포 및 다른 다양 한 시나리오에는 게시에 대 한 서버 환경을 설정 하는 방법을 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: ff6118be618a170ac76d66a9de24a7b5cc2d840a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="configuring-server-environments-for-web-deployment"></a><span data-ttu-id="888d5-103">웹 배포에 대 한 서버 환경 구성</span><span class="sxs-lookup"><span data-stu-id="888d5-103">Configuring Server Environments for Web Deployment</span></span>
====================
<span data-ttu-id="888d5-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="888d5-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="888d5-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="888d5-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="888d5-106">이 자습서에서 한 번 클릭 하거나 자동화 된 지원, 웹 사이트 배포 및 서로 다른 다양 한 시나리오에는 게시에 대 한 서버 환경을 설정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-106">This tutorial will show you how to set up server environments to support one-click, or automated, website deployment and publishing in various different scenarios.</span></span> <span data-ttu-id="888d5-107">자습서 배포 하 고 제공 하는 시나리오 기반 개요와 함께 wff (웹 팜 프레임 워크) 서버 팜 설정 작업 관련 접근법을 지원 하도록 웹 서버를 구성 하는 등의 다양 한 작업을 완료 하는 과정을 안내 하는 데 유용한 항목에 포함 되어 상위 수준 종단 간 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-107">The tutorial includes topics to walk you through completing various tasks, like configuring a web server to support specific approaches to deployment and setting up a Web Farm Framework (WFF) server farm, together with scenario-based overviews that provide higher-level end-to-end guidance.</span></span>
> 
> <span data-ttu-id="888d5-108">이 자습서에 설명 된 Fabrikam, Inc. 배포 시나리오를 사용 하 여 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) 예제 및 네트워크 인프라에 대 한 참조 지점으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-108">The tutorial uses the Fabrikam, Inc. deployment scenario described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) as a reference point for examples and network infrastructure.</span></span>
> 
> <span data-ttu-id="888d5-109">다음 자습서는 이탈리아어로 번역에 대 한 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-109">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


<span data-ttu-id="888d5-110">이 자습서는 이러한 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-110">This tutorial includes these topics:</span></span>

- [<span data-ttu-id="888d5-111">웹 배포에 적합한 접근 방식 선택</span><span class="sxs-lookup"><span data-stu-id="888d5-111">Choosing the Right Approach to Web Deployment</span></span>](choosing-the-right-approach-to-web-deployment.md)
- [<span data-ttu-id="888d5-112">시나리오: 웹 배포용 테스트 환경 구성</span><span class="sxs-lookup"><span data-stu-id="888d5-112">Scenario: Configuring a Test Environment for Web Deployment</span></span>](scenario-configuring-a-test-environment-for-web-deployment.md)
- [<span data-ttu-id="888d5-113">시나리오: 웹 배포용 스테이징 환경 구성</span><span class="sxs-lookup"><span data-stu-id="888d5-113">Scenario: Configuring a Staging Environment for Web Deployment</span></span>](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [<span data-ttu-id="888d5-114">시나리오: 웹 배포용 프로덕션 환경 구성</span><span class="sxs-lookup"><span data-stu-id="888d5-114">Scenario: Configuring a Production Environment for Web Deployment</span></span>](scenario-configuring-a-production-environment-for-web-deployment.md)
- [<span data-ttu-id="888d5-115">웹 배포 게시용 웹 서버 구성(원격 에이전트)</span><span class="sxs-lookup"><span data-stu-id="888d5-115">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [<span data-ttu-id="888d5-116">웹 배포 게시용 웹 서버 구성(웹 배포 처리기)</span><span class="sxs-lookup"><span data-stu-id="888d5-116">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [<span data-ttu-id="888d5-117">웹 배포 게시용 웹 서버 구성(오프라인 배포)</span><span class="sxs-lookup"><span data-stu-id="888d5-117">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [<span data-ttu-id="888d5-118">웹 배포 게시용 데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="888d5-118">Configuring a Database Server for Web Deploy Publishing</span></span>](configuring-a-database-server-for-web-deploy-publishing.md)
- [<span data-ttu-id="888d5-119">웹 팜 프레임워크를 사용하여 서버 팜 만들기</span><span class="sxs-lookup"><span data-stu-id="888d5-119">Creating a Server Farm with the Web Farm Framework</span></span>](creating-a-server-farm-with-the-web-farm-framework.md)
- [<span data-ttu-id="888d5-120">대상 환경의 배포 속성 구성</span><span class="sxs-lookup"><span data-stu-id="888d5-120">Configuring Deployment Properties for a Target Environment</span></span>](configuring-deployment-properties-for-a-target-environment.md)

<span data-ttu-id="888d5-121">첫 번째 항목 [웹 배포에 대 한 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md), 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 웹 응용 프로그램을 게시 하는 데 기본 방법에 설명 2.0.</span><span class="sxs-lookup"><span data-stu-id="888d5-121">The first topic, [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md), describes the main approaches you can use to publish web applications by using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0.</span></span> <span data-ttu-id="888d5-122">또한 각 방법에 매핑되는 시나리오를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-122">It also identifies the scenarios that map to each approach.</span></span> <span data-ttu-id="888d5-123">여기에서 각 시나리오 항목 완료 하는 데 필요한 작업의 높은 수준의 개요를 제공 하 고 이러한 작업을 완료할 수 있도록를 통해 작업 해야 하는 항목을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-123">From here, each scenario topic provides a high-level overview of the tasks you need to complete and identifies the topics you'll need to work through to help you complete these tasks.</span></span>

<span data-ttu-id="888d5-124">설명 하는 분할 프로젝트 파일 방식은 사용 중인 경우 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md) 를 최종 항목에는 솔루션을 빌드하여 배포 [대상환경에대한배포속성구성](configuring-deployment-properties-for-a-target-environment.md), 다른 대상 환경에 배포에 대 한 환경 관련 프로젝트 파일을 구성 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-124">If you're using the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md) to build and deploy your solution, the final topic, [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md), describes how to configure environment-specific project files for deployment to different destination environments.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="888d5-125">핵심 기술</span><span class="sxs-lookup"><span data-stu-id="888d5-125">Key Technologies</span></span>

<span data-ttu-id="888d5-126">이 자습서는 웹 배포를 지원 하기 위해 이러한 제품 및 기술을 사용 하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-126">This tutorial focuses on how to use these products and technologies to support web deployment:</span></span>

- <span data-ttu-id="888d5-127">IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="888d5-127">IIS 7.5</span></span>
- <span data-ttu-id="888d5-128">웹 배포 2.x</span><span class="sxs-lookup"><span data-stu-id="888d5-128">Web Deploy 2.x</span></span>
- <span data-ttu-id="888d5-129">WFF 2.x</span><span class="sxs-lookup"><span data-stu-id="888d5-129">WFF 2.x</span></span>
- <span data-ttu-id="888d5-130">IIS 웹 관리 서비스 (WMSvc)</span><span class="sxs-lookup"><span data-stu-id="888d5-130">IIS Web Management Service (WMSvc)</span></span>

<span data-ttu-id="888d5-131">이 자습서는 Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0 및 ASP.NET MVC 3의 사용에는 대해서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-131">The tutorial also touches on the use of Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="888d5-132">이 시리즈의 다른 자습서</span><span class="sxs-lookup"><span data-stu-id="888d5-132">Other Tutorials in This Series</span></span>

<span data-ttu-id="888d5-133">이 엔터프라이즈급 웹 배포에는 일련의 5 개 자습서의 일부를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-133">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="888d5-134">다른 자습서 시리즈에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-134">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="888d5-135">[엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-135">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="888d5-136">이 소개 콘텐츠는 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-136">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="888d5-137">자습서 시나리오를 설명 하 고 작업 및 계열 전체에서 설명 하는 연습 광범위 한 관리 ALM (Application Lifecycle) 프로세스에 배치 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-137">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="888d5-138">[웹 배포는 기업에서](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-138">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="888d5-139">이 자습서는 Microsoft Build Engine (MSBuild) 프로젝트 파일에 대 한 개념 소개, 웹 게시 파이프라인, 웹 배포 및 기타 관련된 기술을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-139">This tutorial provides a conceptual introduction to Microsoft Build Engine (MSBuild) project files, the Web Publishing Pipeline, Web Deploy, and other related technologies.</span></span> <span data-ttu-id="888d5-140">방법을 함께 사용할 수 있습니다 이러한 도구 복잡 한 배포 프로세스를 관리 하에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-140">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="888d5-141">[웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-141">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="888d5-142">이 자습서에서는 Team Foundation Server (TFS) 및 특정 빌드의 배포를 수동으로 트리거되어 CI (연속 통합) 프로세스의 일부로 자동화 된 배포를 포함 하 여 다양 한 배포 시나리오를 지원 하도록 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-142">This tutorial describes how to configure Team Foundation Server (TFS) to support various deployment scenarios, including automated deployment as part of a continuous integration (CI) process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="888d5-143">[고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="888d5-143">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="888d5-144">이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더를 제외 하 고 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등의 다양 한 고급 배포 작업을 수행 하는 방법을 설명합니다 .</span><span class="sxs-lookup"><span data-stu-id="888d5-144">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="888d5-145">다음</span><span class="sxs-lookup"><span data-stu-id="888d5-145">Next</span></span>](choosing-the-right-approach-to-web-deployment.md)
