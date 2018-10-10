---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: '자습서: 고주파수 SignalR 2 사용 하 여 | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR을 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 빈도가 높은 메시징에 중...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 23dc9cc7fd469e934ed9915922a3baa772d9e1ab
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912035"
---
<a name="tutorial-high-frequency-realtime-with-signalr-2"></a><span data-ttu-id="9327f-104">자습서: 고주파수 SignalR 2 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9327f-104">Tutorial: High-Frequency Realtime with SignalR 2</span></span>
====================
<span data-ttu-id="9327f-105">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="9327f-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[<span data-ttu-id="9327f-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="9327f-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

> <span data-ttu-id="9327f-107">이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR 2를 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-107">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="9327f-108">이 경우 고정 된 요금이; 전송 되는 업데이트를 의미 빈도가 높은 메시징 이 응용 프로그램의 경우 최대 10 개까지 두 번째를 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-108">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
>
> <span data-ttu-id="9327f-109">이 자습서에서 만드는 응용 프로그램 사용자 끌 수 있는 셰이프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-109">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="9327f-110">연결 된 다른 모든 브라우저에서 모양의 위치 다음의 업데이트를 사용 하 여 끌어 온 모양의 위치와 일치 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-110">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
>
> <span data-ttu-id="9327f-111">이 자습서에 도입 된 개념 실시간 게임에서 응용 프로그램 및 다른 시뮬레이션 응용 프로그램을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-111">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9327f-112">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="9327f-112">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="9327f-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9327f-113">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="9327f-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9327f-114">.NET 4.5</span></span>
> - <span data-ttu-id="9327f-115">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="9327f-115">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="9327f-116">이 자습서를 사용 하 여 Visual Studio 2012를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9327f-116">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="9327f-117">이 자습서를 사용 하 여 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-117">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="9327f-118">업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 최신 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-118">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="9327f-119">설치 합니다 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-119">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="9327f-120">웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-120">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="9327f-121">SignalR 클래스에 대 한 Visual Studio 템플릿 같은 설치 합니다 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-121">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="9327f-122">일부 템플릿 (와 같은 **OWIN 시작 클래스**)를 사용할 수 없습니다;이 대 한 클래스 파일을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-122">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="9327f-123">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="9327f-123">Tutorial Versions</span></span>
>
> <span data-ttu-id="9327f-124">이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-124">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="9327f-125">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="9327f-125">Questions and comments</span></span>
>
> <span data-ttu-id="9327f-126">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="9327f-126">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="9327f-127">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-127">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="9327f-128">개요</span><span class="sxs-lookup"><span data-stu-id="9327f-128">Overview</span></span>

<span data-ttu-id="9327f-129">이 자습서에는 실시간으로 다른 브라우저를 사용 하 여 개체의 상태를 공유 하는 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-129">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="9327f-130">응용 프로그램 만들겠습니다 MoveShape 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-130">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="9327f-131">MoveShape 페이지는 다음을 끌 수 있습니다; HTML Div 요소가 표시 됩니다. Div를 끌 때 새 위치로 연결 된 다른 모든 클라이언트에 맞게 도형의 위치를 업데이트 하려면 다음 알려 서버로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-131">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="9327f-133">이 자습서에서 만든 응용 프로그램은 Damian edwards의 데모를 기반으로 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-133">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="9327f-134">이 데모를 포함 하는 비디오를 볼 수 있습니다 [여기](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-134">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="9327f-135">이 자습서는 셰이프를 끌 때 발생 하는 각 이벤트에서 SignalR 메시지를 보내는 방법을 보여 줍니다 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-135">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="9327f-136">연결 된 각 클라이언트가 모양의 로컬 버전의 위치는 메시지가 수신 될 때마다 업데이트 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-136">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="9327f-137">이 메서드를 사용 하 여 응용 프로그램 작동을 하는 동안 이것이 권장 되는 프로그래밍 모델을 클라이언트와 서버가 메시지를 사용 하 여 과부하가 가져올 수 없습니다 하 고 성능 저하는 보낸 시작 메시지의 수에 제한이 없어집니다 것 이므로 .</span><span class="sxs-lookup"><span data-stu-id="9327f-137">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="9327f-138">각 새 위치에 원활 하 게 이동 하는 대신 각 메서드에서 셰이프를 즉시 이동은 연결이 끊긴 클라이언트에 표시 된 애니메이션도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-138">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="9327f-139">자습서의 뒷부분에 나오는 섹션에서는 클라이언트 또는 서버에서 메시지가 전송 되는 최대 속도 제한 하는 타이머 함수를 만드는 방법 및 셰이프를 위치 간에 원활 하 게 이동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-139">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="9327f-140">이 자습서에서 만든 응용 프로그램의 최종 버전에서 다운로드할 수 있습니다 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-140">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a).</span></span>

