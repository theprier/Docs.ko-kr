---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 솔루션 | Microsoft Docs
author: jrjlee
description: 샘플 솔루션을 사용 하 여이 일련의 자습서&#x2014;Contact Manager 솔루션&#x2014;현실적인 수준으로 엔터프라이즈 규모 응용 프로그램을 나타내기 위해...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d7034f800df98747d10401d7e2c7297fea0e46d4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="the-contact-manager-solution"></a><span data-ttu-id="62e08-103">Contact Manager 솔루션</span><span class="sxs-lookup"><span data-stu-id="62e08-103">The Contact Manager Solution</span></span>
====================
<span data-ttu-id="62e08-104">으로 [Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="62e08-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="62e08-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="62e08-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="62e08-106">이 [일련의 자습서](web-deployment-in-the-enterprise.md) 샘플 솔루션을 사용 하 여&#x2014;Contact Manager 솔루션&#x2014;현실적인 수준의 복잡성으로 엔터프라이즈 규모 응용 프로그램을 나타내기 위해.</span><span class="sxs-lookup"><span data-stu-id="62e08-106">This [series of tutorials](web-deployment-in-the-enterprise.md) uses a sample solution&#x2014;the Contact Manager solution&#x2014;to represent an enterprise-scale application with a realistic level of complexity.</span></span> <span data-ttu-id="62e08-107">이 항목 Contact Manager 솔루션을 소개 하 고, 솔루션의 주요 구성 요소에 설명, 이러한 종류의 엔터프라이즈 환경에서 다양 한 대상 플랫폼에 응용 프로그램 배포에서 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-107">This topic introduces the Contact Manager solution, describes the key components of the solution, and identifies the challenges in deploying this kind of application to various destination platforms in an enterprise environment.</span></span>
> 
> <span data-ttu-id="62e08-108">이 자습서에는 항목을 진행할 때는 특정 한 엔터프라이즈 배포 시나리오 요구를 충족할 수 있는 방법을 보여 주는 참조 구현으로 Contact Manager 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-108">As you work through the topics in these tutorials, you can use the Contact Manager solution as a reference implementation that demonstrates how you can meet specific challenges in enterprise deployment scenarios.</span></span> <span data-ttu-id="62e08-109">다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-109">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>


## <a name="solution-overview"></a><span data-ttu-id="62e08-110">솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="62e08-110">Solution Overview</span></span>

<span data-ttu-id="62e08-111">Contact Manager 솔루션 4 개의 개별 프로젝트가 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-111">The Contact Manager solution consists of four individual projects:</span></span>

![](the-contact-manager-solution/_static/image1.png)

- <span data-ttu-id="62e08-112">**ContactManager.Mvc**.</span><span class="sxs-lookup"><span data-stu-id="62e08-112">**ContactManager.Mvc**.</span></span> <span data-ttu-id="62e08-113">이 ASP.NET MVC 3 웹 응용 프로그램 프로젝트를 솔루션에 대 한 진입점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-113">This is an ASP.NET MVC 3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="62e08-114">만들고 연락처 세부 정보를 볼 수 있는 사용자가 제공 하는 등 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-114">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="62e08-115">응용 프로그램 연락처와 인증 및 권한 부여를 관리 하는 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하려면 Windows Communication Foundation (WCF) 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-115">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="62e08-116">**ContactManager.Database**.</span><span class="sxs-lookup"><span data-stu-id="62e08-116">**ContactManager.Database**.</span></span> <span data-ttu-id="62e08-117">이것이 Visual Studio 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-117">This is a Visual Studio database project.</span></span> <span data-ttu-id="62e08-118">프로젝트는 저장소 연락처 세부 정보는 데이터베이스에 대 한 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-118">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="62e08-119">**ContactManager.Service**.</span><span class="sxs-lookup"><span data-stu-id="62e08-119">**ContactManager.Service**.</span></span> <span data-ttu-id="62e08-120">이 WCF 웹 서비스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-120">This is a WCF web service project.</span></span> <span data-ttu-id="62e08-121">검색, 업데이트 및 삭제 (CRUD) 작업에서 수행 하는 호출자를 허용 하는 끝점을 만들려면 WCF 서비스 노출 된 **ContactManager** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-121">The WCF service exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the **ContactManager** database.</span></span> <span data-ttu-id="62e08-122">서비스는 **ContactManager** 데이터베이스 및 **ContactManager.Common.dll** 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-122">The service relies on the **ContactManager** database and the **ContactManager.Common.dll** assembly.</span></span>
- <span data-ttu-id="62e08-123">**ContactManager.Common**.</span><span class="sxs-lookup"><span data-stu-id="62e08-123">**ContactManager.Common**.</span></span> <span data-ttu-id="62e08-124">이 클래스 라이브러리 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-124">This is a class library project.</span></span> <span data-ttu-id="62e08-125">WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-125">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="62e08-126">솔루션에는 게시 라는 솔루션 폴더를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-126">The solution also includes a solution folder named Publish.</span></span> <span data-ttu-id="62e08-127">다양 한 사용자 지정 프로젝트 파일 및 제어 빌드 및 배포 프로세스를 조작 하는 방법을 보여 주기는 명령 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-127">This contains various custom project files and command files that demonstrate how you can control and manipulate the build and deployment process.</span></span> <span data-ttu-id="62e08-128">이 자습서의 뒷부분에서 좀 더 자세히 다룰는 이러한 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-128">These are covered in more detail later in this tutorial.</span></span>

<span data-ttu-id="62e08-129">개념 수준에서 솔루션의 구성 요소에 부합 함께 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-129">At a conceptual level, the components of the solution fit together like this:</span></span>

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="62e08-130">ASP.NET MVC 3 웹 응용 프로그램에서 ASP.NET 멤버 자격 공급자를 사용 하는 동안 웹 응용 프로그램 내의 모든 페이지는 익명 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-130">While the ASP.NET MVC 3 web application uses the ASP.NET membership provider, all the pages within the web application allow anonymous access.</span></span> <span data-ttu-id="62e08-131">이 명확 하 게 현실적인 구성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-131">This is clearly not a realistic configuration.</span></span> <span data-ttu-id="62e08-132">그러나 솔루션을 쉽게 배포 하 고 사용자 계정 및 역할을 구성 하지 않고 솔루션을 테스트에 대 한이 방식으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-132">However, the solution is set up in this way to make it easier for you to deploy and test the solution without configuring user accounts and roles.</span></span>


## <a name="deployment-challenges"></a><span data-ttu-id="62e08-133">배포 문제</span><span class="sxs-lookup"><span data-stu-id="62e08-133">Deployment Challenges</span></span>

<span data-ttu-id="62e08-134">Contact Manager 솔루션에서는 다양 한 엔터프라이즈 배포 시나리오에 공통 된 몇 가지 배포 문제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-134">The Contact Manager solution illustrates several deployment challenges that are common to lots of enterprise deployment scenarios:</span></span>

- <span data-ttu-id="62e08-135">여러 개의 종속 프로젝트가 솔루션 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-135">The solution consists of multiple dependent projects.</span></span> <span data-ttu-id="62e08-136">이러한 프로젝트를 동시에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-136">You need to deploy these projects simultaneously.</span></span>
- <span data-ttu-id="62e08-137">각 환경에 대해 업데이트 해야 할 연결 문자열 및 서비스 끝점 및 대부분의 경우에이 정보 됩니다 개발자에 게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-137">Connection strings and service endpoints need to be updated for each environment, and in a lot of cases this information will not be available to the developer.</span></span>
- <span data-ttu-id="62e08-138">배포 하는 경우는 **ContactManager** 데이터베이스 준비 및 프로덕션 환경에 맞게 후속 배포에 기존 데이터를 보존 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-138">When you deploy the **ContactManager** database to staging and production environments, you need to preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="62e08-139">ASP.NET 응용 프로그램 서비스 데이터베이스를 배포할 때 일부 구성 데이터를 배포 하지만 사용자 계정 데이터를 생략 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-139">When you deploy the ASP.NET application services database, you need to deploy some configuration data but omit any user account data.</span></span>
- <span data-ttu-id="62e08-140">프로젝트에는 일부 파일 및 폴더를 배포 해서는 안 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-140">The projects include some files and folders that should not be deployed.</span></span> <span data-ttu-id="62e08-141">배포 과정에서 이러한 파일 및 폴더를 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-141">You need to exclude these files and folders from the deployment process.</span></span>
- <span data-ttu-id="62e08-142">솔루션에서 Team Foundation Server (TFS) 빌드 서버에서 자동화 된 배포를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-142">The solution needs to support automated deployment from a Team Foundation Server (TFS) build server.</span></span>

## <a name="conclusion"></a><span data-ttu-id="62e08-143">결론</span><span class="sxs-lookup"><span data-stu-id="62e08-143">Conclusion</span></span>

<span data-ttu-id="62e08-144">이 항목 않아 솔루션의 상위 수준 개요를 제공 하 고 일부의 다양 한 엔터프라이즈 배포 시나리오에 공통 된 내재 된 배포 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-144">This topic provided a high-level overview of the Contact Manager solution and identified some of the inherent deployment challenges that are common to lots of enterprise deployment scenarios.</span></span> <span data-ttu-id="62e08-145">이 자습서의 나머지 항목에는 이러한 과제를 충족 하는 데 기술 중 일부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-145">The remaining topics in this tutorial describe some of the techniques you can use to meet these challenges.</span></span>

<span data-ttu-id="62e08-146">다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="62e08-146">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="62e08-147">[이전](web-deployment-in-the-enterprise.md)
> [다음](setting-up-the-contact-manager-solution.md)</span><span class="sxs-lookup"><span data-stu-id="62e08-147">[Previous](web-deployment-in-the-enterprise.md)
[Next](setting-up-the-contact-manager-solution.md)</span></span>
