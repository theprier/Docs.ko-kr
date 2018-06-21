---
title: ASP.NET Core의 호스트
author: guardrex
description: 앱 시작 및 수명 관리를 담당하는 ASP.NET Core 웹 호스트 및 .NET 일반 호스트에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/16/2018
uid: fundamentals/host/index
ms.openlocfilehash: 365c679e789c07818c6eb007f40f6aef43b82c44
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36276619"
---
# <a name="host-in-aspnet-core"></a><span data-ttu-id="0f8fa-103">ASP.NET Core의 호스트</span><span class="sxs-lookup"><span data-stu-id="0f8fa-103">Host in ASP.NET Core</span></span>

<span data-ttu-id="0f8fa-104">.NET 앱은 *호스트*를 구성 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-104">.NET apps configure and launch a *host*.</span></span> <span data-ttu-id="0f8fa-105">호스트는 앱 시작 및 수명 관리를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-105">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="0f8fa-106">두 개의 호스트 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-106">Two host APIs are available for use:</span></span>

* <span data-ttu-id="0f8fa-107">[웹 호스트](xref:fundamentals/host/web-host) &ndash; 웹 응용 프로그램을 호스팅하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-107">[Web Host](xref:fundamentals/host/web-host) &ndash; Suitable for hosting web apps.</span></span>
* <span data-ttu-id="0f8fa-108">[일반 호스트](xref:fundamentals/host/generic-host)(ASP.NET Core 2.1 이상) &ndash; 웹이 아닌 앱(예: 백그라운드 작업을 실행하는 앱)을 호스팅하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-108">[Generic Host](xref:fundamentals/host/generic-host) (ASP.NET Core 2.1 or later) &ndash; Suitable for hosting non-web apps (for example, apps that run background tasks).</span></span> <span data-ttu-id="0f8fa-109">이후 릴리스에서는 일반 호스트가 웹앱을 포함한 모든 종류의 앱을 호스팅하는 데 적합해질 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-109">In a future release, the Generic Host will be suitable for hosting any kind of app, including web apps.</span></span> <span data-ttu-id="0f8fa-110">일반 호스트는 결국 웹 호스트를 대체하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-110">The Generic Host will eventually replace the Web Host.</span></span>

<span data-ttu-id="0f8fa-111">ASP.NET Core *웹앱*을 호스팅할 때 개발자는 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)에 기반한 웹 호스트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-111">For hosting ASP.NET Core *web apps*, developers should use the Web Host based on [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder).</span></span> <span data-ttu-id="0f8fa-112">*비 웹앱*을 호스팅할 때 개발자는 [HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder)에 기반한 제네릭 호스트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f8fa-112">For hosting *non-web apps*, developers should use the Generic Host based on [HostBuilder](/dotnet/api/microsoft.extensions.hosting.hostbuilder).</span></span>
