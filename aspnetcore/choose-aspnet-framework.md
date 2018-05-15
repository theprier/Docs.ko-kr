---
title: ASP.NET 및 ASP.NET Core 중에서 선택
author: rick-anderson
description: ASP.NET 및 ASP.NET Core 중에서 선택하는 방법을 알아보세요.
manager: wpickett
ms.author: riande
ms.date: 03/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/choose-between-aspnet-and-aspnetcore
ms.openlocfilehash: e6ac9f54ef623895b81eea33d90791e5f0ad5120
ms.sourcegitcommit: 71b93b42cbce8a9b1a12c4d88391e75a4dfb6162
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2018
---
# <a name="choose-between-aspnet-and-aspnet-core"></a><span data-ttu-id="72d7c-103">ASP.NET 및 ASP.NET Core 중에서 선택</span><span class="sxs-lookup"><span data-stu-id="72d7c-103">Choose between ASP.NET and ASP.NET Core</span></span>

<span data-ttu-id="72d7c-104">만들려는 웹앱과 관계없이 ASP.NET에는 Windows Server를 대상으로 하는 엔터프라이즈 웹앱에서 Linux 컨테이너를 대상으로 하는 작은 마이크로 서비스 및 그 사이의 모든 항목에 대한 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72d7c-104">No matter the web app you're creating, ASP.NET has a solution for you: from enterprise web apps targeting Windows Server, to small microservices targeting Linux containers, and everything in between.</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="72d7c-105">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="72d7c-105">ASP.NET Core</span></span>

<span data-ttu-id="72d7c-106">ASP.NET Core는 Windows, macOS 또는 Linux에서 클라우드 기반 최신 웹앱을 빌드하기 위한 오픈 소스 플랫폼 간 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="72d7c-106">ASP.NET Core is an open-source, cross-platform framework for building modern, cloud-based web apps on Windows, macOS, or Linux.</span></span>

## <a name="aspnet"></a><span data-ttu-id="72d7c-107">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="72d7c-107">ASP.NET</span></span>

<span data-ttu-id="72d7c-108">ASP.NET은 Windows에서 엔터프라이즈 수준의 서버 기반 웹앱을 만들 때 필요한 모든 서비스를 제공하는 완성도 있는 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="72d7c-108">ASP.NET is a mature framework that provides all the services needed to build enterprise-class, server-based web apps on Windows.</span></span>

## <a name="which-one-is-right-for-me"></a><span data-ttu-id="72d7c-109">어떤 기능이 내게 적합한가요?</span><span class="sxs-lookup"><span data-stu-id="72d7c-109">Which one is right for me?</span></span>

