---
uid: visual-studio/overview/2013/using-browser-link
title: Visual Studio 2013의 브라우저 링크를 사용 하 여 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/04/2013
ms.topic: article
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: e5a13405a303580ec8c1d4cdacafc26c6f8ff34a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28044112"
---
<a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="dd316-102">Visual Studio 2013의 브라우저 링크를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="dd316-102">Using Browser Link in Visual Studio 2013</span></span>
====================
<span data-ttu-id="dd316-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="dd316-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="dd316-104">브라우저 링크는 개발 환경 및 하나 이상의 웹 브라우저 간에 통신 채널을 만드는 Visual Studio 2013의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="dd316-105">다중 브라우저 테스트에 대 한 유용한 여러 브라우저에서 웹 응용 프로그램 한 번에 새로 고치려면 브라우저 링크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="dd316-106">브라우저 새로 고침</span><span class="sxs-lookup"><span data-stu-id="dd316-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="dd316-107">브라우저 링크 대시보드 보기</span><span class="sxs-lookup"><span data-stu-id="dd316-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="dd316-108">정적 HTML 파일에 대 한 브라우저 링크를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="dd316-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="dd316-109">브라우저 링크를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="dd316-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="dd316-110">어떻게 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="dd316-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="dd316-111">브라우저 새로 고침</span><span class="sxs-lookup"><span data-stu-id="dd316-111">Browser Refresh</span></span>

<span data-ttu-id="dd316-112">브라우저 새로 고침와 브라우저 링크를 통해 Visual Studio에 연결 되어 있는 여러 브라우저를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="dd316-113">브라우저 새로 고침을 사용 하려면 먼저 프로젝트 템플릿 중 하나를 사용 하 여 ASP.NET 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="dd316-114">F5 키를 누르거나 도구 모음에 있는 화살표 아이콘을 클릭 하 여 응용 프로그램을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="dd316-115">디버깅에 대 한 특정 브라우저 선택 드롭다운을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="dd316-116">여러 브라우저를 디버깅 하려면 선택 **브라우저**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="dd316-117">에 **브라우저** 대화 상자에서 둘 이상의 브라우저를 선택 하려면 CTRL 키를 보류 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="dd316-118">클릭 **찾아보기** 선택한 브라우저를 사용 하 여 디버그 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="dd316-119">브라우저 링크는 Visual Studio 외부에서 브라우저를 시작 하 고 응용 프로그램 URL로 이동 하는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="dd316-120">브라우저 링크 컨트롤은 순환 화살표 아이콘으로 드롭다운 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="dd316-121">화살표 아이콘은는 **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="dd316-122">브라우저에서 어떤 연결을 보려면 위로 마우스를 가져가고는 **새로 고침** 디버깅 하는 동안 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="dd316-123">연결 된 브라우저 도구 설명 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="dd316-124">연결 된 브라우저를 새로 고치려면 클릭는 **새로 고침** 단추 또는 CTRL + ALT + ENTER를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="dd316-125">예를 들어 다음 스크린 샷에서 MVC 5 프로젝트 템플릿을 사용 하 여 만든 ASP.NET 프로젝트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="dd316-126">위쪽에서 두 개의 브라우저에서 실행 중인 응용 프로그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="dd316-127">아래쪽에서 프로젝트가 Visual Studio에서 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="dd316-128">변경한 다음 Visual Studio에서의 &lt;h1&gt; 홈 페이지에 대 한 제목:</span><span class="sxs-lookup"><span data-stu-id="dd316-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="dd316-129">클릭 시는 **새로 고침** 단추 변경에서는 브라우저 창에 표시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="dd316-130">**참고**</span><span class="sxs-lookup"><span data-stu-id="dd316-130">**Notes**</span></span>

- <span data-ttu-id="dd316-131">브라우저 링크를 사용 하려면 설정 `debug=true` 에 [ &lt;컴파일&gt; ](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) 프로젝트의 Web.config 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="dd316-132">응용 프로그램은 로컬 호스트에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="dd316-133">응용 프로그램.NET 4.0 이상을 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="dd316-134">브라우저 링크 대시보드 보기</span><span class="sxs-lookup"><span data-stu-id="dd316-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="dd316-135">브라우저 링크 대시보드에 브라우저 링크 연결에 대 한 정보를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="dd316-136">대시보드를 보려면 브라우저 링크 드롭다운 메뉴를 선택 (옆에 있는 작은 화살표는 **새로 고침** 단추).</span><span class="sxs-lookup"><span data-stu-id="dd316-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="dd316-137">클릭 **브라우저 링크 대시보드에**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="dd316-138">대시보드는 연결 된 브라우저와 각 브라우저가 탐색 하는 URL을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="dd316-139">**필수 구성 요소** 섹션에서는 해당 프로젝트에 대 한 브라우저 링크를 사용 하는 데 필요한 모든 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="dd316-140">예를 들어 다음 스크린샷은 프로젝트 "debug" 설정 되어 있는 false로 Web.config 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="dd316-141">정적 HTML 파일에 대 한 브라우저 링크를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="dd316-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="dd316-142">브라우저 링크에 정적 HTML 파일을 사용 하려면 다음 Web.config 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="dd316-143">성능상의 이유로 프로젝트를 게시할 때이 설정을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="dd316-144">브라우저 링크를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="dd316-144">Disabling Browser Link</span></span>

<span data-ttu-id="dd316-145">브라우저 링크는 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="dd316-146">여러 가지 방법으로 사용 하지 않도록.</span><span class="sxs-lookup"><span data-stu-id="dd316-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="dd316-147">브라우저 링크 드롭다운 메뉴에서의 선택을 취소 **브라우저 링크를 사용 하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="dd316-148">Web.config 파일에서 "vs: EnableBrowserLink"와 "false" 값 appSettings 섹션에서 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="dd316-149">Web.config 파일에 디버그를 false로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="dd316-150">어떻게 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="dd316-150">How Does It Work?</span></span>

<span data-ttu-id="dd316-151">브라우저 링크를 사용 하 여 [SignalR](../../../signalr/index.md) Visual Studio 및 브라우저 간 통신 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="dd316-152">브라우저 링크를 사용 하는 Visual Studio는 여러 명의 클라이언트 (브라우저)에 연결할 수 있는 SignalR 서버로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="dd316-153">브라우저 링크는 또한 asp.net HTTP 모듈을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="dd316-154">이 모듈에는 특수 삽입 합니다. &lt;스크립트&gt; 서버에서 모든 페이지 요청에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="dd316-155">브라우저에서 "소스 보기"를 선택 하 여 스크립트 참조를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="dd316-156">소스 파일을 수정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-156">Your source files are not modified.</span></span> <span data-ttu-id="dd316-157">HTTP 모듈 스크립트 참조를 동적으로 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="dd316-158">모든 브라우저에서 작동 하는 모든 JavaScript 브라우저 쪽 코드 이므로 [SignalR 지원](../../../signalr/overview/getting-started/supported-platforms.md), 모든 브라우저 플러그 인을 요구 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd316-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
