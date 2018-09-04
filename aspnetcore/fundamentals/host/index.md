---
title: ASP.NET Core의 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 ASP.NET Core 웹 호스트 및 .NET 일반 호스트에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 08/28/2018
uid: fundamentals/host/index
ms.openlocfilehash: 9927722b5080beb94e5628d9e7b54e6d50a5bff8
ms.sourcegitcommit: a669c4e3f42e387e214a354ac4143555602e6f66
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43336052"
---
# <a name="host-in-aspnet-core"></a><span data-ttu-id="452e1-103">ASP.NET Core의 호스트</span><span class="sxs-lookup"><span data-stu-id="452e1-103">Host in ASP.NET Core</span></span>

<span data-ttu-id="452e1-104">.NET 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-104">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="452e1-105">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-105">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="452e1-106">두 개의 호스트 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-106">Two host APIs are available for use:</span></span>

* <span data-ttu-id="452e1-107">[웹 호스트](xref:fundamentals/host/web-host) &ndash; 웹 응용 프로그램을 호스팅하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-107">[Web Host](xref:fundamentals/host/web-host) &ndash; Suitable for hosting web apps.</span></span>
* <span data-ttu-id="452e1-108">[일반 호스트](xref:fundamentals/host/generic-host)(ASP.NET Core 2.1 이상) &ndash; 웹이 아닌 앱(예: 백그라운드 작업을 실행하는 앱)을 호스팅하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-108">[Generic Host](xref:fundamentals/host/generic-host) (ASP.NET Core 2.1 or later) &ndash; Suitable for hosting non-web apps (for example, apps that run background tasks).</span></span> <span data-ttu-id="452e1-109">이후 릴리스에서는 일반 호스트가 웹앱을 포함한 모든 종류의 앱을 호스팅하는 데 적합해질 것입니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-109">In a future release, the Generic Host will be suitable for hosting any kind of app, including web apps.</span></span> <span data-ttu-id="452e1-110">일반 호스트는 결국 웹 호스트를 대체하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-110">The Generic Host will eventually replace the Web Host.</span></span>

<span data-ttu-id="452e1-111">ASP.NET Core *웹앱*을 호스팅할 때 개발자는 <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>에 기반한 웹 호스트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-111">For hosting ASP.NET Core *web apps*, developers should use the Web Host based on <xref:Microsoft.AspNetCore.Hosting.IWebHostBuilder>.</span></span> <span data-ttu-id="452e1-112">*비 웹앱*을 호스팅할 때 개발자는 <xref:Microsoft.Extensions.Hosting.HostBuilder>에 기반한 제네릭 호스트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-112">For hosting *non-web apps*, developers should use the Generic Host based on <xref:Microsoft.Extensions.Hosting.HostBuilder>.</span></span>

<xref:fundamentals/host/hosted-services>  
<span data-ttu-id="452e1-113">ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업을 구현하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-113">Learn how to implement background tasks with hosted services in ASP.NET Core.</span></span>

<xref:fundamentals/configuration/platform-specific-configuration>  
<span data-ttu-id="452e1-114"><xref:Microsoft.AspNetCore.Hosting.IHostingStartup> 구현을 사용하여 참조되거나 참조되지 않은 어셈블리에서 ASP.NET Core 앱을 강화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="452e1-114">Discover how to enhance an ASP.NET Core app from a referenced or unreferenced assembly using an <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> implementation.</span></span>
