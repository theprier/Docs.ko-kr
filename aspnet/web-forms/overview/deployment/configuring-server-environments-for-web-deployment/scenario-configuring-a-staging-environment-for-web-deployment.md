---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: '시나리오: 웹 배포용 스테이징 환경 구성 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 스테이징 환경에 대 한 일반적인 웹 배포 시나리오를 설명 하 고 유사한 env 설정 하기 위해 완료 해야 하는 태스크를 설명 하는 중...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 9c0f12645f10820996a03c232d20ee87031aefaa
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820803"
---
<a name="scenario-configuring-a-staging-environment-for-web-deployment"></a><span data-ttu-id="8ce0c-103">시나리오: 웹 배포용 스테이징 환경 구성</span><span class="sxs-lookup"><span data-stu-id="8ce0c-103">Scenario: Configuring a Staging Environment for Web Deployment</span></span>
====================
<span data-ttu-id="8ce0c-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="8ce0c-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="8ce0c-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="8ce0c-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="8ce0c-106">이 항목에서는 스테이징 환경에 대 한 일반적인 웹 배포 시나리오 및 유사한 환경을 설정 하기 위해 완료 해야 하는 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-106">This topic describes a typical web deployment scenario for a staging environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="8ce0c-107">조직은 많은 웹 응용 프로그램 또는 웹 사이트에 대 한 업데이트를 미리 보려면 스테이징 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-107">Lots of organizations use staging environments to preview updates to web applications or websites.</span></span> <span data-ttu-id="8ce0c-108">이렇게 하면 조직 내 사용자 탐색 하 고 사이트 "위치" 라이브"나 프로덕션 환경에 배포 즉 전에 새로운 기능 또는 콘텐츠를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-108">This gives people within the organization a chance to explore and review new functionality or content before the site "goes live," or in other words is deployed to a production environment.</span></span> <span data-ttu-id="8ce0c-109">스테이징 환경 현실적인 미리 보기를 제공 하기 위해 프로덕션 환경을 최대한 근접 하 게 복제 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-109">The staging environment is designed to replicate the production environment as closely as possible, in order to provide a realistic preview.</span></span> <span data-ttu-id="8ce0c-110">일반적으로 이러한 종류의 스테이징 환경에 이러한 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-110">This kind of staging environment typically has these characteristics:</span></span>

