---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 솔루션 | Microsoft Docs
author: jrjlee
description: 이 자습서 시리즈에서는 샘플 솔루션을 사용 하 여&#x2014;Contact Manager 솔루션&#x2014;현실적인 수준을 사용 하 여 엔터프라이즈급 응용 프로그램을 나타내는...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 8187766190da43ded52359892601f8129b9940ce
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388110"
---
<a name="the-contact-manager-solution"></a><span data-ttu-id="e3b01-103">Contact Manager 솔루션</span><span class="sxs-lookup"><span data-stu-id="e3b01-103">The Contact Manager Solution</span></span>
====================
<span data-ttu-id="e3b01-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="e3b01-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="e3b01-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="e3b01-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="e3b01-106">이 [시리즈의 자습서](web-deployment-in-the-enterprise.md) 샘플 솔루션을 사용 하 여&#x2014;Contact Manager 솔루션&#x2014;현실적인 수준의 복잡성을 사용 하 여 엔터프라이즈급 응용 프로그램을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-106">This [series of tutorials](web-deployment-in-the-enterprise.md) uses a sample solution&#x2014;the Contact Manager solution&#x2014;to represent an enterprise-scale application with a realistic level of complexity.</span></span> <span data-ttu-id="e3b01-107">이 항목에서는 Contact Manager 솔루션을 소개 하 고, 솔루션의 주요 구성 요소에 설명,이 종류의 엔터프라이즈 환경에서 다양 한 대상 플랫폼에 응용 프로그램 배포 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-107">This topic introduces the Contact Manager solution, describes the key components of the solution, and identifies the challenges in deploying this kind of application to various destination platforms in an enterprise environment.</span></span>
> 
> <span data-ttu-id="e3b01-108">이 자습서에서 항목을 통해 작업 하는 동안에 엔터프라이즈 배포 시나리오에서 특정 과제를 충족 하는 방법을 보여 주는 참조 구현으로 Contact Manager 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-108">As you work through the topics in these tutorials, you can use the Contact Manager solution as a reference implementation that demonstrates how you can meet specific challenges in enterprise deployment scenarios.</span></span> <span data-ttu-id="e3b01-109">다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-109">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>


## <a name="solution-overview"></a><span data-ttu-id="e3b01-110">솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="e3b01-110">Solution Overview</span></span>

<span data-ttu-id="e3b01-111">Contact Manager 솔루션 4 개의 개별 프로젝트가 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-111">The Contact Manager solution consists of four individual projects:</span></span>

![](the-contact-manager-solution/_static/image1.png)

- <span data-ttu-id="e3b01-112">**ContactManager.Mvc**.</span><span class="sxs-lookup"><span data-stu-id="e3b01-112">**ContactManager.Mvc**.</span></span> <span data-ttu-id="e3b01-113">솔루션에 대 한 진입점을 나타내는 ASP.NET MVC 3 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-113">This is an ASP.NET MVC 3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="e3b01-114">생성 및 연락처 세부 정보를 확인 하는 기능을 사용 하 여 사용자를 제공 하는 등 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-114">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="e3b01-115">응용 프로그램은 연락처 및 인증 및 권한 부여를 관리 하는 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하는 Windows Communication Foundation (WCF) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-115">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="e3b01-116">**ContactManager.Database**.</span><span class="sxs-lookup"><span data-stu-id="e3b01-116">**ContactManager.Database**.</span></span> <span data-ttu-id="e3b01-117">Visual Studio 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-117">This is a Visual Studio database project.</span></span> <span data-ttu-id="e3b01-118">프로젝트는 저장소 연락처 세부 정보는 데이터베이스에 대 한 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-118">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="e3b01-119">**ContactManager.Service**.</span><span class="sxs-lookup"><span data-stu-id="e3b01-119">**ContactManager.Service**.</span></span> <span data-ttu-id="e3b01-120">WCF 웹 서비스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-120">This is a WCF web service project.</span></span> <span data-ttu-id="e3b01-121">검색, 업데이트 및 삭제 (CRUD) 작업에서 수행 하는 호출자를 허용 하는 끝점을 만들려면 WCF 서비스 노출 합니다 **ContactManager** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-121">The WCF service exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the **ContactManager** database.</span></span> <span data-ttu-id="e3b01-122">서비스에 의존 합니다 **ContactManager** 데이터베이스 및 **ContactManager.Common.dll** 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-122">The service relies on the **ContactManager** database and the **ContactManager.Common.dll** assembly.</span></span>
- <span data-ttu-id="e3b01-123">**ContactManager.Common**.</span><span class="sxs-lookup"><span data-stu-id="e3b01-123">**ContactManager.Common**.</span></span> <span data-ttu-id="e3b01-124">클래스 라이브러리 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-124">This is a class library project.</span></span> <span data-ttu-id="e3b01-125">WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-125">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="e3b01-126">솔루션에는 게시를 폴더가 솔루션도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-126">The solution also includes a solution folder named Publish.</span></span> <span data-ttu-id="e3b01-127">다양 한 사용자 지정 프로젝트 파일 및 제어 하 고 빌드 및 배포 프로세스를 조작할 수는 방법을 보여 주는 명령 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-127">This contains various custom project files and command files that demonstrate how you can control and manipulate the build and deployment process.</span></span> <span data-ttu-id="e3b01-128">이러한이 자습서의 뒷부분에서 자세히 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-128">These are covered in more detail later in this tutorial.</span></span>

