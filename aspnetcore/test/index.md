---
title: ASP.NET Core에서 테스트, 디버깅 및 문제 해결
author: guardrex
description: ASP.NET Core 응용 프로그램 테스트 및 디버깅을 위해 리소스에 연결합니다.
ms.author: riande
ms.custom: mvc
ms.date: 07/03/2018
uid: test/index
ms.openlocfilehash: 20f6804c1db588a88abb0d5686f894b7463ff6a9
ms.sourcegitcommit: 18339e3cb5a891a3ca36d8146fa83cf91c32e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37433963"
---
# <a name="test-debug-and-troubleshoot-in-aspnet-core"></a><span data-ttu-id="163a8-103">ASP.NET Core에서 테스트, 디버깅 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="163a8-103">Test, debug, and troubleshoot in ASP.NET Core</span></span>

## <a name="test"></a><span data-ttu-id="163a8-104">테스트</span><span class="sxs-lookup"><span data-stu-id="163a8-104">Test</span></span>

[<span data-ttu-id="163a8-105">.NET Core 및 .NET Standard의 유닛 테스트</span><span class="sxs-lookup"><span data-stu-id="163a8-105">Unit Testing in .NET Core and .NET Standard</span></span>](/dotnet/articles/core/testing/)  
<span data-ttu-id="163a8-106">.NET Core 및 .NET Standard 프로젝트에서 유닛 테스트를 사용하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="163a8-106">See how to use unit testing in .NET Core and .NET Standard projects.</span></span>

[<span data-ttu-id="163a8-107">통합 테스트</span><span class="sxs-lookup"><span data-stu-id="163a8-107">Integration tests</span></span>](xref:test/integration-tests)  
<span data-ttu-id="163a8-108">통합 테스트를 사용하여 앱의 구성 요소가 데이터베이스, 파일 시스템 및 네트워크를 비롯한 인프라 수준에서 제대로 작동하는지 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-108">Learn how integration tests ensure that an app's components function correctly at the infrastructure level, including the database, file system, and network.</span></span>

[<span data-ttu-id="163a8-109">Razor 페이지 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="163a8-109">Razor Pages unit tests</span></span>](xref:test/razor-pages-tests)  
<span data-ttu-id="163a8-110">Razor 페이지 앱에 단위 테스트를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-110">Discover how to create unit tests for Razor Pages apps.</span></span>

[<span data-ttu-id="163a8-111">테스트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="163a8-111">Test controllers</span></span>](xref:mvc/controllers/testing)  
<span data-ttu-id="163a8-112">ASP.NET Core에서 Moq 및 xUnit로 컨트롤러 논리를 테스트하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-112">Learn how to test controller logic in ASP.NET Core with Moq and xUnit.</span></span>

## <a name="debug"></a><span data-ttu-id="163a8-113">디버그</span><span class="sxs-lookup"><span data-stu-id="163a8-113">Debug</span></span>

[<span data-ttu-id="163a8-114">Visual Studio를 사용하여 디버깅하는 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="163a8-114">Learn to debug using Visual Studio</span></span>](/visualstudio/debugger/getting-started-with-the-debugger)  
<span data-ttu-id="163a8-115">단계별 연습에서는 Visual Studio 디버거의 기능을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-115">Discover the features of the Visual Studio debugger in a step-by-step walkthrough.</span></span>

<span data-ttu-id="163a8-116">[Debugging with Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)(Visual Studio Code를 사용한 디버깅)</span><span class="sxs-lookup"><span data-stu-id="163a8-116">[Debugging with Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)</span></span>  
<span data-ttu-id="163a8-117">Visual Studio Code에 기본 제공되는 디버깅 지원에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-117">Find out about the debugging support built into Visual Studio Code.</span></span>

[<span data-ttu-id="163a8-118">ASP.NET Core 2.x 소스 디버그</span><span class="sxs-lookup"><span data-stu-id="163a8-118">Debug ASP.NET Core 2.x source</span></span>](https://github.com/aspnet/Docs/issues/4155)  
<span data-ttu-id="163a8-119">.NET Core 및 ASP.NET Core 원본을 디버깅하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-119">Learn how to debug .NET Core and ASP.NET Core sources.</span></span>

[<span data-ttu-id="163a8-120">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="163a8-120">Remote debugging</span></span>](/visualstudio/debugger/remote-debugging-azure)  
<span data-ttu-id="163a8-121">Visual Studio 2017 ASP.NET Core 앱을 설정 및 구성하고, Azure를 사용하여 IIS에 배포하고, Visual Studio에서 원격 디버거를 연결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-121">Explore how to set up and configure a Visual Studio 2017 ASP.NET Core app, deploy it to IIS using Azure, and attach the remote debugger from Visual Studio.</span></span>

[<span data-ttu-id="163a8-122">스냅숏 디버깅</span><span class="sxs-lookup"><span data-stu-id="163a8-122">Snapshot debugging</span></span>](/azure/application-insights/app-insights-snapshot-debugger)  
<span data-ttu-id="163a8-123">프로덕션에서 문제를 진단하는 데 필요한 정보를 얻기 위해 가장 많이 throw되는 예외에 대한 스냅숏을 수집하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-123">Find out how to collect snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="163a8-124">문제 해결</span><span class="sxs-lookup"><span data-stu-id="163a8-124">Troubleshoot</span></span>

[<span data-ttu-id="163a8-125">문제 해결</span><span class="sxs-lookup"><span data-stu-id="163a8-125">Troubleshoot</span></span>](xref:test/troubleshoot)  
<span data-ttu-id="163a8-126">ASP.NET Core 프로젝트를 사용하여 경고 및 오류를 이해하고 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="163a8-126">Understand and troubleshoot warnings and errors with ASP.NET Core projects.</span></span>
