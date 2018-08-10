---
title: ASP.NET Core 및 Azure에서 DevOps
author: CamSoper
description: Azure에서 호스팅되는 ASP.NET Core 앱에 대한 DevOps 파이프라인을 빌드하는 방법에 대한 종단 간 지침을 제공하는 가이드입니다.
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/index
ms.openlocfilehash: 09ca835e908e81c6f38f9430fb40638ba6dc3350
ms.sourcegitcommit: 29dfe436f54a27fbb4f6494bc639d16c75001fab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2018
ms.locfileid: "39722540"
---
# <a name="devops-with-aspnet-core-and-azure"></a><span data-ttu-id="93e89-103">ASP.NET Core 및 Azure에서 DevOps</span><span class="sxs-lookup"><span data-stu-id="93e89-103">DevOps with ASP.NET Core and Azure</span></span>

<span data-ttu-id="93e89-104">.NET용 Azure 개발 수명 주기 가이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-104">Welcome to the Azure Development Lifecycle guide for .NET!</span></span> <span data-ttu-id="93e89-105">이 가이드에서는 .NET 도구 및 프로세스를 사용하여 Azure 관련 개발 수명 주기를 빌드하는 기본 개념을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-105">This guide introduces the basic concepts of building a development lifecycle around Azure using .NET tools and processes.</span></span> <span data-ttu-id="93e89-106">이 가이드를 완료하면 성숙한 DevOps 도구 체인의 혜택을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-106">After finishing this guide, you'll reap the benefits of a mature DevOps toolchain.</span></span>

## <a name="who-this-guide-is-for"></a><span data-ttu-id="93e89-107">이 가이드의 대상</span><span class="sxs-lookup"><span data-stu-id="93e89-107">Who this guide is for</span></span>

<span data-ttu-id="93e89-108">ASP.NET에 익숙한 개발자여야 합니다(200~300 수준).</span><span class="sxs-lookup"><span data-stu-id="93e89-108">You should be an experienced ASP.NET developer (200-300 level).</span></span> <span data-ttu-id="93e89-109">이 소개에서 설명할 것처럼 Azure에 대한 지식이 없어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-109">You don't need to know anything about Azure, as we'll cover that in this introduction.</span></span> <span data-ttu-id="93e89-110">이 가이드는 개발보다 작업에 더 집중하는 DevOps 엔지니어의 경우에 유용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-110">This guide may also be useful for DevOps engineers who are more focused on operations than development.</span></span>

<span data-ttu-id="93e89-111">이 가이드는 Windows 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-111">This guide targets Windows developers.</span></span> <span data-ttu-id="93e89-112">그러나 Linux 및 macOS는 .NET Core에서 완전히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-112">However, Linux and macOS are fully supported by .NET Core.</span></span> <span data-ttu-id="93e89-113">Linux/macOS에 이 가이드를 적용하려면 Linux/macOS 차이점에 대한 설명선에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="93e89-113">To adapt this guide for Linux/macOS, watch for callouts for Linux/macOS differences.</span></span>

## <a name="what-this-guide-doesnt-cover"></a><span data-ttu-id="93e89-114">이 가이드에서 다루지 않는 내용</span><span class="sxs-lookup"><span data-stu-id="93e89-114">What this guide doesn't cover</span></span>

<span data-ttu-id="93e89-115">이 가이드는 .NET 개발자를 위한 종단 간 연속 배포 환경에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-115">This guide is focused on an end-to-end continuous deployment experience for .NET developers.</span></span> <span data-ttu-id="93e89-116">Azure의 모든 항목에 대한 완전한 가이드가 아니며 Azure 서비스에 대한 .NET API에만 광범위하게 집중하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-116">It's not an exhaustive guide to all things Azure, and it doesn't focus extensively on .NET APIs for Azure services.</span></span> <span data-ttu-id="93e89-117">지속적인 통합, 배포, 모니터링 및 디버깅과 관련된 모든 항목을 강조합니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-117">The emphasis is all around continuous integration, deployment, monitoring, and debugging.</span></span> <span data-ttu-id="93e89-118">이 가이드의 끝에서 다음 단계에 대한 권장 사항이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-118">Near the end of the guide, recommendations for next steps are offered.</span></span> <span data-ttu-id="93e89-119">ASP.NET 개발자에게 유용한 Azure 플랫폼 서비스가 제안에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-119">Included in the suggestions are Azure platform services that are useful to ASP.NET developers.</span></span>

## <a name="whats-in-this-guide"></a><span data-ttu-id="93e89-120">설명서의 내용</span><span class="sxs-lookup"><span data-stu-id="93e89-120">What's in this guide</span></span>

### <a name="tools-and-downloadsxrefazuredevopstools-and-downloads"></a>[<span data-ttu-id="93e89-121">도구 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="93e89-121">Tools and downloads</span></span>](xref:azure/devops/tools-and-downloads)