<span data-ttu-id="9327f-141">이 자습서는 다음 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-141">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="9327f-142">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9327f-142">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="9327f-143">프로젝트를 만들고 SignalR 및 JQuery.UI NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="9327f-143">Create the project and add the SignalR and JQuery.UI NuGet package</span></span>](#createtheproject2013)
- [<span data-ttu-id="9327f-144">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9327f-144">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="9327f-145">허브를 시작 하면 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="9327f-145">Starting the hub when the application starts</span></span>](#startup2013)
- [<span data-ttu-id="9327f-146">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="9327f-146">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="9327f-147">서버 루프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-147">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="9327f-148">클라이언트에서 부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="9327f-148">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="9327f-149">추가 단계</span><span class="sxs-lookup"><span data-stu-id="9327f-149">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="9327f-150">전제 조건</span><span class="sxs-lookup"><span data-stu-id="9327f-150">Prerequisites</span></span>

<span data-ttu-id="9327f-151">이 자습서에는 Visual Studio 2013에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-151">This tutorial requires Visual Studio 2013.</span></span>

<a id="createtheproject2013"></a>

## <a name="create-the-project-and-add-the-signalr-and-jqueryui-nuget-package"></a><span data-ttu-id="9327f-152">프로젝트를 만들고 SignalR 및 JQuery.UI NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="9327f-152">Create the project and add the SignalR and JQuery.UI NuGet package</span></span>

<span data-ttu-id="9327f-153">이 섹션에서는 Visual Studio 2013에서 프로젝트를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-153">In this section, we'll create the project in Visual Studio 2013.</span></span>

<span data-ttu-id="9327f-154">다음 단계를 ASP.NET 빈 웹 응용 프로그램을 만들고 SignalR 및 jQuery.UI 라이브러리를 추가 하려면 Visual Studio 2013을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-154">The following steps use Visual Studio 2013 to create an ASP.NET Empty Web Application and add the SignalR and jQuery.UI libraries:</span></span>

1. <span data-ttu-id="9327f-155">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-155">In Visual Studio create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)
2. <span data-ttu-id="9327f-157">에 **새 ASP.NET 프로젝트** 둡니다 창 **빈** 선택 하 고 클릭 **프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-157">In the **New ASP.NET Project** window, leave **Empty** selected and click **Create Project**.</span></span>

    ![빈 웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
3. <span data-ttu-id="9327f-159">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭을 **추가 | SignalR 허브 클래스 (v2)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-159">In **Solution Explorer**, right-click the project, select **Add | SignalR Hub Class (v2)**.</span></span> <span data-ttu-id="9327f-160">클래스의 이름을 **MoveShapeHub.cs** 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-160">Name the class **MoveShapeHub.cs** and add it to the project.</span></span> <span data-ttu-id="9327f-161">이 단계에서는 합니다 **MoveShapeHub** 클래스 및 스크립트 파일 및 SignalR을 지 원하는 어셈블리 참조의 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-161">This step creates the **MoveShapeHub** class and adds to the project a set of script files and assembly references that support SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9327f-162">클릭 하 여 프로젝트에 SignalR을 추가할 수도 있습니다 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 및 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-162">You can also add SignalR to a project by clicking **Tools > NuGet Package Manager > Package Manager Console** and running a command:</span></span>

    <span data-ttu-id="9327f-163">`install-package Microsoft.AspNet.SignalR`.</span><span class="sxs-lookup"><span data-stu-id="9327f-163">`install-package Microsoft.AspNet.SignalR`.</span></span>

    <span data-ttu-id="9327f-164">SignalR을 추가 하려면 콘솔을 사용 하는 경우는 SignalR을 추가한 후 별도 단계로 SignalR 허브 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-164">If you use the console to add SignalR, create the SignalR hub class as a separate step after you add SignalR.</span></span>
4. <span data-ttu-id="9327f-165">클릭 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-165">Click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="9327f-166">패키지 관리자 창에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-166">In the package manager window, run the following command:</span></span>

    `Install-Package jQuery.UI.Combined`

    <span data-ttu-id="9327f-167">도형에 애니메이션 효과를 사용 하는 jQuery UI 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-167">This installs the jQuery UI library, which you'll use to animate the shape.</span></span>
5. <span data-ttu-id="9327f-168">**솔루션 탐색기** 스크립트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-168">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="9327f-169">JQuery, jQueryUI, 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-169">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

    ![스크립트 라이브러리 참조](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="9327f-171">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9327f-171">Create the base application</span></span>

<span data-ttu-id="9327f-172">이 섹션에서는 각 마우스 이동 이벤트 동안 모양의 위치 서버로 전송 하는 브라우저 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-172">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="9327f-173">그런 다음 서버를 수신할 때 연결 된 다른 모든 클라이언트에이 정보를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-173">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="9327f-174">이후 섹션에서이 응용 프로그램에서 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-174">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="9327f-175">MoveShapeHub.cs 클래스에서 이미 만든 하지 않은 경우 **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**, **클래스...** . 클래스의 이름을 **MoveShapeHub** 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-175">If you haven't already created the MoveShapeHub.cs class, in **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="9327f-176">새 코드를 바꿉니다 **MoveShapeHub** 다음 코드를 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-176">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="9327f-177">`MoveShapeHub` 위의 클래스는 SignalR 허브의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-177">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="9327f-178">에서처럼 합니다 [SignalR 시작](tutorial-getting-started-with-signalr.md) 자습서에서는 허브에 클라이언트를 직접 호출 하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-178">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="9327f-179">이 경우 클라이언트는 새 포함 된 개체를 보냅니다 서버에 연결 된 다른 모든 클라이언트에 브로드캐스트 가져옵니다 셰이프의 X 및 Y 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-179">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="9327f-180">SignalR은 JSON을 사용 하 여이 개체를 자동으로 직렬화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-180">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="9327f-181">클라이언트에 보낼 개체 (`ShapeModel`) 모양의 위치를 저장 하는 멤버가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-181">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="9327f-182">서버에서 개체의 버전도 멤버를 포함 추적 하는 클라이언트의 데이터가 저장 되 고, 지정된 된 클라이언트는 자체 데이터를 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-182">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="9327f-183">이 멤버를 사용 하는 `JsonIgnore` 특성에서 직렬화 되 고 클라이언트에 전송 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-183">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>

<a id="startup2013"></a>
## <a name="starting-the-hub-when-the-application-starts"></a><span data-ttu-id="9327f-184">허브를 시작 하면 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="9327f-184">Starting the hub when the application starts</span></span>

1. <span data-ttu-id="9327f-185">다음을 시작 하면 응용 프로그램 허브에 대 한 매핑을 설정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-185">Next, we'll set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="9327f-186">SignalR 2에서를 호출 하는 OWIN 시작 클래스를 추가 하면 됩니다 `MapSignalR` 때 startup 클래스 `Configuration` OWIN 시작 될 때 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-186">In SignalR 2, this is done by adding an OWIN startup class, which will call `MapSignalR` when the startup class' `Configuration` method is executed when OWIN starts.</span></span> <span data-ttu-id="9327f-187">OWIN의 시작 클래스는 추가 사용 하 여 처리를 `OwinStartup` 어셈블리 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-187">The class is added to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

    <span data-ttu-id="9327f-188">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | OWIN 시작 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-188">In **Solution Explorer**, right-click the project, then click **Add | OWIN Startup Class**.</span></span> <span data-ttu-id="9327f-189">클래스의 이름을 *시동* 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-189">Name the class *Startup* and click **OK**.</span></span>
2. <span data-ttu-id="9327f-190">Startup.cs의 내용을 다음으로 변경:</span><span class="sxs-lookup"><span data-stu-id="9327f-190">Change the contents of Startup.cs to the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<a id="client"></a>
## <a name="adding-the-client"></a><span data-ttu-id="9327f-191">클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="9327f-191">Adding the client</span></span>

1. <span data-ttu-id="9327f-192">다음으로, 클라이언트가 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-192">Next, we'll add the client.</span></span> <span data-ttu-id="9327f-193">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-193">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="9327f-194">에 **새 항목 추가** 대화 상자에서 **Html 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-194">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="9327f-195">페이지의 이름을 **Default.html** 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-195">Name the page **Default.html** and click **Add**.</span></span>
2. <span data-ttu-id="9327f-196">**솔루션 탐색기**방금 만든 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-196">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
3. <span data-ttu-id="9327f-197">다음 코드 조각을 사용 하 여 HTML 페이지의 기본 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-197">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9327f-198">스크립트 참조 Scripts 폴더에서 프로젝트에 추가 하는 패키지에 일치 하는 아래를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-198">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html)]

    <span data-ttu-id="9327f-199">위의 HTML 및 JavaScript 코드 셰이프라고 빨간색 Div 만듭니다, jQuery 라이브러리를 사용 하 여 셰이프 끌기 동작을 사용 하도록 설정 및 셰이프를 사용 하 여 `drag` 도형의 위치 서버로 보낼 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-199">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
4. <span data-ttu-id="9327f-200">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-200">Start the application by pressing F5.</span></span> <span data-ttu-id="9327f-201">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-201">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9327f-202">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-202">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="9327f-204">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="9327f-204">Add the client loop</span></span>

<span data-ttu-id="9327f-205">위치의 모든 마우스 이동 이벤트의 셰이프를 보내는 만들어집니다는 불필요 한 네트워크 트래픽 양, 클라이언트에서 메시지를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-205">Since sending the location of the shape on every mouse move event will create an unneccesary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="9327f-206">Javascript에서는 `setInterval` 고정된 요금으로 서버에 새 위치 정보를 전송 하는 루프를 설정 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-206">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="9327f-207">이 루프는 "게임 루프의" 모든 게임 또는 기타 시뮬레이션의 기능을 구동 하는 반복적으로 호출된 된 함수는 매우 기본적인 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-207">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="9327f-208">다음 코드 조각에 맞게 HTML 페이지에서 클라이언트 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-208">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html)]

    <span data-ttu-id="9327f-209">위의 업데이트 추가 `updateServerModel` 고정된 빈도 호출 되는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-209">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="9327f-210">이 함수는 서버에 위치 데이터를 보냅니다 때마다는 `moved` 플래그 보낼 새 위치 데이터 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-210">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="9327f-211">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-211">Start the application by pressing F5.</span></span> <span data-ttu-id="9327f-212">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9327f-213">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="9327f-214">서버에 전송 된 메시지 수가 제한 됩니다, 되므로 애니메이션 이전 섹션과 원활 하 게 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-214">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="9327f-216">서버 루프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-216">Add the server loop</span></span>

<span data-ttu-id="9327f-217">현재 응용 프로그램에서 클라이언트에 서버에서 보낸 메시지 서 수신 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-217">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="9327f-218">클라이언트에 표시 된 대로 비슷한 문제가 필요한 연결 수 닥 결과적으로 보다 더 자주 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-218">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="9327f-219">이 섹션에는 나가는 메시지의 속도 제한 하는 타이머를 구현 하도록 서버를 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-219">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="9327f-220">내용을 바꿉니다 `MoveShapeHub.cs` 다음 코드 조각을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-220">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="9327f-221">위의 코드를 추가 하려면 클라이언트를 확장 합니다 `Broadcaster` 나가는 제한 하는 클래스를 사용 하 여 메시지를 `Timer` .NET framework 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-221">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="9327f-222">자체 허브 일시적인 이므로 (만든 필요할 때마다)는 `Broadcaster` 단일 항목으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-222">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="9327f-223">(.NET 4에 도입 됨) 하는 초기화 지연 타이머가 시작 되기 전에 첫 번째 인스턴스에 완전히 만들지 보장, 필요할 때까지 생성을 지연 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-223">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="9327f-224">클라이언트에 대 한 호출 `UpdateShape` 함수는 허브의 외부로 이동 후 `UpdateModel` 메서드, 들어오는 메시지를 받을 때마다 즉시에 더 이상 해당 it 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-224">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="9327f-225">초 당 25 호출의 속도로 클라이언트에 메시지를 전송할 대신 관리 하는 `_broadcastLoop` 내에서 타이머를 `Broadcaster` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-225">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="9327f-226">허브에서 직접 클라이언트 메서드를 호출 하는 대신에 마지막으로, 합니다 `Broadcaster` 클래스를 현재 운영 허브에 대 한 참조를 입수해 야 합니다. (`_hubContext`)를 사용 하 여는 `GlobalHost`합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-226">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="9327f-227">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-227">Start the application by pressing F5.</span></span> <span data-ttu-id="9327f-228">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-228">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9327f-229">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-229">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="9327f-230">더 이상 없습니다 브라우저의 이전 섹션에서 차이 볼 수 있지만 클라이언트에 전송 된 메시지 수가 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-230">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="9327f-232">클라이언트에서 부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="9327f-232">Add smooth animation on the client</span></span>

<span data-ttu-id="9327f-233">응용 프로그램은 거의 완료 하지만 한 가지 자세한 개선, 클라이언트의 모양 동작 서버 메시지에 대 한 응답으로 이동할 때 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-233">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="9327f-234">서버에서 지정 된 새 위치로 모양의 위치를 설정 하는 대신 JQuery UI 라이브러리의 사용 `animate` 현재 및 새 위치로 간에 셰이프를 원활 하 게 이동 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-234">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="9327f-235">클라이언트의 업데이트 `updateShape` 검색할 메서드 같은 아래 강조 표시 된 코드:</span><span class="sxs-lookup"><span data-stu-id="9327f-235">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

    <span data-ttu-id="9327f-236">위의 코드를 새 것 (이 예제의 경우 100 밀리초)에 애니메이션 간격에 걸쳐 서버에서 지정 된 이전 위치에서 셰이프를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-236">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="9327f-237">새 애니메이션을 시작 하기 전에 셰이프를 실행 하는 모든 이전 애니메이션이 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-237">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="9327f-238">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-238">Start the application by pressing F5.</span></span> <span data-ttu-id="9327f-239">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-239">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="9327f-240">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-240">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="9327f-241">다른 창에서 모양 이동 들어오는 메시지당 한 번 설정 하는 것이 아니라 시간 위로 이동을 보간 되는 대로 작은 불규칙적인 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-241">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image8.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="9327f-243">추가 단계</span><span class="sxs-lookup"><span data-stu-id="9327f-243">Further Steps</span></span>

<span data-ttu-id="9327f-244">이 자습서에서는 클라이언트와 서버 간의 빈도가 높은 메시지를 보내는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-244">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="9327f-245">이 통신 패러다임은 온라인 게임 및 다른 시뮬레이션와 같은 개발 하기 위한 유용한 [SignalR을 사용 하 여 만든 ShootR 게임](https://shootr.azurewebsites.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-245">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="9327f-246">이 자습서에서 만든 전체 응용 프로그램에서 다운로드할 수 있습니다 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-246">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a).</span></span>

<span data-ttu-id="9327f-247">SignalR 개발 개념에 대 한 자세한 내용은 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9327f-247">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="9327f-248">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="9327f-248">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="9327f-249">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="9327f-249">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="9327f-250">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="9327f-250">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

<span data-ttu-id="9327f-251">Azure SignalR 응용 프로그램을 배포 하는 방법은 연습을 참조 하세요 [Azure App Service에서 Web apps를 사용 하 여 SignalR](../deployment/using-signalr-with-azure-web-sites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-251">For a walkthrough on how to deploy a SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="9327f-252">Visual Studio 웹 프로젝트를 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9327f-252">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
