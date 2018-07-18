---
title: IIS에서 ASP.NET Core 문제 해결
author: guardrex
description: ASP.NET Core 앱의 IIS(인터넷 정보 서비스) 배포에 대한 문제 진단 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/07/2018
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: cbbdee6849768004476d94c58be4a0e7cc2d6f9e
ms.sourcegitcommit: 661d30492d5ef7bbca4f7e709f40d8f3309d2dac
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37938474"
---
# <a name="troubleshoot-aspnet-core-on-iis"></a><span data-ttu-id="fc796-103">IIS에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="fc796-103">Troubleshoot ASP.NET Core on IIS</span></span>

<span data-ttu-id="fc796-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="fc796-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="fc796-105">이 문서에서는 [IIS(인터넷 정보 서비스)](/iis)를 통해 호스트할 경우 ASP.NET Core 앱 시작 문제를 진단하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-105">This article provides instructions on how to diagnose an ASP.NET Core app startup issue when hosting with [Internet Information Services (IIS)](/iis).</span></span> <span data-ttu-id="fc796-106">이 문서의 정보는 Windows Server 및 Windows 데스크톱의 IIS에서 호스트하는 경우에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-106">The information in this article applies to hosting in IIS on Windows Server and Windows Desktop.</span></span>

<span data-ttu-id="fc796-107">Visual Studio에서 ASP.NET Core 프로젝트는 기본적으로 디버그 중에 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 호스팅으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-107">In Visual Studio, an ASP.NET Core project defaults to [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) hosting during debugging.</span></span> <span data-ttu-id="fc796-108">로컬에서 디버그할 때 발생하는 *502.5 프로세스 실패*는 이 항목의 권장 사항을 사용하여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-108">A *502.5 Process Failure* that occurs when debugging locally can be troubleshooted using the advice in this topic.</span></span>

<span data-ttu-id="fc796-109">추가 문제 해결 항목:</span><span class="sxs-lookup"><span data-stu-id="fc796-109">Additional troubleshooting topics:</span></span>

[<span data-ttu-id="fc796-110">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="fc796-110">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)  
<span data-ttu-id="fc796-111">App Service는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)과 IIS를 사용하여 앱을 호스트하지만 App Service 관련 지침은 전용 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-111">Although App Service uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and IIS to host apps, see the dedicated topic for instructions specific to App Service.</span></span>

[<span data-ttu-id="fc796-112">오류 처리</span><span class="sxs-lookup"><span data-stu-id="fc796-112">Handle errors</span></span>](xref:fundamentals/error-handling)  
<span data-ttu-id="fc796-113">로컬 시스템에서 개발하는 동안 ASP.NET Core 앱에서 오류를 처리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-113">Discover how to handle errors in ASP.NET Core apps during development on a local system.</span></span>

[<span data-ttu-id="fc796-114">Visual Studio를 사용하여 디버깅하는 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="fc796-114">Learn to debug using Visual Studio</span></span>](/visualstudio/debugger/getting-started-with-the-debugger)  
<span data-ttu-id="fc796-115">이 항목에서는 Visual Studio 디버거의 기능을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-115">This topic introduces the features of the Visual Studio debugger.</span></span>

<span data-ttu-id="fc796-116">[Debugging with Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)(Visual Studio Code를 사용한 디버깅)</span><span class="sxs-lookup"><span data-stu-id="fc796-116">[Debugging with Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)</span></span>  
<span data-ttu-id="fc796-117">Visual Studio Code에 기본 제공되는 디버깅 지원에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-117">Learn about the debugging support built into Visual Studio Code.</span></span>

## <a name="app-startup-errors"></a><span data-ttu-id="fc796-118">앱 시작 오류</span><span class="sxs-lookup"><span data-stu-id="fc796-118">App startup errors</span></span>

<span data-ttu-id="fc796-119">**502.5 프로세스 실패**</span><span class="sxs-lookup"><span data-stu-id="fc796-119">**502.5 Process Failure**</span></span>  
<span data-ttu-id="fc796-120">작업자 프로세스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-120">The worker process fails.</span></span> <span data-ttu-id="fc796-121">앱이 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-121">The app doesn't start.</span></span>

