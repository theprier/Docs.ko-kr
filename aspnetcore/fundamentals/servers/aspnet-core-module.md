---
title: ASP.NET Core 모듈
author: rick-anderson
description: ASP.NET Core 모듈이 Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 어떻게 사용하도록 허용하는지 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/23/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: 789b0b2e74405256bb0e247ae5ea9697e3cb28e5
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2018
ms.locfileid: "34153707"
---
# <a name="aspnet-core-module"></a><span data-ttu-id="461af-103">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="461af-103">ASP.NET Core Module</span></span>

<span data-ttu-id="461af-104">작성자: [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl) 및 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="461af-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), and [Chris Ross](https://github.com/Tratcher)</span></span> 

<span data-ttu-id="461af-105">ASP.NET Core 모듈은 역방향 프록시 구성에서 ASP.NET Core 앱을 IIS 뒤에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="461af-105">The ASP.NET Core Module allows ASP.NET Core apps to run behind IIS in a reverse proxy configuration.</span></span> <span data-ttu-id="461af-106">IIS는 고급 웹앱 보안 및 관리 효율성 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-106">IIS provides advanced web app security and manageability features.</span></span>

<span data-ttu-id="461af-107">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="461af-107">Supported Windows versions:</span></span>

* <span data-ttu-id="461af-108">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="461af-108">Windows 7 or later</span></span>
* <span data-ttu-id="461af-109">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="461af-109">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="461af-110">ASP.NET Core 모듈은 Kestrel에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-110">The ASP.NET Core Module only works with Kestrel.</span></span> <span data-ttu-id="461af-111">이 모듈은 [HTTP.sys](xref:fundamentals/servers/httpsys)(이전 명칭 [WebListener](xref:fundamentals/servers/weblistener))와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="461af-111">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span>

## <a name="aspnet-core-module-description"></a><span data-ttu-id="461af-112">ASP.NET Core 모듈 설명</span><span class="sxs-lookup"><span data-stu-id="461af-112">ASP.NET Core Module description</span></span>

<span data-ttu-id="461af-113">ASP.NET Core 모듈은 백 엔드 ASP.NET Core 앱으로 웹 요청을 리디렉션하는 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="461af-113">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to redirect web requests to backend ASP.NET Core apps.</span></span> <span data-ttu-id="461af-114">Windows 인증 등의 많은 네이티브 모듈이 활성 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="461af-114">Many native modules, such as Windows Authentication, remain active.</span></span> <span data-ttu-id="461af-115">모듈을 사용하여 활성화된 IIS 모듈에 대해 자세히 알아보려면 [IIS 모듈](xref:host-and-deploy/iis/modules)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="461af-115">To learn more about IIS modules active with the module, see [IIS modules](xref:host-and-deploy/iis/modules).</span></span>

<span data-ttu-id="461af-116">ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리도 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-116">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module also handles process management.</span></span> <span data-ttu-id="461af-117">이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 충돌이 발생하면 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-117">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it crashes.</span></span> <span data-ttu-id="461af-118">이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 IIS에서 In Process로 실행되는 ASP.NET 4.x 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-118">This is essentially the same behavior as seen with ASP.NET 4.x apps that run in-process in IIS that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="461af-119">다음 다이어그램은 IIS, ASP.NET Core 모듈 및 ASP.NET Core 앱 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="461af-119">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and ASP.NET Core apps:</span></span>

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm.png)

<span data-ttu-id="461af-121">요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-121">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="461af-122">드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-122">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="461af-123">모듈은 포트 80/443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-123">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80/443.</span></span>

<span data-ttu-id="461af-124">모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-124">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="461af-125">추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="461af-125">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="461af-126">모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="461af-126">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="461af-127">Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="461af-127">After Kestrel picks up a request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="461af-128">미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-128">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="461af-129">앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="461af-129">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

<span data-ttu-id="461af-130">ASP.NET Core 모듈에는 몇 가지 기타 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="461af-130">The ASP.NET Core Module has a few other functions.</span></span> <span data-ttu-id="461af-131">모듈은 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="461af-131">The module can:</span></span>

* <span data-ttu-id="461af-132">작업자 프로세스의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-132">Set environment variables for the worker process.</span></span>
* <span data-ttu-id="461af-133">시작 문제를 해결하기 위해 stdout 출력을 파일 저장소에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-133">Log stdout output to file storage for troubleshooting startup issues.</span></span>
* <span data-ttu-id="461af-134">Windows 인증 토큰을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="461af-134">Forward Windows authentication tokens.</span></span>

## <a name="how-to-install-and-use-the-aspnet-core-module"></a><span data-ttu-id="461af-135">ASP.NET Core 모듈을 설치하고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="461af-135">How to install and use the ASP.NET Core Module</span></span>

<span data-ttu-id="461af-136">ASP.NET Core 모듈을 설치하고 사용하는 방법에 대한 자세한 지침은 [IIS가 있는 Windows에서 호스트](xref:host-and-deploy/iis/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="461af-136">For detailed instructions on how to install and use the ASP.NET Core Module, see [Host on Windows with IIS](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="461af-137">모듈 구성에 대한 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="461af-137">For information on configuring the module, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="461af-138">추가 자료</span><span class="sxs-lookup"><span data-stu-id="461af-138">Additional resources</span></span>

* [<span data-ttu-id="461af-139">IIS를 사용하여 Windows에서 호스트</span><span class="sxs-lookup"><span data-stu-id="461af-139">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="461af-140">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="461af-140">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="461af-141">ASP.NET Core 모듈 GitHub 리포지토리(소스 코드)</span><span class="sxs-lookup"><span data-stu-id="461af-141">ASP.NET Core Module GitHub repository (source code)</span></span>](https://github.com/aspnet/AspNetCoreModule)