<span data-ttu-id="93e89-122">이 가이드에 사용되는 도구를 얻을 수 있는 위치에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-122">Learn where to acquire the tools used in this guide.</span></span>

### <a name="deploy-to-app-servicexrefazuredevopsdeploy-to-app-service"></a>[<span data-ttu-id="93e89-123">App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="93e89-123">Deploy to App Service</span></span>](xref:azure/devops/deploy-to-app-service)

<span data-ttu-id="93e89-124">Azure App Service에 ASP.NET Core 앱을 배포하는 다양한 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-124">Learn the various methods for deploying an ASP.NET Core app to Azure App Service.</span></span>

### <a name="continuous-integration-and-deploymentxrefazuredevopscicd"></a>[<span data-ttu-id="93e89-125">연속 통합 및 배포</span><span class="sxs-lookup"><span data-stu-id="93e89-125">Continuous integration and deployment</span></span>](xref:azure/devops/cicd)

<span data-ttu-id="93e89-126">GitHub, VSTS 및 Azure를 사용하여 종단 간 연속 통합 및 ASP.NET Core 앱에 대한 배포 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-126">Build an end-to-end continuous integration and deployment solution for your ASP.NET Core app with GitHub, VSTS, and Azure.</span></span>

### <a name="monitor-and-debugxrefazuredevopsmonitor"></a>[<span data-ttu-id="93e89-127">모니터링 및 디버그</span><span class="sxs-lookup"><span data-stu-id="93e89-127">Monitor and debug</span></span>](xref:azure/devops/monitor)

<span data-ttu-id="93e89-128">Azure 도구를 사용하여 응용 프로그램을 모니터링하고, 문제를 해결하고, 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-128">Use Azure's tools to monitor, troubleshoot, and tune your application.</span></span>

### <a name="next-stepsxrefazuredevopsnext-steps"></a>[<span data-ttu-id="93e89-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93e89-129">Next steps</span></span>](xref:azure/devops/next-steps)

<span data-ttu-id="93e89-130">Azure를 학습하는 ASP.NET Core 개발자를 위한 다른 학습 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-130">Other learning paths for the ASP.NET Core developer learning Azure.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="93e89-131">감사의 글</span><span class="sxs-lookup"><span data-stu-id="93e89-131">Acknowledgments</span></span>

<span data-ttu-id="93e89-132">유용한 제안을 통해 이 가이드에 참여해 주신 .NET 커뮤니티의 모든 사용자에게 감사합니다!</span><span class="sxs-lookup"><span data-stu-id="93e89-132">Thank you to everyone in the .NET community who contributed to this guide with helpful suggestions!</span></span> <span data-ttu-id="93e89-133">특히 이 자료의 최종 검토에 참여해 주신 다음과 같은 커뮤니티 멤버에게 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-133">We'd like to specifically thank the following community members who contributed to the final review of this material:</span></span>

* [<span data-ttu-id="93e89-134">Sam Wronski</span><span class="sxs-lookup"><span data-stu-id="93e89-134">Sam Wronski</span></span>](https://www.youtube.com/c/worldofzerodevelopment)
* [<span data-ttu-id="93e89-135">Jeffrey Palermo</span><span class="sxs-lookup"><span data-stu-id="93e89-135">Jeffrey Palermo</span></span>](https://twitter.com/jeffreypalermo)

## <a name="conclusion"></a><span data-ttu-id="93e89-136">결론</span><span class="sxs-lookup"><span data-stu-id="93e89-136">Conclusion</span></span>

<span data-ttu-id="93e89-137">이 가이드를 통해 ASP.NET Core 및 Azure App Service 관련되어 구축된 연속 통합 개발 수명 주기를 빌드하도록 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e89-137">This guide prepares you to build a continuous integration development lifecycle built around ASP.NET Core and Azure App Service.</span></span>

## <a name="additional-reading"></a><span data-ttu-id="93e89-138">추가 참조 항목</span><span class="sxs-lookup"><span data-stu-id="93e89-138">Additional reading</span></span>

* [<span data-ttu-id="93e89-139">클라우드 컴퓨팅이란?</span><span class="sxs-lookup"><span data-stu-id="93e89-139">What is Cloud Computing?</span></span>](https://azure.microsoft.com/overview/what-is-cloud-computing/)
* [<span data-ttu-id="93e89-140">클라우드 컴퓨팅의 예제</span><span class="sxs-lookup"><span data-stu-id="93e89-140">Examples of Cloud Computing</span></span>](https://azure.microsoft.com/overview/examples-of-cloud-computing/)
* [<span data-ttu-id="93e89-141">IaaS란?</span><span class="sxs-lookup"><span data-stu-id="93e89-141">What is IaaS?</span></span>](https://azure.microsoft.com/overview/what-is-iaas/)
* [<span data-ttu-id="93e89-142">란?</span><span class="sxs-lookup"><span data-stu-id="93e89-142">What is PaaS?</span></span>](https://azure.microsoft.com/overview/what-is-paas/)