<span data-ttu-id="fc796-122">ASP.NET Core 모듈이 작업자 프로세스를 시작하려고 하지만 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-122">The ASP.NET Core Module attempts to start the worker process but it fails to start.</span></span> <span data-ttu-id="fc796-123">프로세스 시작 실패의 원인은 일반적으로 [응용 프로그램 이벤트 로그](#application-event-log) 및 [ASP.NET Core 모듈 stdout 로그](#aspnet-core-module-stdout-log)의 항목에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-123">The cause of a process startup failure can usually be determined from entries in the [Application Event Log](#application-event-log) and the [ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log).</span></span>

<span data-ttu-id="fc796-124">호스팅 또는 앱의 잘못된 구성으로 인해 작업자 프로세스가 실패하면 ‘502.5 프로세스 실패’ 오류 페이지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-124">The *502.5 Process Failure* error page is returned when a hosting or app misconfiguration causes the worker process to fail:</span></span>

![502.5 프로세스 실패 페이지를 보여주는 브라우저 창](troubleshoot/_static/process-failure-page.png)

<span data-ttu-id="fc796-126">**500 내부 서버 오류**</span><span class="sxs-lookup"><span data-stu-id="fc796-126">**500 Internal Server Error**</span></span>  
<span data-ttu-id="fc796-127">앱이 시작되지만 오류로 인해 서버에서 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-127">The app starts, but an error prevents the server from fulfilling the request.</span></span>

<span data-ttu-id="fc796-128">이 오류는 시작하는 동안 또는 응답을 만드는 동안 앱 코드 내에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-128">This error occurs within the app's code during startup or while creating a response.</span></span> <span data-ttu-id="fc796-129">응답에 콘텐츠가 없거나 응답이 브라우저에 ‘500 내부 서버 오류’로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-129">The response may contain no content, or the response may appear as a *500 Internal Server Error* in the browser.</span></span> <span data-ttu-id="fc796-130">응용 프로그램 이벤트 로그는 일반적으로 앱이 정상적으로 시작되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-130">The Application Event Log usually states that the app started normally.</span></span> <span data-ttu-id="fc796-131">서버의 관점에서 보면 맞습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-131">From the server's perspective, that's correct.</span></span> <span data-ttu-id="fc796-132">앱이 시작되었지만 유효한 응답을 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-132">The app did start, but it can't generate a valid response.</span></span> <span data-ttu-id="fc796-133">서버의 [명령 프롬프트에서 앱을 실행](#run-the-app-at-a-command-prompt)하거나 [ASP.NET Core 모듈 stdout 로그를 사용](#aspnet-core-module-stdout-log)하여 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-133">[Run the app at a command prompt](#run-the-app-at-a-command-prompt) on the server or [enable the ASP.NET Core Module stdout log](#aspnet-core-module-stdout-log) to troubleshoot the problem.</span></span>

<span data-ttu-id="fc796-134">**연결 다시 설정**</span><span class="sxs-lookup"><span data-stu-id="fc796-134">**Connection reset**</span></span>

<span data-ttu-id="fc796-135">헤더가 전송된 후 오류가 발생할 경우, 오류가 발생할 때 서버에서 **500 내부 서버 오류**를 전송하는 것은 너무 늦은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-135">If an error occurs after the headers are sent, it's too late for the server to send a **500 Internal Server Error** when an error occurs.</span></span> <span data-ttu-id="fc796-136">응답에 대한 복잡한 개체의 serialization 중에 오류가 발생할 때 이 문제가 종종 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-136">This often happens when an error occurs during the serialization of complex objects for a response.</span></span> <span data-ttu-id="fc796-137">이 유형의 오류는 클라이언트에서 ‘연결 다시 설정’ 오류로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-137">This type of error appears as a *connection reset* error on the client.</span></span> <span data-ttu-id="fc796-138">[응용 프로그램 로깅](xref:fundamentals/logging/index)은 이러한 유형의 오류를 해결하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-138">[Application logging](xref:fundamentals/logging/index) can help troubleshoot these types of errors.</span></span>

## <a name="default-startup-limits"></a><span data-ttu-id="fc796-139">기본 시작 제한</span><span class="sxs-lookup"><span data-stu-id="fc796-139">Default startup limits</span></span>

<span data-ttu-id="fc796-140">ASP.NET Core 모듈은 기본 *startupTimeLimit*이 120초로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-140">The ASP.NET Core Module is configured with a default *startupTimeLimit* of 120 seconds.</span></span> <span data-ttu-id="fc796-141">기본값으로 남아 있으면 앱에서 모듈이 프로세스 실패를 기록하기 전에 시작하는 데 최대 2분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-141">When left at the default value, an app may take up to two minutes to start before the module logs a process failure.</span></span> <span data-ttu-id="fc796-142">모듈 구성에 대한 자세한 내용은 [aspNetCore 요소의 특성](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-142">For information on configuring the module, see [Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

## <a name="troubleshoot-app-startup-errors"></a><span data-ttu-id="fc796-143">앱 시작 오류 해결</span><span class="sxs-lookup"><span data-stu-id="fc796-143">Troubleshoot app startup errors</span></span>

### <a name="application-event-log"></a><span data-ttu-id="fc796-144">응용 프로그램 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="fc796-144">Application Event Log</span></span>

<span data-ttu-id="fc796-145">응용 프로그램 이벤트 로그에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-145">Access the Application Event Log:</span></span>

1. <span data-ttu-id="fc796-146">[시작] 메뉴를 열고 **이벤트 뷰어**를 검색한 다음, **이벤트 뷰어** 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-146">Open the Start menu, search for **Event Viewer**, and then select the **Event Viewer** app.</span></span>
1. <span data-ttu-id="fc796-147">**이벤트 뷰어**에서 **Windows 로그** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-147">In **Event Viewer**, open the **Windows Logs** node.</span></span>
1. <span data-ttu-id="fc796-148">**응용 프로그램**을 선택하여 응용 프로그램 이벤트 로그를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-148">Select **Application** to open the Application Event Log.</span></span>
1. <span data-ttu-id="fc796-149">실패한 앱과 연결된 오류를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-149">Search for errors associated with the failing app.</span></span> <span data-ttu-id="fc796-150">오류는 ‘소스’ 열에서 ‘IIS AspNetCore 모듈’ 또는 ‘IIS Express AspNetCore 모듈’의 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-150">Errors have a value of *IIS AspNetCore Module* or *IIS Express AspNetCore Module* in the *Source* column.</span></span>

### <a name="run-the-app-at-a-command-prompt"></a><span data-ttu-id="fc796-151">명령 프롬프트에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="fc796-151">Run the app at a command prompt</span></span>

<span data-ttu-id="fc796-152">응용 프로그램 이벤트 로그에서 대부분의 시작 오류는 유용한 정보를 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-152">Many startup errors don't produce useful information in the Application Event Log.</span></span> <span data-ttu-id="fc796-153">호스팅 시스템의 명령 프롬프트에서 앱을 실행하여 일부 오류의 원인을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-153">You can find the cause of some errors by running the app at a command prompt on the hosting system.</span></span>

<span data-ttu-id="fc796-154">**프레임워크 종속 배포**</span><span class="sxs-lookup"><span data-stu-id="fc796-154">**Framework-dependent deployment**</span></span>

<span data-ttu-id="fc796-155">앱이 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)인 경우:</span><span class="sxs-lookup"><span data-stu-id="fc796-155">If the app is a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd):</span></span>

1. <span data-ttu-id="fc796-156">명령 프롬프트에서 배포 폴더로 이동하고 *dotnet.exe*로 앱의 어셈블리를 실행하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-156">At a command prompt, navigate to the deployment folder and run the app by executing the app's assembly with *dotnet.exe*.</span></span> <span data-ttu-id="fc796-157">`dotnet .\<assembly_name>.dll` 명령에서 \<assembly_name>을 앱 어셈블리의 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-157">In the following command, substitute the name of the app's assembly for \<assembly_name>: `dotnet .\<assembly_name>.dll`.</span></span>
1. <span data-ttu-id="fc796-158">오류를 표시하는 앱의 콘솔 출력이 콘솔 창에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-158">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="fc796-159">앱에 대한 요청을 실행할 때 오류가 발생하는 경우에는 Kestrel이 수신 대기하는 호스트 및 포트에 대한 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-159">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="fc796-160">기본 호스트 및 게시를 사용하여 `http://localhost:5000/`에 대한 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-160">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="fc796-161">앱이 Kestrel 끝점 주소에서 정상적으로 응답하는 경우, 문제는 역방향 프록시 구성과 관련이 있으며 앱 내에서 관련되었을 가능성은 작습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-161">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

<span data-ttu-id="fc796-162">**자체 포함 배포**</span><span class="sxs-lookup"><span data-stu-id="fc796-162">**Self-contained deployment**</span></span>

<span data-ttu-id="fc796-163">앱이 [자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd)인 경우:</span><span class="sxs-lookup"><span data-stu-id="fc796-163">If the app is a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd):</span></span>