- <span data-ttu-id="8ce0c-111">여러 부하 분산 된 웹 서버 및 하나 이상의 데이터베이스 서버를 장애 조치 클러스터링 및 데이터베이스 미러링을 사용 하 여 자주 환경 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="8ce0c-112">개발 팀 또는 팀 빌드 서버에서 자동으로 응용 프로그램을 수동으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-112">Applications may be deployed manually by a development team or automatically by a Team Build server.</span></span>
- <span data-ttu-id="8ce0c-113">사용자 또는 응용 프로그램을 배포 하는 프로세스 계정 가능성이 스테이징 서버에서 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-113">The users or process accounts that deploy applications are unlikely to have administrator privileges on the staging servers.</span></span>
- <span data-ttu-id="8ce0c-114">응용 프로그램을 변경을 자주 배포 되므로 단일 단계를 지원 해야 하는 환경 또는 배포를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-114">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="8ce0c-115">이 자습서의 범위를 벗어납니다 여러 서버에 데이터베이스 배포를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-115">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="8ce0c-116">이 영역에 대 한 자세한 내용은 참조 하세요 [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-116">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>


<span data-ttu-id="8ce0c-117">예를 들어, 우리의 [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) Contact Manager 솔루션을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-117">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) manages the Contact Manager solution.</span></span> <span data-ttu-id="8ce0c-118">Rob Walters, TFS 관리자는 개발자가 필요에 따라 스테이징 환경에 배포를 트리거할 수 있는 빌드 정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-118">The TFS administrator, Rob Walters, has created a build definition that lets developers trigger a deployment to the staging environment as required.</span></span>

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="8ce0c-119">메모는 대부분의 경우에서 않습니다 반드시를 스테이징 환경에 최신 빌드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-119">Note that in most cases, you won't necessarily want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="8ce0c-120">대신 가능성이 훨씬 더에 유효성 검사 및 테스트 환경에서 검증 되었습니다 이미는 특정 빌드를 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-120">Instead, you're a lot more likely to want to deploy a specific build that has already undergone validation and verification in the test environment.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="8ce0c-121">솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="8ce0c-121">Solution Overview</span></span>

<span data-ttu-id="8ce0c-122">이 시나리오에서 배포 요구 사항 분석에서 이러한 팩트를 추론할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-122">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="8ce0c-123">배포를 수행 하는 사용자 또는 프로세스 계정은 스테이징 웹 서버 관리자가 아닌 배포를 지원 해야 하므로 준비 서버에서 관리자 권한이 있어야 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-123">The user or process account that performs the deployment won't have administrator privileges on the staging servers, so the staging web servers must support non-administrator deployment.</span></span> <span data-ttu-id="8ce0c-124">따라서 원격 에이전트 대신 웹 배포 처리기를 사용 하도록 스테이징 웹 서버를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-124">As such, you'll need to configure the staging web servers to use the Web Deploy Handler rather than the remote agent.</span></span>
- <span data-ttu-id="8ce0c-125">스테이징 환경에 여러 웹 서버를 포함 하지만 웹 팜 프레임 워크 (WFF)를 사용 하 여 서버 팜을 만들도록 해야 하므로 한 번의 클릭 또는 자동화 된 배포를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-125">The staging environment includes multiple web servers, but it needs to support one-click or automated deployment, so you'll need to use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="8ce0c-126">이 방법을 사용 하면 하나의 웹 서버 (주 서버)에서 응용 프로그램을 배포할 수 있습니다 및 WFF 배포는 다른 모든 웹 서버에서 스테이징 환경에서 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-126">Using this approach, you can deploy an application to one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the staging environment.</span></span>
- <span data-ttu-id="8ce0c-127">사용자 또는 프로세스 계정 배포를 수행 하는 데이터베이스를 만들 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-127">The user or process account that performs the deployment must have permissions to create databases.</span></span> <span data-ttu-id="8ce0c-128">계정을 추가 해야 하는 이와 같이 합니다 **dbcreator** 원격 액세스 및 배포를 지원 하도록 데이터베이스 서버를 구성 하는 것 외에도 데이터베이스 서버의 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-128">As such, you'll need to add the account to the **dbcreator** server role on the database server, in addition to configuring the database server to support remote access and deployment.</span></span>

<span data-ttu-id="8ce0c-129">이러한 항목에는 이러한 작업을 완료 하기 위해 필요한 모든 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-129">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="8ce0c-130">[웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기](creating-a-server-farm-with-the-web-farm-framework.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-130">[Create a Server Farm with the Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md).</span></span> <span data-ttu-id="8ce0c-131">이 항목에서는 만들고 웹 플랫폼 제품 및 구성 요소, 구성 설정 및 웹 사이트 및 응용 프로그램은 여러 부하 분산 된 웹 서버에 걸쳐 복제 됩니다 있도록 WFF를 사용 하 여 서버 팜을 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-131">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="8ce0c-132">[웹 배포 게시용 웹 서버 구성 (웹 배포 처리기)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-132">[Configure a Web Server for Web Deploy Publishing (Web Deploy Handler)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="8ce0c-133">이 항목에서는 웹 배포 게시를 원격 에이전트 방식을 사용 하 여 Windows Server 2008 R2 빌드 정리에서 시작을 지 원하는 웹 서버를 구축 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-133">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="8ce0c-134">[웹 배포 게시용 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-134">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="8ce0c-135">이 항목에서는 원격 액세스 및 SQL Server 2008 R2의 기본 설치에서 시작 하는 배포를 지원 하기 위해 데이터베이스 서버를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-135">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="8ce0c-136">추가 정보</span><span class="sxs-lookup"><span data-stu-id="8ce0c-136">Further Reading</span></span>

<span data-ttu-id="8ce0c-137">일반적인 개발자 테스트 환경 구성에 대 한 지침을 참조 하세요 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-137">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="8ce0c-138">일반적인 프로덕션 환경 구성에 대 한 지침을 참조 하세요 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce0c-138">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8ce0c-139">[이전](scenario-configuring-a-test-environment-for-web-deployment.md)
> [다음](scenario-configuring-a-production-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="8ce0c-139">[Previous](scenario-configuring-a-test-environment-for-web-deployment.md)
[Next](scenario-configuring-a-production-environment-for-web-deployment.md)</span></span>
