---
title: ASP.NET Core의 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 ASP.NET Core 웹 호스트 및 .NET 일반 호스트에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/host/index
ms.openlocfilehash: 7ad059e39866f59040c12b7ac15e9fa3405a9aad
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="host-in-aspnet-core"></a><span data-ttu-id="beb71-103">ASP.NET Core의 호스트</span><span class="sxs-lookup"><span data-stu-id="beb71-103">Host in ASP.NET Core</span></span>

<span data-ttu-id="beb71-104">.NET 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-104">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="beb71-105">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-105">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="beb71-106">두 개의 호스트 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-106">Two host APIs are available for use:</span></span>

* <span data-ttu-id="beb71-107">[웹 호스트](xref:fundamentals/host/web-host) &ndash; 웹 응용 프로그램을 호스팅하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-107">[Web Host](xref:fundamentals/host/web-host) &ndash; Suitable for hosting web apps.</span></span>
* <span data-ttu-id="beb71-108">[일반 호스트](xref:fundamentals/host/generic-host)(ASP.NET Core 2.1 이상) &ndash; 웹이 아닌 앱(예: 백그라운드 작업을 실행하는 앱)을 호스팅하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-108">[Generic Host](xref:fundamentals/host/generic-host) (ASP.NET Core 2.1 or later) &ndash; Suitable for hosting non-web apps (for example, apps that run background tasks).</span></span> <span data-ttu-id="beb71-109">이후 릴리스에서는 일반 호스트가 웹앱을 포함한 모든 종류의 앱을 호스팅하는 데 적합해질 것입니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-109">In a future release, the Generic Host will be suitable for hosting any kind of app, including web apps.</span></span> <span data-ttu-id="beb71-110">일반 호스트는 결국 웹 호스트를 대체하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-110">The Generic Host will eventually replace the Web Host.</span></span>

<span data-ttu-id="beb71-111">이 경우 개발자는 ASP.NET Core 앱을 호스팅할 때 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에 기반을 둔 [웹 호스트](xref:fundamentals/host/web-host)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="beb71-111">At this time, developers should use the [Web Host](xref:fundamentals/host/web-host) based on [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) for hosting ASP.NET Core apps.</span></span>