1. <span data-ttu-id="fc796-164">명령 프롬프트에서 배포 폴더로 이동하고 앱의 실행 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-164">At a command prompt, navigate to the deployment folder and run the app's executable.</span></span> <span data-ttu-id="fc796-165">`<assembly_name>.exe` 명령에서 \<assembly_name>을 앱 어셈블리의 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-165">In the following command, substitute the name of the app's assembly for \<assembly_name>: `<assembly_name>.exe`.</span></span>
1. <span data-ttu-id="fc796-166">오류를 표시하는 앱의 콘솔 출력이 콘솔 창에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-166">The console output from the app, showing any errors, is written to the console window.</span></span>
1. <span data-ttu-id="fc796-167">앱에 대한 요청을 실행할 때 오류가 발생하는 경우에는 Kestrel이 수신 대기하는 호스트 및 포트에 대한 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-167">If the errors occur when making a request to the app, make a request to the host and port where Kestrel listens.</span></span> <span data-ttu-id="fc796-168">기본 호스트 및 게시를 사용하여 `http://localhost:5000/`에 대한 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-168">Using the default host and post, make a request to `http://localhost:5000/`.</span></span> <span data-ttu-id="fc796-169">앱이 Kestrel 끝점 주소에서 정상적으로 응답하는 경우, 문제는 역방향 프록시 구성과 관련이 있으며 앱 내에서 관련되었을 가능성은 작습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-169">If the app responds normally at the Kestrel endpoint address, the problem is more likely related to the reverse proxy configuration and less likely within the app.</span></span>