<span data-ttu-id="e3b01-129">개념 수준에서 솔루션의 구성 요소 처럼 잘 맞습니다이:</span><span class="sxs-lookup"><span data-stu-id="e3b01-129">At a conceptual level, the components of the solution fit together like this:</span></span>

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="e3b01-130">ASP.NET 멤버 자격 공급자를 사용 하는 ASP.NET MVC 3 웹 응용 프로그램을 웹 응용 프로그램 내의 모든 페이지는 익명 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-130">While the ASP.NET MVC 3 web application uses the ASP.NET membership provider, all the pages within the web application allow anonymous access.</span></span> <span data-ttu-id="e3b01-131">이 명확 하 게 실제 구성이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-131">This is clearly not a realistic configuration.</span></span> <span data-ttu-id="e3b01-132">그러나 솔루션을 쉽게 배포 및 사용자 계정 및 역할을 구성 하지 않고 솔루션을 테스트할 수 있도록이 방식으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-132">However, the solution is set up in this way to make it easier for you to deploy and test the solution without configuring user accounts and roles.</span></span>


## <a name="deployment-challenges"></a><span data-ttu-id="e3b01-133">배포 과제</span><span class="sxs-lookup"><span data-stu-id="e3b01-133">Deployment Challenges</span></span>

<span data-ttu-id="e3b01-134">Contact Manager 솔루션은 많은 엔터프라이즈 배포 시나리오에 공통 되는 여러 가지 배포 문제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-134">The Contact Manager solution illustrates several deployment challenges that are common to lots of enterprise deployment scenarios:</span></span>

- <span data-ttu-id="e3b01-135">여러 종속 프로젝트가 솔루션 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-135">The solution consists of multiple dependent projects.</span></span> <span data-ttu-id="e3b01-136">이러한 프로젝트를 동시에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-136">You need to deploy these projects simultaneously.</span></span>
- <span data-ttu-id="e3b01-137">연결 문자열 및 서비스 끝점을 각 환경에 대 한 업데이트 해야 하 고는 대부분의 경우가이 정보를 사용할 수 없습니다 개발자에 게 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-137">Connection strings and service endpoints need to be updated for each environment, and in a lot of cases this information will not be available to the developer.</span></span>
- <span data-ttu-id="e3b01-138">배포 하는 경우는 **ContactManager** 데이터베이스 스테이징 및 프로덕션 환경에 후속 배포에서 기존 데이터를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-138">When you deploy the **ContactManager** database to staging and production environments, you need to preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="e3b01-139">ASP.NET 응용 프로그램 서비스 데이터베이스를 배포할 때 일부 구성 데이터를 배포 하지만 모든 사용자 계정 데이터를 생략 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-139">When you deploy the ASP.NET application services database, you need to deploy some configuration data but omit any user account data.</span></span>
- <span data-ttu-id="e3b01-140">일부 파일 및 배포 해야 하는 폴더를 프로젝트에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-140">The projects include some files and folders that should not be deployed.</span></span> <span data-ttu-id="e3b01-141">배포 프로세스에서 이러한 파일 및 폴더를 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-141">You need to exclude these files and folders from the deployment process.</span></span>
- <span data-ttu-id="e3b01-142">솔루션은 Team Foundation Server (TFS) 빌드 서버에서 자동화 된 배포를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-142">The solution needs to support automated deployment from a Team Foundation Server (TFS) build server.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e3b01-143">결론</span><span class="sxs-lookup"><span data-stu-id="e3b01-143">Conclusion</span></span>

<span data-ttu-id="e3b01-144">이 항목에서는 Contact Manager 솔루션의 대략적인 개요를 제공 하 고 일부의 다양 한 엔터프라이즈 배포 시나리오에 공통 되는 고유한 배포 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-144">This topic provided a high-level overview of the Contact Manager solution and identified some of the inherent deployment challenges that are common to lots of enterprise deployment scenarios.</span></span> <span data-ttu-id="e3b01-145">이 자습서의 나머지 항목에서는 이러한 과제를 충족 하 여 기술 중 일부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-145">The remaining topics in this tutorial describe some of the techniques you can use to meet these challenges.</span></span>

<span data-ttu-id="e3b01-146">다음 항목인 [the Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)를 다운로드 하 고 개발자 워크스테이션에서 솔루션을 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3b01-146">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e3b01-147">[이전](web-deployment-in-the-enterprise.md)
> [다음](setting-up-the-contact-manager-solution.md)</span><span class="sxs-lookup"><span data-stu-id="e3b01-147">[Previous](web-deployment-in-the-enterprise.md)
[Next](setting-up-the-contact-manager-solution.md)</span></span>
