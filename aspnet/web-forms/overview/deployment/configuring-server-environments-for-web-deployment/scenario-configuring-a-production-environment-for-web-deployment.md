---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: '시나리오: 웹 배포용 프로덕션 환경 구성 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 프로덕션 환경에 대 한 일반적인 웹 배포 시나리오를 설명 하 고 유사한 설정 하기 위해 완료 해야 하는 태스크를 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: ff9a1e7657852f37b3dc4fc1dbc4f6e78e6427cb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370350"
---
<a name="scenario-configuring-a-production-environment-for-web-deployment"></a><span data-ttu-id="53974-103">시나리오: 웹 배포용 프로덕션 환경 구성</span><span class="sxs-lookup"><span data-stu-id="53974-103">Scenario: Configuring a Production Environment for Web Deployment</span></span>
====================
<span data-ttu-id="53974-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="53974-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="53974-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="53974-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="53974-106">이 항목에서는 프로덕션 환경에 대 한 일반적인 웹 배포 시나리오 및 유사한 환경을 설정 하기 위해 완료 해야 하는 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-106">This topic describes a typical web deployment scenario for a production environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="53974-107">프로덕션 환경은 웹 응용 프로그램 또는 웹 사이트에 대 한 최종 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="53974-107">The production environment is the final destination for a web application or a website.</span></span> <span data-ttu-id="53974-108">이 지점에서 응용 프로그램 테스트를 통해 되었습니다, 그리고 스테이징 환경에 배포한 이며 "go live." 준비 완료</span><span class="sxs-lookup"><span data-stu-id="53974-108">By this point, your application has been through testing, has been deployed to a staging environment, and is ready to "go live."</span></span> <span data-ttu-id="53974-109">프로덕션 환경의 특성은 특성 및 용도 웹 콘텐츠를 조직, 대상 그룹 및 많은 기타 요인의 크기에 따라 광범위 하 게 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53974-109">The characteristics of a production environment can vary widely according to the nature and purpose of your web content, the size of your organization, your target audience, and lots of other factors.</span></span> <span data-ttu-id="53974-110">엔터프라이즈 규모 시나리오에서는 프로덕션 환경 이러한 특성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53974-110">In an enterprise-scale scenario, the production environment may have these characteristics:</span></span>