### <a name="aspnet-core-module-stdout-log"></a><span data-ttu-id="fc796-170">ASP.NET Core 모듈 stdout 로그</span><span class="sxs-lookup"><span data-stu-id="fc796-170">ASP.NET Core Module stdout log</span></span>

<span data-ttu-id="fc796-171">stdout 로그를 사용하고 보려면:</span><span class="sxs-lookup"><span data-stu-id="fc796-171">To enable and view stdout logs:</span></span>

1. <span data-ttu-id="fc796-172">호스팅 시스템에서 사이트의 배포 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-172">Navigate to the site's deployment folder on the hosting system.</span></span>
1. <span data-ttu-id="fc796-173">*logs* 폴더가 없으면 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-173">If the *logs* folder isn't present, create the folder.</span></span> <span data-ttu-id="fc796-174">MSBuild를 사용하여 배포에서 *logs* 폴더를 자동으로 만드는 방법에 대한 지침은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-174">For instructions on how to enable MSBuild to create the *logs* folder in the deployment automatically, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>
1. <span data-ttu-id="fc796-175">*web.config* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-175">Edit the *web.config* file.</span></span> <span data-ttu-id="fc796-176">**stdoutLogEnabled**를 `true`로 설정하고 **stdoutLogFile** 경로가 *logs* 폴더를 가리키도록 변경합니다(예: `.\logs\stdout`).</span><span class="sxs-lookup"><span data-stu-id="fc796-176">Set **stdoutLogEnabled** to `true` and change the **stdoutLogFile** path to point to the *logs* folder (for example, `.\logs\stdout`).</span></span> <span data-ttu-id="fc796-177">경로의 `stdout`은 로그 파일 이름 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-177">`stdout` in the path is the log file name prefix.</span></span> <span data-ttu-id="fc796-178">로그가 만들어질 때 타임스탬프, 프로세스 ID 및 파일 확장명이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-178">A timestamp, process id, and file extension are added automatically when the log is created.</span></span> <span data-ttu-id="fc796-179">`stdout`을 파일 이름 접두사로 사용하여 일반적인 로그 파일의 이름은 *stdout_20180205184032_5412.log*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-179">Using `stdout` as the file name prefix, a typical log file is named *stdout_20180205184032_5412.log*.</span></span> 
1. <span data-ttu-id="fc796-180">업데이트된 *web.config* 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-180">Save the updated *web.config* file.</span></span>
1. <span data-ttu-id="fc796-181">앱에 대한 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-181">Make a request to the app.</span></span>
1. <span data-ttu-id="fc796-182">*logs* 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-182">Navigate to the *logs* folder.</span></span> <span data-ttu-id="fc796-183">가장 최근의 stdout 로그를 찾아서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-183">Find and open the most recent stdout log.</span></span>
1. <span data-ttu-id="fc796-184">오류에 대한 로그를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-184">Study the log for errors.</span></span>

