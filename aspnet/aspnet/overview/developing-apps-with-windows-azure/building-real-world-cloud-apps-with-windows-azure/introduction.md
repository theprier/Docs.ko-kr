---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Azure 사용 하 여 실제 클라우드 앱 빌드 | Microsoft Docs
author: MikeWasson
description: 이 전자책에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 설명 합니다. 패턴은 적용에 개발 프로세스에는...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: c496e93d7517bc187514d5fa2dfa90d29c5f47f9
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48576315"
---
<a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="0a22d-104">Azure 사용 하 여 실제 클라우드 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="0a22d-104">Building Real-World Cloud Apps with Azure</span></span>
====================
<span data-ttu-id="0a22d-105">하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0a22d-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="0a22d-106">[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="0a22d-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="0a22d-107">이 전자책에서는 실제 클라우드 솔루션을 빌드하는 패턴 기반 접근 방식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="0a22d-108">패턴은 아키텍처 및 코딩 방식 뿐만 아니라 개발 프로세스에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="0a22d-109">콘텐츠는 고 제공한 프레젠테이션을 Scott Guthrie를 개발한 여 문의 사항이 있으면 노르웨이 개발자 회의 NDC ())의 2013 년 6 월을 기반으로 ([1 부](http://vimeo.com/68215538)를 [2 부](http://vimeo.com/68215602)), 및에서 Microsoft Tech Ed 오스트레일리아 2013 년 9 월 ([1 부](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)하십시오 [2 부](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span><span class="sxs-lookup"><span data-stu-id="0a22d-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="0a22d-110">[다른 많은](more-patterns-and-guidance.md#acknowledgments) 업데이트 하 고 양식으로 비디오에서 전환 하는 동안 콘텐츠를 쌓아 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>


## <a name="intended-audience"></a><span data-ttu-id="0a22d-111">대상</span><span class="sxs-lookup"><span data-stu-id="0a22d-111">Intended Audience</span></span>

<span data-ttu-id="0a22d-112">클라우드로 이동을 고려 중이거나, 클라우드 용 개발에 대해 궁금한 점이 있거나 클라우드 개발 모르는 개발자 여기 가장 중요 한 개념 및 알아야 하는 방법의 간단한 개요를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="0a22d-113">개념은 구체적인 예제 및 기타 리소스에 대 한 자세한 내용은 각 장의 링크와 함께 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="0a22d-114">예제 및 추가 리소스에 대 한 링크는 Microsoft 프레임 워크 및 서비스를 하지만 나와 있는 원칙 다른 웹 개발 프레임 워크에 적용 되며 클라우드 환경도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="0a22d-115">여기에서 아이디어 데 도움이 되는 게 더 성공적인 클라우드를 위해 이미 개발 중인 개발자 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="0a22d-116">계열의 각 장의 읽을 수 독립적으로 선택 하 고 관심이 있는 항목을 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="0a22d-117">Scott Guthrie의 감시 하는 사람 *실제 세계 클라우드 앱 빌드 Azure* 프레젠테이션 및 추가 및 업데이트 된 정보는 여기에서 찾을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="0a22d-118">클라우드 개발 패턴</span><span class="sxs-lookup"><span data-stu-id="0a22d-118">Cloud development patterns</span></span>

<span data-ttu-id="0a22d-119">이 전자책은 클라우드 개발에 대 한 패턴을 권장 13을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="0a22d-120">"Pattern" 의미로 사용 됩니다 여기는 넓은 의미에서 작업을 수행 하는 것이 좋습니다: 개발, 설계 및 클라우드 앱을 코딩 하는 방법에 대 한 이동 하는 최선의 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="0a22d-121">이들은 도움이 되는 "성공 pit에 해당"을 수행 하는 경우 키 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="0a22d-122">[모든 것을 자동화](automate-everything.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="0a22d-123">스크립트를 사용 하 여 효율성을 최대화 하 고 반복적인 프로세스에서 오류를 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="0a22d-124">Azure 관리 스크립트 데모:입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="0a22d-125">[소스 제어](source-control.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="0a22d-126">DevOps 워크플로 용이 하 게 하려면 소스 제어에서 분기 구조를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="0a22d-127">데모: 소스 제어에 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="0a22d-128">데모: 소스 제어에서 중요 한 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="0a22d-129">데모: Visual Studio에서 Git을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="0a22d-130">[지속적인 통합 및 업데이트](continuous-integration-and-continuous-delivery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="0a22d-131">빌드 및 각 원본 제어 체크 인을 사용 하 여 배포를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="0a22d-132">[웹 개발 모범 사례](web-development-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="0a22d-133">상태 비저장 웹 계층을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="0a22d-134">데모: 크기 조정 및 Azure App Service의 Web Apps에서 자동 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="0a22d-135">세션 상태를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-135">Avoid session state.</span></span>
    - <span data-ttu-id="0a22d-136">CDN을 사용할 수 없을 때 대체 사용 하 여 CDN을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="0a22d-137">비동기 프로그래밍 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="0a22d-138">데모: 비동기 ASP.NET MVC 및 Entity Framework에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="0a22d-139">[Single sign on](single-sign-on.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="0a22d-140">Azure Active Directory에 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="0a22d-141">데모: Azure Active Directory를 사용 하는 ASP.NET 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="0a22d-142">[데이터 저장소 옵션](data-storage-options.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="0a22d-143">데이터 저장소의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-143">Types of data stores.</span></span>
    - <span data-ttu-id="0a22d-144">적절 한 데이터 저장소를 선택 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="0a22d-145">데모: Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="0a22d-146">[데이터 분할 전략](data-partitioning-strategies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="0a22d-147">가로, 데이터를 분할 또는 관계형 데이터베이스 크기 조정을 용이 하 게 둘 다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="0a22d-148">[구조화 되지 않은 blob storage](unstructured-blob-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="0a22d-149">Blob service를 사용 하 여 클라우드에서 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="0a22d-150">데모: Fix It 응용 프로그램에서 blob storage를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="0a22d-151">[장애를 견딜 수 디자인](design-to-survive-failures.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="0a22d-152">형식 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-152">Types of failures.</span></span>
    - <span data-ttu-id="0a22d-153">오류 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-153">Failure Scope.</span></span>
    - <span data-ttu-id="0a22d-154">Sla를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-154">Understanding SLAs.</span></span>
- <span data-ttu-id="0a22d-155">[모니터링 및 원격 분석](monitoring-and-telemetry.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="0a22d-156">이유 모두 원격 분석 앱 구입 하며 앱 계측 하는 사용자 고유의 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="0a22d-157">Azure 용 New Relic 데모:</span><span class="sxs-lookup"><span data-stu-id="0a22d-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="0a22d-158">데모: Fix It 응용 프로그램에서 코드를 로깅.</span><span class="sxs-lookup"><span data-stu-id="0a22d-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="0a22d-159">데모: Fix It 응용 프로그램에서 종속성 주입 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="0a22d-160">데모: Azure에서 기본 제공 로깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="0a22d-161">[일시적인 오류 처리](transient-fault-handling.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="0a22d-162">일시적인 오류의 영향을 완화 하기 위해 스마트 재시도/백오프 논리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="0a22d-163">데모: 다시 시도/백오프 Entity Framework 6에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="0a22d-164">[분산 캐싱](distributed-caching.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="0a22d-165">확장성을 개선 하 고 분산 캐싱을 사용 하 여 데이터베이스 트랜잭션 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="0a22d-166">[큐 중심 작업 패턴](queue-centric-work-pattern.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="0a22d-167">고가용성을 사용 하도록 설정 하 고 느슨하게 웹 및 작업자 계층을 결합 하 여 확장성을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="0a22d-168">데모: Fix It 응용 프로그램에서 Azure storage 큐.</span><span class="sxs-lookup"><span data-stu-id="0a22d-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="0a22d-169">[더 많은 클라우드 앱 패턴 및 지침도](more-patterns-and-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="0a22d-170">부록: Fix It 응용 프로그램 예제</span><span class="sxs-lookup"><span data-stu-id="0a22d-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="0a22d-171">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="0a22d-171">Known Issues</span></span>
    - <span data-ttu-id="0a22d-172">모범 사례</span><span class="sxs-lookup"><span data-stu-id="0a22d-172">Best Practices</span></span>
    - <span data-ttu-id="0a22d-173">다운로드, 빌드, 실행 및 배포 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="0a22d-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="0a22d-174">이러한 패턴 모든 클라우드 환경에 적용 되지만 Microsoft 기술 및 Visual Studio, Team Foundation Service, ASP.NET 및 Azure 같은 서비스에 따라 예제를 사용 하 여 설명 하겠습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="0a22d-175">이 장의 나머지 부분이에서는이 Fix It 샘플 응용 프로그램 및 Fix It 응용 프로그램에서 실행 되는 Azure App Service 클라우드 환경에서 웹 앱을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="0a22d-176">샘플 응용 프로그램 수정</span><span class="sxs-lookup"><span data-stu-id="0a22d-176">The Fix it sample application</span></span>

<span data-ttu-id="0a22d-177">대부분의 스크린 샷 및이 전자책에 나와 있는 코드 예제에서 처음으로 개발한 Fix It 앱에 기반한 [Scott Guthrie](https://weblogs.asp.net/scottgu/) 권장 되는 클라우드 앱 개발 패턴 및 사례를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![앱 홈 페이지 해결](introduction/_static/image1.png)

<span data-ttu-id="0a22d-179">샘플 앱은 간단한 작업 항목 발권 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="0a22d-180">버그를 발견 해야 하는 경우 티켓을 할당 하 고 다른 사용자를 로그인 하 고 할당 된 티켓을 볼 수를 만들고 티켓을 작업이 완료 되 면 완료 됨으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="0a22d-181">표준 Visual Studio 웹 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="0a22d-182">ASP.NET MVC를 기반으로 하는 하 고 SQL Server 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="0a22d-183">IIS Express에서 로컬로 실행할 수 있습니다 하 고 클라우드에서 실행 하도록 Azure 웹 사이트에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="0a22d-184">폼 인증 및 로컬 데이터베이스를 사용 하 여 이나 Google 같은 소셜 공급자를 사용 하 여 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="0a22d-185">(나중에 살펴보겠습니다 Active Directory 조직 계정으로 로그인 하는 방법.)</span><span class="sxs-lookup"><span data-stu-id="0a22d-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![로그인 페이지](introduction/_static/image2.png)

<span data-ttu-id="0a22d-187">로그인 되 면에서 티켓을 작성, 사용자에 게, 할당 및 업로드할 수 수정 하려는 항목의 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![Fix It 작업 만들기](introduction/_static/image3.png)

![작업에서 만든 수정](introduction/_static/image4.png)

<span data-ttu-id="0a22d-190">완료 된 것으로, 티켓 세부 정보 보기 및 표시 항목에 할당 된 티켓을 참조 하십시오 만든 작업 항목의 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="0a22d-191">기능 측면에서 매우 간단한 앱 이지만 수백만 명의 사용자로 확장할 수 있습니다 하 고 데이터베이스 오류 및 연결 종료 등을 탄력적으로 대처할 수 있도록 구축 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="0a22d-192">간단 하 게 시작 하 고 앱을 더 빠르고 효율적으로 개발 주기를 반복 하 여 하는 자동화 되 고 민첩 한 개발 워크플로를 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="0a22d-193">Azure App Service에서 웹 앱</span><span class="sxs-lookup"><span data-stu-id="0a22d-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="0a22d-194">Fix It 응용 프로그램에 사용 되는 클라우드 환경에는 웹 사이트 라고 하는 Azure의 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="0a22d-195">이 서비스는 방식으로 Vm을 만들고 업데이트할를 유지 하지 않고도 Azure에서 고유한 웹 앱을 호스트, 설치 구성 하는 IIS, 등. Vm에서 사이트를 호스트 하 고 자동으로 백업 및 복구와 다른 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="0a22d-196">웹 사이트 서비스는 ASP.NET, Node.js, PHP 및 Python을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="0a22d-197">Visual Studio, 웹 배포, FTP, Git 또는 TFS를 사용 하 여 매우 신속 하 게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="0a22d-198">이 일반적으로 몇 초 안에 배포를 시작 하는 시간 사이 업데이트는 인터넷을 통해 사용할 수 있는 시간.</span><span class="sxs-lookup"><span data-stu-id="0a22d-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="0a22d-199">시작 하려면 모든 무료 이며 트래픽 증가 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="0a22d-200">내부적으로 Azure App Service에서 Web Apps는 많은 아키텍처 구성 요소 및 사용자 고유의 Vm에서 IIS를 사용 하 여 웹 사이트를 호스트 하려는 경우 직접 작성 해야 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="0a22d-201">하나의 구성 요소 배포 끝점을 자동으로 IIS를 구성 하 고 사이트에서 실행 하려는 만큼 Vm에서 응용 프로그램을 설치 하는 경우</span><span class="sxs-lookup"><span data-stu-id="0a22d-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![배포 서비스](introduction/_static/image5.png)

<span data-ttu-id="0a22d-203">IIS Vm에 직접 도달 하지 않게는 사용자 웹 사이트에 도달 하면, 겪는 [응용 프로그램 요청 라우팅 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) 부하 분산 장치.</span><span class="sxs-lookup"><span data-stu-id="0a22d-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="0a22d-204">사용자 고유의 서버를 사용 하 여 사용할 수 있습니다 이지만 장점은 해당 하는 수에 대 한 자동으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="0a22d-205">세션 선호도, IIS에서 큐 깊이 같은 요인을 고려 하는 스마트 추론을 사용 하 고 CPU 사용량 각 컴퓨터를 Vm에 트래픽을 호스트 하는 웹 사이트.</span><span class="sxs-lookup"><span data-stu-id="0a22d-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR 부하 분산 장치](introduction/_static/image6.png)

<span data-ttu-id="0a22d-207">컴퓨터 다운 되 면 Azure 자동으로 순환에서 가져오는, 새 VM 인스턴스를 스핀업 및 새 인스턴스에-응용 프로그램에 대 한 중단 시간 없이 모든 트래픽을 전달 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![시스템 오류 로부터 자동 복구](introduction/_static/image7.png)

<span data-ttu-id="0a22d-209">이 모두 자동으로 수행이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-209">All of this takes place automatically.</span></span> <span data-ttu-id="0a22d-210">웹 사이트를 만들고 응용 프로그램을 배포 후 Windows PowerShell, Visual Studio 또는 Azure 관리 포털을 사용 하 여 수행 해야 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="0a22d-211">쉽고 빠르게 단계별 자습서는 Visual Studio에서 웹 응용 프로그램을 만들고 Azure 웹 사이트를 배포 하는 방법을 보여주는 참조 하세요 [Azure 및 ASP.NET 시작](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="0a22d-212">요약</span><span class="sxs-lookup"><span data-stu-id="0a22d-212">Summary</span></span>

<span data-ttu-id="0a22d-213">이 소개 항목 책 설명, 샘플 응용 프로그램의 스크린샷 및 Azure App Service 클라우드 환경에서 웹 앱에 간략하게 설명의 목록을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="0a22d-214">클라우드 용으로 앱을 개발 하는 가장 큰 장점 중 하나는 테스트 환경 만들기 및 코드 배포와 같은 반복적인 개발 작업을 자동화 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="0a22d-215">주체는 수행 하는 방법을 합니다 [다음 장에서](automate-everything.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="0a22d-216">자료</span><span class="sxs-lookup"><span data-stu-id="0a22d-216">Resources</span></span>

<span data-ttu-id="0a22d-217">이 장에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0a22d-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="0a22d-218">설명서:</span><span class="sxs-lookup"><span data-stu-id="0a22d-218">Documentation:</span></span>

- <span data-ttu-id="0a22d-219">[Azure App Service의 웹 앱](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="0a22d-220">Web Apps에 대 한 Azure 설명서에 대 한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="0a22d-221">Web Apps, Cloud Services 및 Vm: 사용 하는 경우?</span><span class="sxs-lookup"><span data-stu-id="0a22d-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="0a22d-222">WAWS이 챕터에 표시 된 것 처럼 Azure에서 웹 앱을 실행할 수 있습니다 하는 세 가지 방법 중 하나일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="0a22d-223">이 문서는 세 가지 방법 간의 차이점을 설명 하 고 시나리오에 적합 한 선택 하는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="0a22d-224">웹 사이트와 같은 클라우드 서비스는 Azure의 PaaS 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="0a22d-225">Vm은 IaaS 기능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="0a22d-226">IaaS와 PaaS의 설명에 대 한 참조를 [데이터 옵션](data-storage-options.md#paasiaas) 장입니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="0a22d-227">비디오:</span><span class="sxs-lookup"><span data-stu-id="0a22d-227">Videos:</span></span>

- [<span data-ttu-id="0a22d-228">Scott Guthrie 시작 단계 0-Azure 클라우드 OS 란?</span><span class="sxs-lookup"><span data-stu-id="0a22d-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="0a22d-229">[Stefan Schackow를 사용 하 여 웹 사이트 아키텍처-](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="0a22d-230">[Nir Mashkowski를 사용 하 여 azure 웹 사이트 내부](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a22d-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0a22d-231">다음</span><span class="sxs-lookup"><span data-stu-id="0a22d-231">Next</span></span>](automate-everything.md)