- <span data-ttu-id="53974-111">여러 부하 분산 된 웹 서버 및 하나 이상의 데이터베이스 서버를 장애 조치 클러스터링 및 데이터베이스 미러링을 사용 하 여 자주 환경 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53974-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="53974-112">환경이 인터넷 경우 내부 네트워크에서 분리 되어야 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="53974-112">If the environment is Internet-facing, it's likely to be segregated from your internal network.</span></span> <span data-ttu-id="53974-113">경계 네트워크의 다른 서브넷에서 수행 될 수, 다른 도메인에서 수행 될 수 및 완전히 다른 네트워크 인프라에서 수행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53974-113">It may be on a different subnet in a perimeter network, it may be on a different domain, and it may be on an entirely different network infrastructure.</span></span>
- <span data-ttu-id="53974-114">개발자 및 빌드 서버 프로세스 계정 가능성이 항상 프로덕션 서버에서 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-114">Developers and build server process accounts are highly unlikely to have administrator privileges on the production servers.</span></span>
- <span data-ttu-id="53974-115">응용 프로그램에 대 한 변경 내용은 자주 테스트 또는 스테이징 배포에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53974-115">Changes to applications are deployed on a less frequent basis than test or staging deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="53974-116">이 자습서의 범위를 벗어납니다 여러 서버에 데이터베이스 배포를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-116">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="53974-117">이 영역에 대 한 자세한 내용은 참조 하세요 [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-117">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>


<span data-ttu-id="53974-118">예를 들어, 우리의 [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Build server Contact Manager 솔루션을 빌드 및 한 번에 스테이징 환경에 배포할 수 있도록 하는 빌드 정의 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-118">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), a Team Build server includes build definitions that let users build the Contact Manager solution and deploy it to a staging environment in a single step.</span></span> <span data-ttu-id="53974-119">응용 프로그램 보안 요구 사항과 네트워크 인프라에 의해 적용 된 제약 조건으로 인해 프로덕션에 배포할 준비가 되 면 프로덕션 환경 관리자가 수동으로 웹 패키지를 프로덕션 웹 서버로 복사 하며 가져오기 인터넷 정보 서비스 (IIS) 관리자를 통해 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-119">When the application is ready to be deployed to production, due to the constraints imposed by security requirements and the network infrastructure, the production environment administrator must manually copy the web package onto a production web server and import it through Internet Information Services (IIS) Manager.</span></span>

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a><span data-ttu-id="53974-120">솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="53974-120">Solution Overview</span></span>

<span data-ttu-id="53974-121">이 시나리오에서 배포 요구 사항 분석에서 이러한 팩트를 추론할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53974-121">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="53974-122">보안 제한 사항 및 네트워크 구성으로 인해 한 번의 클릭 또는 자동화 된 배포를 지원 하기 위해 프로덕션 환경을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53974-122">Due to security restrictions and the network configuration, you can't configure the production environment to support one-click or automated deployment.</span></span> <span data-ttu-id="53974-123">오프 라인 배포는이 시나리오에만 실행 가능한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="53974-123">Offline deployment is the only viable approach in this scenario.</span></span>
- <span data-ttu-id="53974-124">프로덕션 환경의 서버 팜을 만들려면 웹 팜 프레임 워크 (WFF)을 사용할 수 있도록 여러 웹 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-124">The production environment includes multiple web servers, so you can use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="53974-125">이 방법을 사용 하면 관리자만 하나의 웹 서버 (주 서버)에서 응용 프로그램을 가져올 하며 WFF는 프로덕션 환경에서 모든 다른 웹 서버에서 배포를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-125">Using this approach, the administrator only needs to import the application onto one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the production environment.</span></span>

<span data-ttu-id="53974-126">이러한 항목에는 이러한 작업을 완료 하기 위해 필요한 모든 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-126">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="53974-127">[웹 팜 프레임 워크를 사용 하 여 서버 팜 만들기](configuring-a-database-server-for-web-deploy-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-127">[Create a Server Farm with the Web Farm Framework](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="53974-128">이 항목에서는 만들고 웹 플랫폼 제품 및 구성 요소, 구성 설정 및 웹 사이트 및 응용 프로그램은 여러 부하 분산 된 웹 서버에 걸쳐 복제 됩니다 있도록 WFF를 사용 하 여 서버 팜을 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-128">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="53974-129">[웹 배포 게시용 (오프 라인 배포)에 대 한 웹 서버를 구성할](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-129">[Configure a Web Server for Web Deploy Publishing (Offline Deployment)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="53974-130">이 항목에서는 관리자 가져오기 및 웹 패키지를 수동으로 배포 하 여 Windows Server 2008 R2 빌드 정리를 시작 하도록 하는 웹 서버를 빌드하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-130">This topic describes how to build a web server that lets administrators import and deploy web packages manually, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="53974-131">[웹 배포 게시용 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-131">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="53974-132">이 항목에서는 원격 액세스 및 SQL Server 2008 R2의 기본 설치에서 시작 하는 배포를 지원 하기 위해 데이터베이스 서버를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-132">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="53974-133">추가 정보</span><span class="sxs-lookup"><span data-stu-id="53974-133">Further Reading</span></span>

<span data-ttu-id="53974-134">일반적인 개발자 테스트 환경 구성에 대 한 지침을 참조 하세요 [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-134">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="53974-135">일반적인 스테이징 환경 구성에 대 한 지침을 참조 하세요 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53974-135">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="53974-136">[이전](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [다음](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span><span class="sxs-lookup"><span data-stu-id="53974-136">[Previous](scenario-configuring-a-staging-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span></span>