<span data-ttu-id="fc796-185">**중요!**</span><span class="sxs-lookup"><span data-stu-id="fc796-185">**Important!**</span></span> <span data-ttu-id="fc796-186">문제 해결이 완료되면 stdout 로깅을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-186">Disable stdout logging when troubleshooting is complete.</span></span>

1. <span data-ttu-id="fc796-187">*web.config* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-187">Edit the *web.config* file.</span></span>
1. <span data-ttu-id="fc796-188">**stdoutLogEnabled**를 `false`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-188">Set **stdoutLogEnabled** to `false`.</span></span>
1. <span data-ttu-id="fc796-189">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-189">Save the file.</span></span>

> [!WARNING]
> <span data-ttu-id="fc796-190">stdout 로그를 사용하지 않도록 설정하지 않으면 앱 또는 서버 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-190">Failure to disable the stdout log can lead to app or server failure.</span></span> <span data-ttu-id="fc796-191">로그 파일 크기 또는 생성되는 로그 파일 수에 대한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-191">There's no limit on log file size or the number of log files created.</span></span>
>
> <span data-ttu-id="fc796-192">ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-192">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="fc796-193">자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-193">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

## <a name="enabling-the-developer-exception-page"></a><span data-ttu-id="fc796-194">개발자 예외 페이지 사용</span><span class="sxs-lookup"><span data-stu-id="fc796-194">Enabling the Developer Exception Page</span></span>

<span data-ttu-id="fc796-195">`ASPNETCORE_ENVIRONMENT` [환경 변수를 web.config에 추가](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)하여 개발 환경에서 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-195">The `ASPNETCORE_ENVIRONMENT` [environment variable can be added to web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) to run the app in the Development environment.</span></span> <span data-ttu-id="fc796-196">앱 시작 시 호스트 작성기의 `UseEnvironment`에 의해 환경이 재정의되지 않는 한, 환경 변수를 설정하면 앱이 실행될 때 [개발자 예외 페이지](xref:fundamentals/error-handling)가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-196">As long as the environment isn't overridden in app startup by `UseEnvironment` on the host builder, setting the environment variable allows the [Developer Exception Page](xref:fundamentals/error-handling) to appear when the app is run.</span></span>

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

