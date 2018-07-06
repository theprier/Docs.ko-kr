---
uid: signalr/overview/releases/upgrading-signalr-1x-projects-to-20
title: SignalR 1.x 프로젝트를 버전 2로 업그레이드 | Microsoft Docs
author: pfletcher
description: 이 항목에서는 signalr 기존 SignalR 1.x 프로젝트를 업그레이드 하는 방법에 설명 합니다 2.x 및 업그레이드 프로세스 중 발생할 수 있는 문제를 해결 하는 방법...
ms.author: aspnetcontent
ms.date: 06/10/2014
ms.assetid: adcfef99-9bc5-489d-a91b-9b7c2bc35e04
msc.legacyurl: /signalr/overview/releases/upgrading-signalr-1x-projects-to-20
msc.type: authoredcontent
ms.openlocfilehash: 393beb1ef696bd2dfae25789f79a67157780a219
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824165"
---
<a name="upgrading-signalr-1x-projects-to-version-2"></a><span data-ttu-id="19557-103">SignalR 1.x 프로젝트를 버전 2로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="19557-103">Upgrading SignalR 1.x Projects to version 2</span></span>
====================
<span data-ttu-id="19557-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="19557-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="19557-105">이 항목에서는 signalr 기존 SignalR 1.x 프로젝트를 업그레이드 하는 방법에 설명 합니다 2.x 및 업그레이드 프로세스 중 발생할 수 있는 문제를 해결 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="19557-105">This topic describes how to upgrade an existing SignalR 1.x project to SignalR 2.x, and how to troubleshoot issues that may arise during the upgrade process.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="19557-106">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="19557-106">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="19557-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="19557-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="19557-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="19557-108">.NET 4.5</span></span>
> - <span data-ttu-id="19557-109">SignalR 버전 1과 2</span><span class="sxs-lookup"><span data-stu-id="19557-109">SignalR versions 1 and 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="19557-110">이 자습서를 사용 하 여 Visual Studio 2012를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="19557-110">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="19557-111">이 자습서를 사용 하 여 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-111">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="19557-112">업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 최신 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-112">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="19557-113">설치 합니다 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-113">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="19557-114">웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-114">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="19557-115">SignalR 클래스에 대 한 Visual Studio 템플릿 같은 설치 합니다 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-115">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="19557-116">일부 템플릿 (와 같은 **OWIN 시작 클래스**)를 사용할 수 없습니다;이 대 한 클래스 파일을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-116">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="19557-117">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="19557-117">Questions and comments</span></span>
> 
> <span data-ttu-id="19557-118">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="19557-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="19557-119">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="19557-120">SignalR 2를 사용 하 여 서버 플랫폼에서 일관 된 개발 환경을 제공 [OWIN](http://owin.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-120">SignalR 2 offers a consistent development experience across server platforms using [OWIN](http://owin.org).</span></span> <span data-ttu-id="19557-121">이 문서에서는 버전 2로 SignalR 1.x 응용 프로그램을 업데이트 하는 데 필요한 몇 가지 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-121">This article describes the few steps that are needed to update a SignalR 1.x application to version 2.</span></span>

<span data-ttu-id="19557-122">SignalR 2로 응용 프로그램을 업그레이드 하는 것이 좋습니다, 있지만 SignalR 1.x를 계속 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-122">While it is encouraged to upgrade applications to SignalR 2, SignalR 1.x will still be supported.</span></span>

<span data-ttu-id="19557-123">이 자습서에는 SignalR 2를 웹 호스팅 응용 프로그램을 업그레이드 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-123">This tutorial describes how to upgrade a web-hosted application to SignalR 2.</span></span> <span data-ttu-id="19557-124">(콘솔 응용 프로그램, Windows 서비스 또는 다른 프로세스에서 서버를 호스팅하는) 자체 호스팅된 응용 프로그램은 이제 SignalR 2에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19557-124">Self-hosted applications (those that host a server in a console application, Windows service, or other process) are now supported under SignalR 2.</span></span> <span data-ttu-id="19557-125">SignalR 2를 사용 하 여 자체 호스팅된 응용 프로그램을 만들기 시작 하는 방법에 대 한 자세한 내용은 [자습서: SignalR 자체 호스팅](../deployment/tutorial-signalr-self-host.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-125">For information on how to get started creating a self-hosted application with SignalR 2, see [Tutorial: SignalR Self-Host](../deployment/tutorial-signalr-self-host.md).</span></span>

## <a name="contents"></a><span data-ttu-id="19557-126">목차</span><span class="sxs-lookup"><span data-stu-id="19557-126">Contents</span></span>

<span data-ttu-id="19557-127">다음 섹션에서는 발생할 수 있는 문제를 해결 하는 방법과 SignalR 프로젝트 업그레이드와 관련 된 태스크를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-127">The following sections describe tasks involved with upgrading SignalR projects, and how to troubleshoot issues that may arise.</span></span>

- [<span data-ttu-id="19557-128">예: SignalR 2 시작 자습서로</span><span class="sxs-lookup"><span data-stu-id="19557-128">Example: Upgrading the Getting Started tutorial to SignalR 2</span></span>](#example)
- [<span data-ttu-id="19557-129">업그레이드 하는 동안 발생 한 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="19557-129">Troubleshooting errors encountered during upgrading</span></span>](#troubleshooting)

<a id="example"></a>

## <a name="example-upgrading-the-getting-started-tutorial-application-to-signalr-2"></a><span data-ttu-id="19557-130">예: Getting Started tutorial 응용 프로그램 업그레이드에서 SignalR 2</span><span class="sxs-lookup"><span data-stu-id="19557-130">Example: Upgrading the Getting Started tutorial application to SignalR 2</span></span>

<span data-ttu-id="19557-131">이 섹션에서는에서 만든 응용 프로그램을 업데이트 합니다 [시작 자습서의 SignalR 1.x 버전](../older-versions/index.md) SignalR 2를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-131">In this section, you'll update the application created in the [SignalR 1.x version of the Getting Started Tutorial](../older-versions/index.md) to use SignalR 2.</span></span>

1. <span data-ttu-id="19557-132">시작 자습서를 마친 후 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-132">Once you've finished the Getting Started tutorial, right-click on the project, and select **Properties**.</span></span> <span data-ttu-id="19557-133">있는지 확인 합니다 **대상 프레임 워크** 로 설정 된 **.NET Framework 4.5.**</span><span class="sxs-lookup"><span data-stu-id="19557-133">Verify that the **Target framework** is set to **.NET Framework 4.5.**</span></span>
2. <span data-ttu-id="19557-134">패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="19557-134">Open the Package Manager Console.</span></span> <span data-ttu-id="19557-135">SignalR 제거 명령을 사용 하 여 프로젝트에서 1.x:</span><span class="sxs-lookup"><span data-stu-id="19557-135">Remove SignalR 1.x from the project using the following command:</span></span>

    [!code-powershell[Main](upgrading-signalr-1x-projects-to-20/samples/sample1.ps1)]
3. <span data-ttu-id="19557-136">다음 명령을 사용 하 여 SignalR 2를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-136">Install SignalR 2 using the following command:</span></span>

    [!code-powershell[Main](upgrading-signalr-1x-projects-to-20/samples/sample2.ps1)]
4. <span data-ttu-id="19557-137">HTML 페이지에 이제 프로젝트에 포함 된 스크립트의 버전과 일치 하도록 SignalR에 대 한 스크립트 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-137">In the HTML page, update the script reference for SignalR to match the version of the script now included in the project.</span></span>

    [!code-html[Main](upgrading-signalr-1x-projects-to-20/samples/sample3.html)]
5. <span data-ttu-id="19557-138">전역 응용 프로그램 클래스에서 MapHubs에 대 한 호출을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-138">In the global application class, remove the call to MapHubs.</span></span>

    [!code-csharp[Main](upgrading-signalr-1x-projects-to-20/samples/sample4.cs)]
6. <span data-ttu-id="19557-139">솔루션을 마우스 오른쪽 단추로 클릭 **추가**, **새 항목...** . 대화 상자에서 선택 **Owin Startup 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-139">Right-click the solution, and select **Add**, **New Item...**. In the dialog, select **Owin Startup Class**.</span></span> <span data-ttu-id="19557-140">새 클래스 이름을 **Startup.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-140">Name the new class **Startup.cs**.</span></span>

    ![](upgrading-signalr-1x-projects-to-20/_static/image1.png)
7. <span data-ttu-id="19557-141">Startup.cs의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="19557-141">Replace the contents of Startup.cs with the following code:</span></span>

    [!code-csharp[Main](upgrading-signalr-1x-projects-to-20/samples/sample5.cs)]

    <span data-ttu-id="19557-142">Owin의 시작 프로세스를 실행 하는 클래스를 추가 하는 어셈블리 특성을 `Configuration` Owin 시작 되 면 메서드.</span><span class="sxs-lookup"><span data-stu-id="19557-142">The assembly attribute adds the class to Owin's startup process, which executes the `Configuration` method when Owin starts up.</span></span> <span data-ttu-id="19557-143">가 호출 된 `MapSignalR` 메서드를 응용 프로그램에서 모든 SignalR 허브에 대 한 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19557-143">This in turn calls the `MapSignalR` method, which creates routes for all SignalR hubs in the application.</span></span>
8. <span data-ttu-id="19557-144">프로젝트를 실행 하 고 다른 기본 페이지의 URL을 복사 브라우저나 이전 처럼 브라우저 창.</span><span class="sxs-lookup"><span data-stu-id="19557-144">Run the project, and copy the URL of the main page into another browser or browser pane, as before.</span></span> <span data-ttu-id="19557-145">각 페이지는 사용자 이름을 요청 하 고 각 페이지에서 보낸 메시지는 두 브라우저 창에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-145">Each page will ask for a username, and messages sent from each page should be visible in both browser panes.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting-errors-encountered-during-upgrading"></a><span data-ttu-id="19557-146">업그레이드 하는 동안 발생 한 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="19557-146">Troubleshooting errors encountered during upgrading</span></span>

<span data-ttu-id="19557-147">이 섹션에서는 업그레이드 하는 동안 발생할 수 있는 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-147">This section describes issues that may arise during upgrading.</span></span> <span data-ttu-id="19557-148">오류 보다 포괄적인 목록과 SignalR 응용 프로그램을 사용 하 여 발생할 수 있는 문제를 참조 하세요 [SignalR 문제 해결](../testing-and-debugging/troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-148">For a more comprehensive list of errors and issues that may occur with a SignalR application, see [SignalR Troubleshooting](../testing-and-debugging/troubleshooting.md).</span></span>

### <a name="the-call-is-ambiguous-between-the-following-methods-or-properties"></a><span data-ttu-id="19557-149">' 호출 되는 다음 메서드 또는 속성 사이 모호한 '</span><span class="sxs-lookup"><span data-stu-id="19557-149">'The call is ambiguous between the following methods or properties'</span></span>

<span data-ttu-id="19557-150">이 오류가 발생 하는 경우에 대 한 참조 `Microsoft.AspNet.SignalR.Owin` 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19557-150">This error will occur if a reference to `Microsoft.AspNet.SignalR.Owin` is not removed.</span></span> <span data-ttu-id="19557-151">이 패키지는 사용 되지 않습니다. 참조를 제거 해야 하 고 SelfHost 패키지의 1.x 버전을 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-151">This package is deprecated; the reference must be removed and the 1.x version of the SelfHost package must be uninstalled.</span></span>

### <a name="hub-methods-fail-silently"></a><span data-ttu-id="19557-152">허브 메서드를 자동으로 실패</span><span class="sxs-lookup"><span data-stu-id="19557-152">Hub methods fail silently</span></span>

<span data-ttu-id="19557-153">날짜 및는 최대 클라이언트에서 스크립트 참조 되는지 확인 합니다 `OwinStartup` Startup 클래스에는 올바른 클래스와 프로젝트의 어셈블리 이름에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="19557-153">Verify that the script references in your client are up to date, and that the `OwinStartup` attribute for your Startup class has the correct class and assembly names for your project.</span></span> <span data-ttu-id="19557-154">또한 열어보세요; 브라우저에서 hubs 주소 (/ signalr 허브) 표시 되는 모든 오류는 무엇이 하는 방법에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19557-154">Also, try opening up the hubs address (/signalr/hubs) in your browser; any error that appears will offer more information about what's going wrong.</span></span>
