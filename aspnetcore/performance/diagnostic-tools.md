---
title: 성능 진단 도구
author: mjrousos
description: ASP.NET Core 앱에서 성능 문제를 진단 하는 데 유용한 도구입니다.
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.date: 12/07/2018
uid: performance/diagnostic-tools
ms.openlocfilehash: 3093b7d646e4fa943334c7b1e70ddc007ab18780
ms.sourcegitcommit: 1ea1b4fc58055c62728143388562689f1ef96cb2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53329206"
---
# <a name="performance-diagnostic-tools"></a><span data-ttu-id="3ae0d-103">성능 진단 도구</span><span class="sxs-lookup"><span data-stu-id="3ae0d-103">Performance Diagnostic Tools</span></span>

<span data-ttu-id="3ae0d-104">[Mike Rousos](https://github.com/mjrousos)</span><span class="sxs-lookup"><span data-stu-id="3ae0d-104">By [Mike Rousos](https://github.com/mjrousos)</span></span>

<span data-ttu-id="3ae0d-105">이 문서에서는 ASP.NET Core의 성능 문제를 진단 하기 위한 도구를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-105">This article lists tools for diagnosing performance issues in ASP.NET Core.</span></span>

## <a name="visual-studio-diagnostic-tools"></a><span data-ttu-id="3ae0d-106">Visual Studio 진단 도구</span><span class="sxs-lookup"><span data-stu-id="3ae0d-106">Visual Studio Diagnostic Tools</span></span>

<span data-ttu-id="3ae0d-107">합니다 [프로 파일링 및 진단 도구](/visualstudio/profiling) 성능 문제 조사를 시작 하는 것이 좋습니다는 Visual Studio에 기본 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-107">The [profiling and diagnostic tools](/visualstudio/profiling) built into Visual Studio are a good place to start investigating performance issues.</span></span> <span data-ttu-id="3ae0d-108">이러한 도구는 강력 하 고 Visual Studio 개발 환경에서 사용 하면 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-108">These tools are powerful and convenient to use from the Visual Studio development environment.</span></span> <span data-ttu-id="3ae0d-109">ASP.NET Core 앱에서 CPU 사용량, 메모리 사용량 및 성능 이벤트의 분석을 허용 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-109">The tooling allows analysis of CPU usage, memory usage, and performance events in ASP.NET Core apps.</span></span>

<span data-ttu-id="3ae0d-110">자세한 내용은 [Visual Studio 설명서](/visualstudio/profiling/profiling-overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-110">More information is available in [Visual Studio documentation](/visualstudio/profiling/profiling-overview).</span></span>

## <a name="application-insights"></a><span data-ttu-id="3ae0d-111">응용 프로그램 정보</span><span class="sxs-lookup"><span data-stu-id="3ae0d-111">Application Insights</span></span>

<span data-ttu-id="3ae0d-112">[Application Insights](/azure/application-insights/app-insights-overview) 앱에 대 한 자세한 성능 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-112">[Application Insights](/azure/application-insights/app-insights-overview) provides in-depth performance data for your app.</span></span> <span data-ttu-id="3ae0d-113">Application Insights는 자동으로 응답 속도, 실패율, 종속성 응답 시간 등의 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-113">Application Insights automatically collects data on response rates, failure rates, dependency response times, and more.</span></span> <span data-ttu-id="3ae0d-114">Application Insights는 앱에 사용자 지정 이벤트 및 특정 메트릭 로깅을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-114">Application Insights supports logging custom events and metrics specific to your app.</span></span>

<span data-ttu-id="3ae0d-115">Application Insights는 다양 한 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-115">Application Insights can be used in a variety environments:</span></span>

* <span data-ttu-id="3ae0d-116">Azure에서 작동 하도록 최적화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-116">Optimized to work in Azure.</span></span>
* <span data-ttu-id="3ae0d-117">프로덕션, 개발 및 스테이징에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-117">Works in production, development, and staging.</span></span>
* <span data-ttu-id="3ae0d-118">로컬로 작동 [Visual Studio](/azure/application-insights/app-insights-visual-studio) 또는 다른 호스팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-118">Works locally from [Visual Studio](/azure/application-insights/app-insights-visual-studio) or in other hosting environments.</span></span>

<span data-ttu-id="3ae0d-119">자세한 내용은 [ASP.NET Core용 Application Insights](/azure/application-insights/app-insights-asp-net-core)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-119">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="perfview"></a><span data-ttu-id="3ae0d-120">PerfView</span><span class="sxs-lookup"><span data-stu-id="3ae0d-120">PerfView</span></span>

<span data-ttu-id="3ae0d-121">[PerfView](https://github.com/Microsoft/perfview) 은.NET 성능 문제를 진단 하는 데 특별히.NET 팀에서 만든 성능 분석 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-121">[PerfView](https://github.com/Microsoft/perfview) is a performance analysis tool created by the .NET team specifically for diagnosing .NET performance issues.</span></span> <span data-ttu-id="3ae0d-122">PerfView는 CPU 사용량, 메모리 GC 동작, 성능 및 이벤트 벽 시계 시간 분석을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-122">PerfView allows analysis of CPU usage, memory and GC behavior, performance events, and wall clock time.</span></span>

<span data-ttu-id="3ae0d-123">PerfView 및 시작 하는 방법에 대 한 자세히 알아볼 수 있습니다 [PerfView 비디오 자습서](http://channel9.msdn.com/Series/PerfView-Tutorial) 또는 도구에서 사용할 수 있는 사용자 가이드를 참조 하 여 또는 [github](https://github.com/Microsoft/perfview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-123">You can learn more about PerfView and how to get started with [PerfView video tutorials](http://channel9.msdn.com/Series/PerfView-Tutorial) or by reading the user's guide available in the tool or [on GitHub](https://github.com/Microsoft/perfview).</span></span>

## <a name="perfcollect"></a><span data-ttu-id="3ae0d-124">PerfCollect</span><span class="sxs-lookup"><span data-stu-id="3ae0d-124">PerfCollect</span></span>

<span data-ttu-id="3ae0d-125">PerfView.NET 시나리오에 대 한 유용한 성능 분석 도구 이지만만 실행 됩니다 Windows 하므로 Linux 환경에서 실행 되는 ASP.NET Core 앱에서 추적을 수집에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-125">While PerfView is a useful performance analysis tool for .NET scenarios, it only runs on Windows so you can't use it to collect traces from ASP.NET Core apps running in Linux environments.</span></span>

<span data-ttu-id="3ae0d-126">[PerfCollect](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md) 네이티브 Linux 프로 파일링 도구를 사용 하는 bash 스크립트는 ([Perf](https://perf.wiki.kernel.org/index.php/Main_Page) 하 고 [LTTng](https://lttng.org/)) PerfView에서 분석할 수 있는 Linux에서 추적을 수집 하려면.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-126">[PerfCollect](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md) is a bash script that uses native Linux profiling tools ([Perf](https://perf.wiki.kernel.org/index.php/Main_Page) and [LTTng](https://lttng.org/)) to collect traces on Linux that can be analyzed by PerfView.</span></span> <span data-ttu-id="3ae0d-127">PerfCollect은 PerfView를 직접 사용할 수 없는 위치는 Linux 환경에서 성능 문제가 표시 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-127">PerfCollect is useful when performance problems show up in Linux environments where PerfView can't be used directly.</span></span> <span data-ttu-id="3ae0d-128">대신 PerfCollect PerfView를 사용 하 여 Windows 컴퓨터에서 다음 분석 되는.NET Core 앱에서 추적을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-128">Instead, PerfCollect can collect traces from .NET Core apps that are then analyzed on a Windows computer using PerfView.</span></span>

<span data-ttu-id="3ae0d-129">설치 하 고 PerfCollect 시작 하는 방법에 대 한 자세한 내용은 [GitHub에서](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae0d-129">More information about how to install and get started with PerfCollect is available [on GitHub](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/linux-performance-tracing.md).</span></span>
