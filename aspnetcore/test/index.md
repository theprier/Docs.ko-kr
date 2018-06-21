---
title: ASP.NET Core에서 테스트, 디버깅 및 문제 해결
author: guardrex
description: ASP.NET Core 응용 프로그램 테스트 및 디버깅을 위해 리소스에 연결합니다.
ms.author: riande
ms.custom: mvc
ms.date: 06/13/2018
uid: test/index
ms.openlocfilehash: c5925d55a1b7d50d44d6bea4013331416ce3cec8
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278803"
---
# <a name="test-debug-and-troubleshoot-in-aspnet-core"></a><span data-ttu-id="82c70-103">ASP.NET Core에서 테스트, 디버깅 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="82c70-103">Test, debug, and troubleshoot in ASP.NET Core</span></span>

## <a name="test"></a><span data-ttu-id="82c70-104">테스트</span><span class="sxs-lookup"><span data-stu-id="82c70-104">Test</span></span>

[<span data-ttu-id="82c70-105">.NET Core 및 .NET Standard의 유닛 테스트</span><span class="sxs-lookup"><span data-stu-id="82c70-105">Unit Testing in .NET Core and .NET Standard</span></span>](/dotnet/articles/core/testing/)  
<span data-ttu-id="82c70-106">.NET Core 및 .NET Standard 프로젝트에서 유닛 테스트를 사용하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82c70-106">See how to use unit testing in .NET Core and .NET Standard projects.</span></span>

[<span data-ttu-id="82c70-107">통합 테스트</span><span class="sxs-lookup"><span data-stu-id="82c70-107">Integration tests</span></span>](xref:test/integration-tests)  
<span data-ttu-id="82c70-108">통합 테스트를 사용하여 앱의 구성 요소가 데이터베이스, 파일 시스템 및 네트워크를 비롯한 인프라 수준에서 제대로 작동하는지 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="82c70-108">Learn how integration tests ensure that an app's components function correctly at the infrastructure level, including the database, file system, and network.</span></span>

[<span data-ttu-id="82c70-109">Razor 페이지 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="82c70-109">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)  
<span data-ttu-id="82c70-110">Razor 페이지 앱에 단위 테스트를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="82c70-110">Discover how to create unit tests for Razor Pages apps.</span></span>

[<span data-ttu-id="82c70-111">테스트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="82c70-111">Test controllers</span></span>](xref:mvc/controllers/testing)  
<span data-ttu-id="82c70-112">ASP.NET Core에서 Moq 및 xUnit로 컨트롤러 논리를 테스트하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="82c70-112">Learn how to test controller logic in ASP.NET Core with Moq and xUnit.</span></span>

## <a name="debug"></a><span data-ttu-id="82c70-113">디버그</span><span class="sxs-lookup"><span data-stu-id="82c70-113">Debug</span></span>

[<span data-ttu-id="82c70-114">ASP.NET Core 2.x 소스 디버그</span><span class="sxs-lookup"><span data-stu-id="82c70-114">Debug ASP.NET Core 2.x source</span></span>](https://github.com/aspnet/Docs/issues/4155)  
<span data-ttu-id="82c70-115">.NET Core 및 ASP.NET Core 원본을 디버깅하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="82c70-115">Learn how to debug .NET Core and ASP.NET Core sources.</span></span>

[<span data-ttu-id="82c70-116">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="82c70-116">Remote debugging</span></span>](/visualstudio/debugger/remote-debugging-azure)  
<span data-ttu-id="82c70-117">Visual Studio 2017 ASP.NET Core 앱을 설정하고 구성하고, Azure를 사용하여 IIS에 배포하고, Visual Studio에서 원격 디버거를 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="82c70-117">Discover how to set up and configure a Visual Studio 2017 ASP.NET Core app, deploy it to IIS using Azure, and attach the remote debugger from Visual Studio.</span></span>

[<span data-ttu-id="82c70-118">스냅숏 디버깅</span><span class="sxs-lookup"><span data-stu-id="82c70-118">Snapshot debugging</span></span>](/azure/application-insights/app-insights-snapshot-debugger)  
<span data-ttu-id="82c70-119">프로덕션에서 문제를 진단하는 데 필요한 정보를 얻기 위해 가장 많이 throw되는 예외에 대한 스냅숏을 수집하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="82c70-119">Learn how to collect snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="82c70-120">문제 해결</span><span class="sxs-lookup"><span data-stu-id="82c70-120">Troubleshoot</span></span>

[<span data-ttu-id="82c70-121">문제 해결</span><span class="sxs-lookup"><span data-stu-id="82c70-121">Troubleshoot</span></span>](xref:test/troubleshoot)  
<span data-ttu-id="82c70-122">ASP.NET Core 프로젝트를 사용하여 경고 및 오류를 이해하고 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="82c70-122">Understand and troubleshoot warnings and errors with ASP.NET Core projects.</span></span>