<span data-ttu-id="fc796-197">`ASPNETCORE_ENVIRONMENT`에 대한 환경 변수 설정은 인터넷에 노출되지 않은 스테이징 및 테스트 서버에서만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-197">Setting the environment variable for `ASPNETCORE_ENVIRONMENT` is only recommended for use on staging and testing servers that aren't exposed to the Internet.</span></span> <span data-ttu-id="fc796-198">문제를 해결한 후 *web.config* 파일에서 환경 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-198">Remove the environment variable from the *web.config* file after troubleshooting.</span></span> <span data-ttu-id="fc796-199">*web.config*에서 환경 변수를 설정하는 방법에 대한 자세한 내용은[aspNetCore의 environmentVariables 자식 요소](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-199">For information on setting environment variables in *web.config*, see [environmentVariables child element of aspNetCore](xref:host-and-deploy/aspnet-core-module#setting-environment-variables).</span></span>

## <a name="common-startup-errors"></a><span data-ttu-id="fc796-200">일반 시작 오류</span><span class="sxs-lookup"><span data-stu-id="fc796-200">Common startup errors</span></span> 

<span data-ttu-id="fc796-201">[ASP.NET Core 일반 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-201">See the [ASP.NET Core common errors reference](xref:host-and-deploy/azure-iis-errors-reference).</span></span> <span data-ttu-id="fc796-202">앱 시작을 차단하는 대부분의 일반적인 문제는 참조 항목에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-202">Most of the common problems that prevent app startup are covered in the reference topic.</span></span>

## <a name="slow-or-hanging-app"></a><span data-ttu-id="fc796-203">앱이 느리거나 중단됨</span><span class="sxs-lookup"><span data-stu-id="fc796-203">Slow or hanging app</span></span>

<span data-ttu-id="fc796-204">요청 시 앱이 느리게 응답하거나 중단되면 [덤프 파일](/visualstudio/debugger/using-dump-files)을 가져와서 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-204">When an app responds slowly or hangs on a request, obtain and analyze a [dump file](/visualstudio/debugger/using-dump-files).</span></span> <span data-ttu-id="fc796-205">덤프 파일은 다음 도구를 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-205">Dump files can be obtained using any of the following tools:</span></span>

* [<span data-ttu-id="fc796-206">ProcDump</span><span class="sxs-lookup"><span data-stu-id="fc796-206">ProcDump</span></span>](/sysinternals/downloads/procdump)
* [<span data-ttu-id="fc796-207">DebugDiag</span><span class="sxs-lookup"><span data-stu-id="fc796-207">DebugDiag</span></span>](https://www.microsoft.com/download/details.aspx?id=49924)
* <span data-ttu-id="fc796-208">WinDbg: [Windows용 디버깅 도구 다운로드](https://developer.microsoft.com/windows/hardware/download-windbg), [WinDbg를 사용하여 디버그](/windows-hardware/drivers/debugger/debugging-using-windbg)</span><span class="sxs-lookup"><span data-stu-id="fc796-208">WinDbg: [Download Debugging tools for Windows](https://developer.microsoft.com/windows/hardware/download-windbg), [Debugging Using WinDbg](/windows-hardware/drivers/debugger/debugging-using-windbg)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="fc796-209">원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="fc796-209">Remote debugging</span></span>

<span data-ttu-id="fc796-210">Visual Studio 설명서에서 [Visual Studio 2017의 원격 IIS 컴퓨터에서 ASP.NET Core 원격 디버그](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-210">See [Remote Debug ASP.NET Core on a Remote IIS Computer in Visual Studio 2017](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) in the Visual Studio documentation.</span></span>

## <a name="application-insights"></a><span data-ttu-id="fc796-211">응용 프로그램 정보</span><span class="sxs-lookup"><span data-stu-id="fc796-211">Application Insights</span></span>

<span data-ttu-id="fc796-212">[Application Insights](/azure/application-insights/)에서는 오류 로깅 및 보고 기능을 포함하여 IIS를 통해 호스트된 앱의 원격 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-212">[Application Insights](/azure/application-insights/) provides telemetry from apps hosted by IIS, including error logging and reporting features.</span></span> <span data-ttu-id="fc796-213">Application Insights는 앱의 로깅 기능을 사용할 수 있게 될 때 응용 프로그램이 시작된 후 발생하는 오류만 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-213">Application Insights can only report on errors that occur after the app starts when the app's logging features become available.</span></span> <span data-ttu-id="fc796-214">자세한 내용은 [ASP.NET Core용 Application Insights](/azure/application-insights/app-insights-asp-net-core)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc796-214">For more information, see [Application Insights for ASP.NET Core](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="additional-troubleshooting-advice"></a><span data-ttu-id="fc796-215">추가 문제 해결 권장 사항</span><span class="sxs-lookup"><span data-stu-id="fc796-215">Additional troubleshooting advice</span></span>

<span data-ttu-id="fc796-216">개발 컴퓨터의 .NET Core SDK 또는 앱 내의 패키지 버전을 업그레이드한 후에 즉시 작동 중인 앱에서 오류가 발생하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-216">Sometimes a functioning app fails immediately after upgrading either the .NET Core SDK on the development machine or package versions within the app.</span></span> <span data-ttu-id="fc796-217">경우에 따라 중요한 업그레이드를 수행할 때 일관되지 않은 패키지로 인해 응용 프로그램이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-217">In some cases, incoherent packages may break an app when performing major upgrades.</span></span> <span data-ttu-id="fc796-218">이러한 대부분의 문제는 다음 지침에 따라 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-218">Most of these issues can be fixed by following these instructions:</span></span>

1. <span data-ttu-id="fc796-219">*bin* 및 *obj* 폴더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-219">Delete the *bin* and *obj* folders.</span></span>
1. <span data-ttu-id="fc796-220">*%UserProfile%\\.nuget\\packages* 및 *%LocalAppData%\\Nuget\\v3-cache*에 있는 패키지 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-220">Clear the package caches at *%UserProfile%\\.nuget\\packages* and *%LocalAppData%\\Nuget\\v3-cache*.</span></span>
1. <span data-ttu-id="fc796-221">프로젝트를 복원하고 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-221">Restore and rebuild the project.</span></span>
1. <span data-ttu-id="fc796-222">서버의 이전 배포가 앱을 다시 배포하기 전에 완전히 삭제되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-222">Confirm that the prior deployment on the server has been completely deleted prior to redeploying the app.</span></span>

> [!TIP]
> <span data-ttu-id="fc796-223">명령 프롬프트에서 `dotnet nuget locals all --clear`를 실행하면 간편하게 패키지 캐시를 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-223">A convenient way to clear package caches is to execute `dotnet nuget locals all --clear` from a command prompt.</span></span>
> 
> <span data-ttu-id="fc796-224">[nuget.exe](https://www.nuget.org/downloads) 도구를 사용하고 명령 `nuget locals all -clear`를 실행하여 패키지 캐시를 지울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-224">Clearing package caches can also be accomplished by using the [nuget.exe](https://www.nuget.org/downloads) tool and executing the command `nuget locals all -clear`.</span></span> <span data-ttu-id="fc796-225">*nuget.exe*는 Windows 데스크톱 운영 체제와 함께 제공되는 설치가 아니므로 [NuGet 웹 사이트](https://www.nuget.org/downloads)에서 별도로 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc796-225">*nuget.exe* isn't a bundled install with the Windows desktop operating system and must be obtained separately from the [NuGet website](https://www.nuget.org/downloads).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc796-226">추가 자료</span><span class="sxs-lookup"><span data-stu-id="fc796-226">Additional resources</span></span>

* [<span data-ttu-id="fc796-227">ASP.NET Core의 오류 처리 소개</span><span class="sxs-lookup"><span data-stu-id="fc796-227">Introduction to Error Handling in ASP.NET Core</span></span>](xref:fundamentals/error-handling)
* [<span data-ttu-id="fc796-228">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="fc796-228">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="fc796-229">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="fc796-229">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="fc796-230">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="fc796-230">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
