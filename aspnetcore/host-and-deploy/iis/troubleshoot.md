---
title: "IIS에서 ASP.NET Core 문제 해결"
author: guardrex
description: "ASP.NET Core 응용 프로그램의 인터넷 정보 서비스 (IIS) 배포와 문제를 진단 하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/07/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: 65173e0101a17c64f4cde583e5bbb9fb0a9c7718
ms.sourcegitcommit: b83a5f731a9c02bdb1cc1e3f9a8bf273eb5b33e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="troubleshoot-aspnet-core-on-iis"></a><span data-ttu-id="d2a43-103">IIS에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d2a43-103">Troubleshoot ASP.NET Core on IIS</span></span>

<span data-ttu-id="d2a43-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="d2a43-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d2a43-105">이 문서에서는 설명 ASP.NET Core를 진단 하는 방법에 응용 프로그램 시작 문제를 호스트 하는 경우 [인터넷 정보 서비스 (IIS)](/iis)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue when hosting with [Internet Information Services (IIS)](/iis).</span></span> <span data-ttu-id="d2a43-106">이 문서의 정보는 Windows Server 및 Windows 바탕 화면에는 IIS에서 호스팅에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-106">The information in this article applies to hosting in IIS on Windows Server and Windows Desktop.</span></span>

<span data-ttu-id="d2a43-107">Visual Studio에서 ASP.NET Core 프로젝트 기본값은 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 디버깅 하는 동안 호스팅.</span><span class="sxs-lookup"><span data-stu-id="d2a43-107">In Visual Studio, an ASP.NET Core project defaults to [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) hosting during debugging.</span></span> <span data-ttu-id="d2a43-108">A *502.5 프로세스 오류* 로컬로 troubleshooted 권장 하는이 항목의 사용 될 수 있습니다 디버깅 하는 경우 발생 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-108">A *502.5 Process Failure* that occurs when debugging locally can be troubleshooted using the advice in this topic.</span></span>

<span data-ttu-id="d2a43-109">추가 문제 해결 항목:</span><span class="sxs-lookup"><span data-stu-id="d2a43-109">Additional troubleshooting topics:</span></span>