| <span data-ttu-id="72d7c-110">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="72d7c-110">ASP.NET Core</span></span> | <span data-ttu-id="72d7c-111">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="72d7c-111">ASP.NET</span></span> |
|---|---|
|<span data-ttu-id="72d7c-112">Windows, macOS 또는 Linux용 빌드</span><span class="sxs-lookup"><span data-stu-id="72d7c-112">Build for Windows, macOS, or Linux</span></span>|<span data-ttu-id="72d7c-113">Windows용 빌드</span><span class="sxs-lookup"><span data-stu-id="72d7c-113">Build for Windows</span></span>|
|<span data-ttu-id="72d7c-114">[Razor 페이지](xref:mvc/razor-pages/index)는 ASP.NET Core 2.x에서 웹 UI를 만드는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="72d7c-114">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span> <span data-ttu-id="72d7c-115">[MVC](xref:mvc/overview), [Web API](xref:tutorials/first-web-api) 및 [SignalR](xref:signalr/introduction)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="72d7c-115">See also [MVC](xref:mvc/overview), [Web API](xref:tutorials/first-web-api), and [SignalR](xref:signalr/introduction).</span></span>|<span data-ttu-id="72d7c-116">[Web Forms](/aspnet/web-forms), [SignalR](/aspnet/signalr), [MVC](/aspnet/mvc), [Web API](/aspnet/web-api/) 또는 [웹 페이지](/aspnet/web-pages)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="72d7c-116">Use [Web Forms](/aspnet/web-forms), [SignalR](/aspnet/signalr), [MVC](/aspnet/mvc), [Web API](/aspnet/web-api/), or [Web Pages](/aspnet/web-pages)</span></span>|
|<span data-ttu-id="72d7c-117">컴퓨터당 여러 버전</span><span class="sxs-lookup"><span data-stu-id="72d7c-117">Multiple versions per machine</span></span>|<span data-ttu-id="72d7c-118">컴퓨터당 하나의 버전</span><span class="sxs-lookup"><span data-stu-id="72d7c-118">One version per machine</span></span>|
|<span data-ttu-id="72d7c-119">C# 또는 F#을 사용하여 Visual Studio, [Mac용 Visual Studio](https://www.visualstudio.com/vs/visual-studio-mac/) 또는 [Visual Studio Code](https://code.visualstudio.com/)에서 개발</span><span class="sxs-lookup"><span data-stu-id="72d7c-119">Develop with Visual Studio, [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/), or [Visual Studio Code](https://code.visualstudio.com/) using C# or F#</span></span>|<span data-ttu-id="72d7c-120">C#, VB 또는 F#을 사용하여 Visual Studio에서 개발</span><span class="sxs-lookup"><span data-stu-id="72d7c-120">Develop with Visual Studio using C#, VB, or F#</span></span>|
|<span data-ttu-id="72d7c-121">ASP.NET보다 고성능</span><span class="sxs-lookup"><span data-stu-id="72d7c-121">Higher performance than ASP.NET</span></span>|<span data-ttu-id="72d7c-122">성능 양호</span><span class="sxs-lookup"><span data-stu-id="72d7c-122">Good performance</span></span>|
|[<span data-ttu-id="72d7c-123">.NET Framework 또는 .NET Core 런타임 선택</span><span class="sxs-lookup"><span data-stu-id="72d7c-123">Choose .NET Framework or .NET Core runtime</span></span>](/dotnet/articles/standard/choosing-core-framework-server)|<span data-ttu-id="72d7c-124">.NET Framework 런타임 사용</span><span class="sxs-lookup"><span data-stu-id="72d7c-124">Use .NET Framework runtime</span></span>|

## <a name="aspnet-core-scenarios"></a><span data-ttu-id="72d7c-125">ASP.NET Core 시나리오</span><span class="sxs-lookup"><span data-stu-id="72d7c-125">ASP.NET Core scenarios</span></span>

<!-- update link to Razor Pages mvc movie series when done -->
* <span data-ttu-id="72d7c-126">[Razor 페이지](xref:mvc/razor-pages/index)는 ASP.NET Core 2.x에서 웹 UI를 만드는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="72d7c-126">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span>
* [<span data-ttu-id="72d7c-127">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="72d7c-127">Websites</span></span>](xref:tutorials/first-mvc-app/index)
* [<span data-ttu-id="72d7c-128">API</span><span class="sxs-lookup"><span data-stu-id="72d7c-128">APIs</span></span>](xref:tutorials/first-web-api)
* [<span data-ttu-id="72d7c-129">실시간</span><span class="sxs-lookup"><span data-stu-id="72d7c-129">Real-time</span></span>](xref:signalr/index)

## <a name="aspnet-scenarios"></a><span data-ttu-id="72d7c-130">ASP.NET 시나리오</span><span class="sxs-lookup"><span data-stu-id="72d7c-130">ASP.NET scenarios</span></span>

* [<span data-ttu-id="72d7c-131">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="72d7c-131">Websites</span></span>](/aspnet/mvc)
* [<span data-ttu-id="72d7c-132">API</span><span class="sxs-lookup"><span data-stu-id="72d7c-132">APIs</span></span>](/aspnet/web-api)
* [<span data-ttu-id="72d7c-133">실시간</span><span class="sxs-lookup"><span data-stu-id="72d7c-133">Real-time</span></span>](/aspnet/signalr)

## <a name="resources"></a><span data-ttu-id="72d7c-134">자료</span><span class="sxs-lookup"><span data-stu-id="72d7c-134">Resources</span></span>

* [<span data-ttu-id="72d7c-135">ASP.NET 소개</span><span class="sxs-lookup"><span data-stu-id="72d7c-135">Introduction to ASP.NET</span></span>](/aspnet/overview)
* [<span data-ttu-id="72d7c-136">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="72d7c-136">Introduction to ASP.NET Core</span></span>](xref:index)