[<span data-ttu-id="d2a43-110">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d2a43-110">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="d2a43-111">앱 서비스를 사용 하지는 않지만 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 및 호스트 응용 프로그램에는 IIS 응용 프로그램 서비스와 관련 된 지침에 대 한 전용된 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2a43-111">Although App Service uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and IIS to host apps, see the dedicated topic for instructions specific to App Service.</span></span>

[<span data-ttu-id="d2a43-112">오류 처리</span><span class="sxs-lookup"><span data-stu-id="d2a43-112">Error handling</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="d2a43-113">로컬 시스템에서 개발 하는 동안 ASP.NET Core 응용 프로그램에서 오류를 처리 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-113">Discover how to handle errors in ASP.NET Core apps during development on a local system.</span></span>

[<span data-ttu-id="d2a43-114">Visual Studio를 사용하여 디버깅하는 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="d2a43-114">Learn to debug using Visual Studio</span></span>](/visualstudio/debugger/getting-started-with-the-debugger)  
<span data-ttu-id="d2a43-115">이 항목에서는 Visual Studio 디버거 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-115">This topic introduces the features of the Visual Studio debugger.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="d2a43-116">응용 프로그램 시작 오류</span><span class="sxs-lookup"><span data-stu-id="d2a43-116">App startup errors</span></span>

<span data-ttu-id="d2a43-117">**502.5 프로세스 오류**</span><span class="sxs-lookup"><span data-stu-id="d2a43-117">**502.5 Process Failure**</span></span>  
<span data-ttu-id="d2a43-118">작업자 프로세스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-118">The worker process fails.</span></span> <span data-ttu-id="d2a43-119">응용 프로그램을 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-119">The app doesn't start.</span></span>

<span data-ttu-id="d2a43-120">ASP.NET Core 모듈 작업자 프로세스를 시작 하려고 시도 하지만 시작 하지 못한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-120">The ASP.NET Core Module attempts to start the worker process but it fails to start.</span></span> <span data-ttu-id="d2a43-121">프로세스 시작 실패의 원인을 일반적으로 항목에서 확인할 수 있습니다는 [응용 프로그램 이벤트 로그](#application-event-log) 및 [ASP.NET Core 모듈 stdout 로그](#aspnet-core-module-stdout-log)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-121">The cause of a process startup failure can usually be determined from entries in the [Application Event Log](#application-event-log) and the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log).</span></span>

<span data-ttu-id="d2a43-122">*502.5 프로세스 오류* 호스팅 또는 응용 프로그램 구성이 잘못 작업자 프로세스가 실패 하면 오류 페이지가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-122">The *502.5 Process Failure* error page is returned when a hosting or app misconfiguration causes the worker process to fail:</span></span>

![브라우저 창에 502.5 프로세스 오류 페이지를 표시 합니다.](troubleshoot/_static/process-failure-page.png)

<span data-ttu-id="d2a43-124">**500 내부 서버 오류**</span><span class="sxs-lookup"><span data-stu-id="d2a43-124">**500 Internal Server Error**</span></span>  
<span data-ttu-id="d2a43-125">응용 프로그램 시작 하지만 오류는 서버에서 요청을 수행할 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-125">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="d2a43-126">시작 하는 동안 또는 응답을 만드는 동안 응용 프로그램의 코드 내에서이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-126">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="d2a43-127">응답 없는 콘텐츠를 포함할 수 또는 응답으로 나타날 수 있습니다는 *500 내부 서버 오류* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-127">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="d2a43-128">응용 프로그램 이벤트 로그는 일반적으로 응용 프로그램이 정상적으로 시작 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-128">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="d2a43-129">서버의 관점에서는 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-129">From the server's perspective, that's correct.</span></span> <span data-ttu-id="d2a43-130">응용 프로그램 시작 않았습니다 하지만 유효한 응답을 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-130">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="d2a43-131">[명령 프롬프트에서 앱 실행](#run-the-app-at-a-command-prompt) 서버의 또는 [ASP.NET Core 모듈 stdout 로그 사용](#aspnet-core-module-stdout-log) 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-131">[Run the app at a command prompt](#run-the-app-at-a-command-prompt) on the server or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

<span data-ttu-id="d2a43-132">**연결 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="d2a43-132">**Connection reset**</span></span>

<span data-ttu-id="d2a43-133">보낼 서버에 대 한 너무 늦을 때 헤더를 보낸 다음 오류가 발생 하는 경우는 **500 내부 서버 오류** 오류가 발생할 경우.</span><span class="sxs-lookup"><span data-stu-id="d2a43-133">If an error occurs after the headers are sent, it's too late for the server to send a **500 Internal Server Error** when an error occurs.</span></span> <span data-ttu-id="d2a43-134">이 문제는 종종 복잡 한 개체에 대 한 응답을 직렬화 하는 동안 오류가 발생 하면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-134">This often happens when an error occurs during the serialization of complex objects for a response.</span></span> <span data-ttu-id="d2a43-135">으로 이러한 종류의 오류 표시는 *연결 다시 설정* 클라이언트에 대 한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-135">This type of error appears as a *connection reset* error on the client.</span></span> <span data-ttu-id="d2a43-136">[응용 프로그램 로깅](xref:fundamentals/logging/index) 이러한 종류의 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-136">[Application logging](xref:fundamentals/logging/index) can help troubleshoot these types of errors.</span></span>

## <a name="default-startup-limits"></a><span data-ttu-id="d2a43-137">기본 시작 제한</span><span class="sxs-lookup"><span data-stu-id="d2a43-137">Default startup limits</span></span>

<span data-ttu-id="d2a43-138">ASP.NET Core 모듈 구성 된 기본 *startupTimeLimit* 120 초입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-138">The ASP.NET Core Module is configured with a default *startupTimeLimit* of 120 seconds.</span></span> <span data-ttu-id="d2a43-139">기본값에 그대로 유지, 응용 프로그램 모듈 프로세스 오류를 기록 하기 전에 시작 하려면 최대 2 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-139">When left at the default value, an app may take up to two minutes to start before the module logs a process failure.</span></span> <span data-ttu-id="d2a43-140">모듈 구성에 대 한 참조 [aspNetCore 요소의 특성](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-140">For information on configuring the module, see [Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="d2a43-141">응용 프로그램 시작 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d2a43-141">Troubleshoot app startup errors</span></span>

### <a name="application-event-log"></a><span data-ttu-id="d2a43-142">응용 프로그램 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="d2a43-142">Application Event Log</span></span>

<span data-ttu-id="d2a43-143">응용 프로그램 이벤트 로그에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-143">Access the Application Event Log:</span></span>

1. <span data-ttu-id="d2a43-144">시작 메뉴를 열고, 검색할 **이벤트 뷰어**를 선택한 후는 **이벤트 뷰어** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-144">Open the Start menu, search for **Event Viewer**, and then select the **Event Viewer** app.</span></span>
1. <span data-ttu-id="d2a43-145">**이벤트 뷰어**열고는 **Windows 로그** 노드.</span><span class="sxs-lookup"><span data-stu-id="d2a43-145">In **Event Viewer**, open the **Windows Logs** node.</span></span>
1. <span data-ttu-id="d2a43-146">선택 **응용 프로그램** 를 응용 프로그램 이벤트 로그를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-146">Select **Application** to open the Application Event Log.</span></span>
1. <span data-ttu-id="d2a43-147">실패 한 앱과 연결 된 오류에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-147">Search for errors associated with the failing app.</span></span> <span data-ttu-id="d2a43-148">오류 값을 가질 *IIS AspNetCore 모듈* 또는 *IIS Express AspNetCore 모듈* 에 *소스* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-148">Errors have a value of *IIS AspNetCore Module* or *IIS Express AspNetCore Module* in the *Source* column.</span></span>

### <a name="run-the-app-at-a-command-prompt"></a><span data-ttu-id="d2a43-149">명령 프롬프트에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="d2a43-149">Run the app at a command prompt</span></span>

<span data-ttu-id="d2a43-150">많은 시작 오류 응용 프로그램 이벤트 로그에서 유용한 정보를 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-150">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="d2a43-151">호스팅 시스템에서 명령 프롬프트에서 앱을 실행 하 여 일부 오류 원인을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-151">You can find the cause of some errors by running the app at a command prompt on the hosting system.</span></span>

<span data-ttu-id="d2a43-152">**프레임 워크 종속 배포**</span><span class="sxs-lookup"><span data-stu-id="d2a43-152">**Framework-dependent deployment**</span></span>

<span data-ttu-id="d2a43-153">하는 경우는 [프레임 워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span><span class="sxs-lookup"><span data-stu-id="d2a43-153">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span></span>

1. <span data-ttu-id="d2a43-154">명령 프롬프트에서 배포 폴더로 이동 하 고 사용 하 여 응용 프로그램의 어셈블리를 실행 하 여 앱을 실행 *dotnet.exe*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-154">At a command prompt, navigate to the deployment folder and run the app by executing the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="d2a43-155">다음 명령에서에 대 한 응용 프로그램의 어셈블리의 이름을 바꾸어야 \<assembly_name >: `dotnet .\<assembly_name>.dll`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-155">In the following command, substitute the name of the app's assembly for \<assembly_name>: `dotnet .\<assembly_name>.dll`.</span></span>
1. <span data-ttu-id="d2a43-156">오류를 보여 주는 응용 프로그램에서 콘솔 출력은 콘솔 창에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-156">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="d2a43-157">응용 프로그램에 요청을 하는 경우는 오류가 발생 한 경우 호스트 및 Kestrel 수신 대기 포트에 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-157">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="d2a43-158">요청을 수행 기본 호스트 및 게시를 사용 하 여 `http://localhost:5000/`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-158">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="d2a43-159">응용 프로그램 Kestrel 끝점 주소에서 정상적으로 응답을 하는 경우 문제가 관련 역방향 프록시 구성 및 응용 프로그램 내에서 될 가능성이 적기 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-159">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

<span data-ttu-id="d2a43-160">**자체 포함된 배포**</span><span class="sxs-lookup"><span data-stu-id="d2a43-160">**Self-contained deployment**</span></span>

<span data-ttu-id="d2a43-161">하는 경우는 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd):</span><span class="sxs-lookup"><span data-stu-id="d2a43-161">If the app is a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd):</span></span>

1. <span data-ttu-id="d2a43-162">명령 프롬프트에서 배포 폴더로 이동한 다음 응용 프로그램의 실행 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-162">At a command prompt, navigate to the deployment folder and run the app's executable.</span></span> <span data-ttu-id="d2a43-163">다음 명령에서에 대 한 응용 프로그램의 어셈블리의 이름을 바꾸어야 \<assembly_name >: `<assembly_name>.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-163">In the following command, substitute the name of the app's assembly for \<assembly_name>: `<assembly_name>.exe`.</span></span>
1. <span data-ttu-id="d2a43-164">오류를 보여 주는 응용 프로그램에서 콘솔 출력은 콘솔 창에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-164">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="d2a43-165">응용 프로그램에 요청을 하는 경우는 오류가 발생 한 경우 호스트 및 Kestrel 수신 대기 포트에 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-165">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="d2a43-166">요청을 수행 기본 호스트 및 게시를 사용 하 여 `http://localhost:5000/`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-166">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="d2a43-167">응용 프로그램 Kestrel 끝점 주소에서 정상적으로 응답을 하는 경우 문제가 관련 역방향 프록시 구성 및 응용 프로그램 내에서 될 가능성이 적기 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-167">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="d2a43-168">ASP.NET Core 모듈 stdout 로그</span><span class="sxs-lookup"><span data-stu-id="d2a43-168">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="d2a43-169">사용 하도록 설정 하 고 stdout 로그를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2a43-169">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="d2a43-170">호스팅 시스템에 표시 되는 사이트의 배포 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-170">Navigate to the site's deployment folder on the hosting system.</span></span>
1. <span data-ttu-id="d2a43-171">경우는 *로그* 폴더 존재 하지, 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-171">If the *logs* folder isn't present, create the folder.</span></span> <span data-ttu-id="d2a43-172">MSBuild를 사용 하도록 설정 하는 방법에 만드는 지침은 *로그* 폴더 배포에서 자동으로 참조는 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-172">For instructions on how to enable MSBuild to create the *logs* folder in the deployment automatically, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>
1. <span data-ttu-id="d2a43-173">편집 된 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-173">Edit the *web.config* file.</span></span> <span data-ttu-id="d2a43-174">설정 **stdoutLogEnabled** 를 `true` 변경 하 고는 **가 stdoutLogFile** 가리키도록 경로 *로그* 폴더 (예를 들어 `.\logs\stdout`).</span><span class="sxs-lookup"><span data-stu-id="d2a43-174">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to point to the *logs* folder (for example, `.\logs\stdout`).</span></span> <span data-ttu-id="d2a43-175">`stdout`경로에 로그 파일 이름 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-175">`stdout` in the path is the log file name prefix.</span></span> <span data-ttu-id="d2a43-176">로그를 만들 때 타임 스탬프, 프로세스 id 및 파일 확장명이 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-176">A timestamp, process id, and file extension are added automatically when the log is created.</span></span> <span data-ttu-id="d2a43-177">사용 하 여 `stdout` 일반적인 로그 파일의 이름은 파일 이름 접두사로 *stdout_20180205184032_5412.log*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-177">Using `stdout` as the file name prefix, a typical log file is named *stdout_20180205184032_5412.log*.</span></span> 
1. <span data-ttu-id="d2a43-178">업데이트 된 저장 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-178">Save the updated *web.config* file.</span></span>
1. <span data-ttu-id="d2a43-179">응용 프로그램에 요청을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-179">Make a request to the app.</span></span>
1. <span data-ttu-id="d2a43-180">탐색 하 고 *로그* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-180">Navigate to the *logs* folder.</span></span> <span data-ttu-id="d2a43-181">찾기 및 가장 최근의 stdout 로그를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-181">Find and open the most recent stdout log.</span></span>
1. <span data-ttu-id="d2a43-182">로그에서 오류를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-182">Study the log for errors.</span></span>

<span data-ttu-id="d2a43-183">**기억해 야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2a43-183">**Important!**</span></span> <span data-ttu-id="d2a43-184">Stdout 문제 해결이 완료 될 때의 로깅이 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="d2a43-184">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="d2a43-185">편집 된 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-185">Edit the *web.config* file.</span></span>
1. <span data-ttu-id="d2a43-186">설정 **stdoutLogEnabled** 를 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-186">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="d2a43-187">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-187">Save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="d2a43-188">Stdout 로그를 사용 하지 않도록 설정 하지 않으면 응용 프로그램 또는 서버 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-188">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="d2a43-189">로그 파일 크기에 제한이 없음을 또는 로그 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-189">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="d2a43-190">ASP.NET Core 응용 프로그램의 일상적인 로깅에 대 한 로그 파일 크기를 제한 하 고 로그를 회전 하는 로깅 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-190">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="d2a43-191">자세한 내용은 참조 [제 3 자 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-191">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="enabling-the-developer-exception-page"></a><span data-ttu-id="d2a43-192">개발자 예외 페이지를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d2a43-192">Enabling the Developer Exception Page</span></span>

<span data-ttu-id="d2a43-193">`ASPNETCORE_ENVIRONMENT` [web.config에 환경 변수를 추가할 수 있습니다](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 개발 환경에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-193">The `ASPNETCORE_ENVIRONMENT` [environment variable can be added to web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) to run the app in the Development environment.</span></span> <span data-ttu-id="d2a43-194">으로 환경에서 응용 프로그램 시작에서 재정의 되지 않습니다 `UseEnvironment` 호스트 작성기 허용 환경 변수를 설정의 [개발자 예외 페이지](xref:fundamentals/error-handling) 표시할 때 앱이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-194">As long as the environment isn't overridden in app startup by `UseEnvironment` on the host builder, setting the environment variable allows the [Developer Exception Page](xref:fundamentals/error-handling) to appear when the app is run.</span></span>

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

<span data-ttu-id="d2a43-195">에 대 한 환경 변수를 설정 `ASPNETCORE_ENVIRONMENT` 준비 하 고 테스트 하는 인터넷에 노출 되지 않습니다는 서버에서 사용 하기 위해만 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-195">Setting the environment variable for `ASPNETCORE_ENVIRONMENT` is only recommended for use on staging and testing servers that aren't exposed to the Internet.</span></span> <span data-ttu-id="d2a43-196">환경 변수를 제거는 *web.config* 문제 해결 후 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-196">Remove the environment variable from the *web.config* file after troubleshooting.</span></span> <span data-ttu-id="d2a43-197">환경 변수 설정에 대 한 내용은 *web.config*, 참조 [aspNetCore의 자식 요소 environmentVariables](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-197">For information on setting environment variables in *web.config*, see [environmentVariables child element of aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="d2a43-198">일반적인 시작 오류</span><span class="sxs-lookup"><span data-stu-id="d2a43-198">Common startup errors</span></span> 

<span data-ttu-id="d2a43-199">참조는 [ASP.NET Core 오류 통칭](xref:host-and-deploy/azure-iis-errors-reference)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-199">See the [ASP.NET Core common errors reference](xref:host-and-deploy/azure-iis-errors-reference).</span></span> <span data-ttu-id="d2a43-200">대부분의 응용 프로그램 시작을 방해 하는 일반적인 문제는 참조 항목에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-200">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="slow-or-hanging-app"></a><span data-ttu-id="d2a43-201">느린 되거나 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2a43-201">Slow or hanging app</span></span>

<span data-ttu-id="d2a43-202">앱 느리게 응답 하거나 요청에 응답 하지를 구하여 분석는 [덤프 파일](/visualstudio/debugger/using-dump-files)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-202">When an app responds slowly or hangs on a request, obtain and analyze a [dump file](/visualstudio/debugger/using-dump-files).</span></span> <span data-ttu-id="d2a43-203">다음 도구 중 하나를 사용 하 여 덤프 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-203">Dump files can be obtained using any of the following tools:</span></span>

* [<span data-ttu-id="d2a43-204">ProcDump</span><span class="sxs-lookup"><span data-stu-id="d2a43-204">ProcDump</span></span>](/sysinternals/downloads/procdump)
* [<span data-ttu-id="d2a43-205">DebugDiag</span><span class="sxs-lookup"><span data-stu-id="d2a43-205">DebugDiag</span></span>](https://www.microsoft.com/download/details.aspx?id=49924)
* <span data-ttu-id="d2a43-206">WinDbg: [Windows 용 디버깅 도구를 다운로드](https://developer.microsoft.com/windows/hardware/download-windbg), [를 사용 하 여 WinDbg 디버깅](/windows-hardware/drivers/debugger/debugging-using-windbg)</span><span class="sxs-lookup"><span data-stu-id="d2a43-206">WinDbg: [Download Debugging tools for Windows](https://developer.microsoft.com/windows/hardware/download-windbg), [Debugging Using WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="d2a43-207">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="d2a43-207">Remote debugging</span></span>

<span data-ttu-id="d2a43-208">참조 [Visual Studio 2017에 원격 IIS 컴퓨터에 있는 원격 디버깅 ASP.NET Core](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) Visual Studio 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-208">See [Remote Debug ASP.NET Core on a Remote IIS Computer in Visual Studio 2017](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) in the Visual Studio documentation.</span></span>

## <a name="application-insights"></a><span data-ttu-id="d2a43-209">응용 프로그램 정보</span><span class="sxs-lookup"><span data-stu-id="d2a43-209">Application Insights</span></span>

<span data-ttu-id="d2a43-210">[Application Insights](/azure/application-insights/) 오류 로깅 및 보고 기능을 포함 하 여 IIS에서 호스트 되는 앱에서 원격 분석을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-210">[Application Insights](/azure/application-insights/) provides telemetry from apps hosted by IIS, including error logging and reporting features.</span></span> <span data-ttu-id="d2a43-211">Application Insights에서 응용 프로그램의 로깅 기능을 사용할 수 있게 하는 경우 응용 프로그램에서 시작 된 이후에 발생 하는 오류만 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-211">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="d2a43-212">자세한 내용은 참조 [ASP.NET Core 용 Application Insights](/azure/application-insights/app-insights-asp-net-core)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-212">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="additional-troubleshooting-advice"></a><span data-ttu-id="d2a43-213">추가 문제 해결 도움말 제공</span><span class="sxs-lookup"><span data-stu-id="d2a43-213">Additional troubleshooting advice</span></span>

<span data-ttu-id="d2a43-214">경우에 따라 작동 중인 응용 프로그램 중 하나가.NET Core SDK 앱 내에서 개발 컴퓨터 또는 패키지 버전에서 업그레이드 한 후에 즉시 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-214">Sometimes a functioning app fails immediately after upgrading either the .NET Core SDK on the development machine or package versions within the app.</span></span> <span data-ttu-id="d2a43-215">경우에 따라 중요한 업그레이드를 수행할 때 일관되지 않은 패키지로 인해 응용 프로그램이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-215">In some cases, incoherent packages may break an app when performing major upgrades.</span></span> <span data-ttu-id="d2a43-216">다음과 같은이 방법으로 이러한 문제를 대부분 해결할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="d2a43-216">Most of these issues can be fixed by following these instructions:</span></span>

1. <span data-ttu-id="d2a43-217">삭제 된 *bin* 및 *obj* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-217">Delete the *bin* and *obj* folders.</span></span>
1. <span data-ttu-id="d2a43-218">패키지에서 캐시 지우기 *% UserProfile %\\.nuget\\패키지* 및 *% LocalAppData %\\Nuget\\v3 캐시*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-218">Clear the package caches at *%UserProfile%\\.nuget\\packages* and *%LocalAppData%\\Nuget\\v3-cache*.</span></span>
1. <span data-ttu-id="d2a43-219">복원 하 고 프로젝트를 다시 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="d2a43-219">Restore and rebuild the project.</span></span>
1. <span data-ttu-id="d2a43-220">서버에서 이전 배포 응용 프로그램을 다시 배포 하기 전에 완전히 삭제 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-220">Confirm that the prior deployment on the server has been completely deleted prior to redeploying the app.</span></span>

> [!TIP]
> <span data-ttu-id="d2a43-221">패키지 캐시의 선택을 취소 하는 편리한 방법을 실행 하는 것 `dotnet nuget locals all --clear` 명령 프롬프트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-221">A convenient way to clear package caches is to execute `dotnet nuget locals all --clear` from a command prompt.</span></span>
> 
> <span data-ttu-id="d2a43-222">패키지 캐시를 지우기 수행할 수도 있습니다를 사용 하 여는 [nuget.exe](https://www.nuget.org/downloads) 도구 및 명령 실행 `nuget locals all -clear`합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-222">Clearing package caches can also be accomplished by using the [nuget.exe](https://www.nuget.org/downloads) tool and executing the command `nuget locals all -clear`.</span></span> <span data-ttu-id="d2a43-223">*nuget.exe* Windows 데스크톱 운영 체제에 설치를 번들로 묶은 아니고에서 별도로 구입 해야는 [NuGet 웹 사이트](https://www.nuget.org/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a43-223">*nuget.exe* isn't a bundled install with the Windows desktop operating system and must be obtained separately from the [NuGet website](https://www.nuget.org/downloads).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2a43-224">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d2a43-224">Additional resources</span></span>

* [<span data-ttu-id="d2a43-225">ASP.NET Core의 오류 처리 소개</span><span class="sxs-lookup"><span data-stu-id="d2a43-225">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)
* [<span data-ttu-id="d2a43-226">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="d2a43-226">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="d2a43-227">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="d2a43-227">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="d2a43-228">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d2a43-228">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
