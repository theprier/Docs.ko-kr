---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: "자습서: 2 SignalR 시작 | Microsoft Docs"
author: pfletcher
description: "이 자습서에는 SignalR을 사용하여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 하 고 HTML pa를 만드는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 3bec32b9b21325cde461541d7a313f401a0cfce7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="tutorial-getting-started-with-signalr-2"></a><span data-ttu-id="2c92c-104">자습서: 2 SignalR 시작</span><span class="sxs-lookup"><span data-stu-id="2c92c-104">Tutorial: Getting Started with SignalR 2</span></span>
====================
<span data-ttu-id="2c92c-105">으로 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="2c92c-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[<span data-ttu-id="2c92c-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

> <span data-ttu-id="2c92c-107">이 자습서에는 SignalR을 사용하여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-107">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="2c92c-108">SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 되며를 보내고 메시지를 표시 합니다. HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-108">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span> 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2c92c-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2c92c-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="2c92c-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2c92c-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="2c92c-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2c92c-111">.NET 4.5</span></span>
> - <span data-ttu-id="2c92c-112">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="2c92c-112">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="2c92c-113">이 자습서와 함께 Visual Studio 2012를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2c92c-113">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="2c92c-114">이 자습서와 함께 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-114">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="2c92c-115">업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 를 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-115">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="2c92c-116">설치는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-116">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="2c92c-117">웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-117">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="2c92c-118">SignalR 클래스에 대 한 Visual Studio 템플릿을와 같은 설치 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-118">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="2c92c-119">일부 서식 파일 (와 같은 **OWIN 시작 클래스**)은 사용할 수 없습니다; 이러한 경우에 대 한 클래스 파일을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-119">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="2c92c-120">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="2c92c-120">Tutorial versions</span></span>
> 
> <span data-ttu-id="2c92c-121">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-121">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="2c92c-122">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="2c92c-122">Questions and comments</span></span>
> 
> <span data-ttu-id="2c92c-123">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="2c92c-123">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2c92c-124">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-124">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="2c92c-125">개요</span><span class="sxs-lookup"><span data-stu-id="2c92c-125">Overview</span></span>

<span data-ttu-id="2c92c-126">이 자습서에서는 간단한 브라우저 기반 채팅 응용 프로그램을 빌드하는 방법을 보여 SignalR 개발을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-126">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="2c92c-127">빈 ASP.NET 웹 응용 프로그램에 SignalR 라이브러리를 추가, 메시지를 보내는 클라이언트에 허브 클래스 만들고 사용자가 채팅 메시지를 주고받을 수 있는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-127">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="2c92c-128">MVC 뷰를 사용 하 여 MVC 5에서 채팅 응용 프로그램을 만드는 방법을 보여 주는 유사한 자습서를 참조 하십시오. [SignalR 2 및 MVC 5 시작](tutorial-getting-started-with-signalr-and-mvc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-128">For a similar tutorial that shows how to create a chat application in MVC 5 using an MVC view, see [Getting Started with SignalR 2 and MVC 5](tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2c92c-129">이 자습서에서는 버전 2에서에서 SignalR 응용 프로그램을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-129">This tutorial demonstrates how to create SignalR applications in version 2.</span></span> <span data-ttu-id="2c92c-130">SignalR 간의 변경 사항에 대 한 자세한 내용은 1.x와 2, 참조 [업그레이드 SignalR 1.x 프로젝트](../releases/upgrading-signalr-1x-projects-to-20.md) 및 [Visual Studio 2013 릴리스 정보](../../../visual-studio/overview/2013/release-notes.md#TOC13)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-130">For details on changes between SignalR 1.x and 2, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md) and [Visual Studio 2013 Release Notes](../../../visual-studio/overview/2013/release-notes.md#TOC13).</span></span>

<span data-ttu-id="2c92c-131">SignalR은 오픈 소스.NET 라이브러리를 사용 하 여 실시간 사용자 조작 또는 실시간 데이터 업데이트를 필요로 하는 웹 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="2c92c-131">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="2c92c-132">소셜 응용 프로그램, 다중 사용자 게임, 비즈니스 공동 작업 및 뉴스, 날씨, 또는 재무 업데이트 응용 프로그램을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-132">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="2c92c-133">이러한 실시간 응용 프로그램 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-133">These are often called real-time applications.</span></span>

<span data-ttu-id="2c92c-134">SignalR의 실시간 응용 프로그램을 작성 과정을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-134">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="2c92c-135">ASP.NET 서버 라이브러리와 클라이언트 및 서버 연결을 관리 하 고 클라이언트에 대 한 푸시의 콘텐츠 업데이트를 쉽게 수행할 수 있도록 JavaScript 클라이언트 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-135">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="2c92c-136">SignalR 라이브러리 실시간 기능을 사용 하려면 기존 ASP.NET 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-136">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="2c92c-137">이 자습서에서는 다음 SignalR 개발 작업:</span><span class="sxs-lookup"><span data-stu-id="2c92c-137">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="2c92c-138">ASP.NET 웹 응용 프로그램에 SignalR 라이브러리에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-138">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="2c92c-139">클라이언트에 콘텐츠를 푸시 하려면 허브 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-139">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="2c92c-140">응용 프로그램을 구성 하는 OWIN 시작 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-140">Creating an OWIN startup class to configure the application.</span></span>
- <span data-ttu-id="2c92c-141">웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-141">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="2c92c-142">다음 스크린 샷에서 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-142">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="2c92c-143">새 사용자가 의견을 게시 하 고 추가한 사용자의 채팅에 가입한 후 메모를 참조 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-143">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![채팅 인스턴스](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="2c92c-145">섹션:</span><span class="sxs-lookup"><span data-stu-id="2c92c-145">Sections:</span></span>

- [<span data-ttu-id="2c92c-146">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="2c92c-146">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="2c92c-147">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="2c92c-147">Run the Sample</span></span>](#run)
- [<span data-ttu-id="2c92c-148">코드 검사</span><span class="sxs-lookup"><span data-stu-id="2c92c-148">Examine the Code</span></span>](#code)
- [<span data-ttu-id="2c92c-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c92c-149">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="2c92c-150">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="2c92c-150">Set up the Project</span></span>

<span data-ttu-id="2c92c-151">이 섹션에서는 빈 ASP.NET 웹 응용 프로그램을 만들려면 Visual Studio 2013과 SignalR 버전 2 사용 하는 방법을 추가 SignalR에 하 고 채팅 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-151">This section shows how to use Visual Studio 2013 and SignalR version 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="2c92c-152">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="2c92c-152">Prerequisites:</span></span>

- <span data-ttu-id="2c92c-153">Visual Studio 2013입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-153">Visual Studio 2013.</span></span> <span data-ttu-id="2c92c-154">Visual Studio가 참조 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2013 Express 개발 도구를 얻으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-154">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express Development Tool.</span></span>

<span data-ttu-id="2c92c-155">다음 단계는 ASP.NET 빈 웹 응용 프로그램을 만들고 SignalR 라이브러리를 추가 Visual Studio 2013을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-155">The following steps use Visual Studio 2013 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="2c92c-156">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-156">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="2c92c-158">에 **새 ASP.NET 프로젝트** 창 leave **빈** 선택한 클릭 **프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-158">In the **New ASP.NET Project** window, leave **Empty** selected and click **Create Project**.</span></span>

    ![빈 웹 만들기](tutorial-getting-started-with-signalr/_static/image3.png)
3. <span data-ttu-id="2c92c-160">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 선택 **추가 | SignalR 허브 클래스 (v2)**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-160">In **Solution Explorer**, right-click the project, select **Add | SignalR Hub Class (v2)**.</span></span> <span data-ttu-id="2c92c-161">클래스의 이름을 **ChatHub.cs** 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-161">Name the class **ChatHub.cs** and add it to the project.</span></span> <span data-ttu-id="2c92c-162">이 단계에서는 **ChatHub** 클래스 및 스크립트 파일 및 SignalR을 지 원하는 어셈블리 참조의 집합을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-162">This step creates the **ChatHub** class and adds to the project a set of script files and assembly references that support SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c92c-163">열어 SignalR 프로젝트에 추가할 수도 있습니다는 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔** 하 고 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-163">You can also add SignalR to a project by opening the **Tools | Library Package Manager | Package Manager Console** and running a command:</span></span>

    `install-package Microsoft.AspNet.SignalR`

    <span data-ttu-id="2c92c-164">SignalR을 추가 하 고 콘솔을 사용 하는 경우는 SignalR을 추가한 다음 별도 단계로 SignalR 허브 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-164">If you use the console to add SignalR, create the SignalR hub class as a separate step after you add SignalR.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c92c-165">Visual Studio 2012를 사용 하는 경우는 **SignalR 허브 클래스 (v2)** 템플릿을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-165">If you are using Visual Studio 2012, the **SignalR Hub Class (v2)** template will not be available.</span></span> <span data-ttu-id="2c92c-166">일반을 추가할 수 있습니다 **클래스** 호출 `ChatHub` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-166">You can add a plain **Class** called `ChatHub` instead.</span></span>
4. <span data-ttu-id="2c92c-167">**솔루션 탐색기**, 스크립트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-167">In **Solution Explorer**, expand the Scripts node.</span></span> <span data-ttu-id="2c92c-168">JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-168">Script libraries for jQuery and SignalR are visible in the project.</span></span>
5. <span data-ttu-id="2c92c-169">새 코드를 바꿉니다 **ChatHub** 를 다음 코드로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-169">Replace the code in the new **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="2c92c-170">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가 | OWIN 시작 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-170">In **Solution Explorer**, right-click the project, then click **Add | OWIN Startup Class**.</span></span> <span data-ttu-id="2c92c-171">클래스의 새 이름을 `Startup` 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-171">Name the new class `Startup` and click OK.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c92c-172">Visual Studio 2012를 사용 하는 경우는 **OWIN 시작 클래스** 템플릿을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-172">If you are using Visual Studio 2012, the **OWIN Startup Class** template will not be available.</span></span> <span data-ttu-id="2c92c-173">일반을 추가할 수 있습니다 **클래스** 호출 `Startup` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-173">You can add a plain **Class** called `Startup` instead.</span></span>
7. <span data-ttu-id="2c92c-174">다음에 새 시작 클래스의 콘텐츠를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-174">Change the contents of the new Startup class to the following.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="2c92c-175">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가 | HTML 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-175">In **Solution Explorer**, right-click the project, then click **Add | HTML Page**.</span></span> <span data-ttu-id="2c92c-176">새 페이지 이름을 `index.html`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-176">Name the new page `index.html`.</span></span>
    >[!NOTE]
    ><span data-ttu-id="2c92c-177">SignalR 및 JQuery 라이브러리에 대 한 참조에 대 한 버전 번호를 변경 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-177">You might need to change the version numbers for the references to JQuery and SignalR libraries</span></span>
9. <span data-ttu-id="2c92c-178">**솔루션 탐색기**방금 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-178">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
10. <span data-ttu-id="2c92c-179">HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-179">Replace the default code in the HTML page with the following code.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c92c-180">패키지 관리자에서 SignalR 스크립트의 이후 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-180">A later version of the SignalR scripts may be installed by the package manager.</span></span> <span data-ttu-id="2c92c-181">아래 스크립트 참조 (됩니다 SignalR 허브를 추가 하는 대신 NuGet을 사용 하 여 추가한 경우 다른.) 프로젝트에서 스크립트 파일의 버전에 맞는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2c92c-181">Verify that the script references below correspond to the versions of the script files in the project (they will be different if you added SignalR using NuGet rather than adding a hub.)</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]
11. <span data-ttu-id="2c92c-182">**모두 저장** 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-182">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="2c92c-183">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="2c92c-183">Run the Sample</span></span>

1. <span data-ttu-id="2c92c-184">F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-184">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="2c92c-185">HTML 페이지를 사용자 이름에 대 한 프롬프트 및 브라우저 인스턴스를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-185">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image4.png)
2. <span data-ttu-id="2c92c-187">사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-187">Enter a user name.</span></span>
3. <span data-ttu-id="2c92c-188">브라우저의 주소 표시줄에서 URL을 복사 하 고 두 인스턴스를 열어 자세한 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-188">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="2c92c-189">각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-189">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="2c92c-190">각 브라우저 인스턴스에서 주석을 추가 하 고 클릭 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-190">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="2c92c-191">모든 브라우저 인스턴스에 주석을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-191">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c92c-192">이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-192">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="2c92c-193">허브 모든 현재 사용자에 게 의견을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-193">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="2c92c-194">사용자에 게 채팅을 나중에 조인에 참여할 때부터 추가 된 메시지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-194">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="2c92c-195">다음 스크린 샷에서 한 인스턴스 메시지를 보낼 때 업데이트 됩니다 인 모든 브라우저 인스턴스 3 개에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-195">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![채팅 브라우저](tutorial-getting-started-with-signalr/_static/image5.png)
5. <span data-ttu-id="2c92c-197">**솔루션 탐색기**, 검사는 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-197">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="2c92c-198">라는 스크립트 파일이 **허브** SignalR 라이브러리를 런타임에 동적으로 생성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-198">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="2c92c-199">이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-199">This file manages the communication between jQuery script and server-side code.</span></span>

    ![](tutorial-getting-started-with-signalr/_static/image6.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="2c92c-200">코드 검사</span><span class="sxs-lookup"><span data-stu-id="2c92c-200">Examine the Code</span></span>

<span data-ttu-id="2c92c-201">SignalR 채팅 응용 프로그램에서는 두 가지 기본 SignalR 개발 작업: 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 주고받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-201">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="2c92c-202">SignalR 허브</span><span class="sxs-lookup"><span data-stu-id="2c92c-202">SignalR Hubs</span></span>

<span data-ttu-id="2c92c-203">코드 예제에서는 **ChatHub** 클래스에서 파생 되는 **Microsoft.AspNet.SignalR.Hub** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-203">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="2c92c-204">파생 되는 **허브** 클래스는 SignalR 응용 프로그램을 작성 하는 유용한 방법은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-204">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="2c92c-205">허브 클래스에 공용 메서드를 만들고 그런 다음 웹 페이지의 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-205">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="2c92c-206">클라이언트 채팅 코드에서 호출할는 **ChatHub.Send** 메서드 새 메시지를 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-206">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="2c92c-207">허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 **Clients.All.broadcastMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-207">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="2c92c-208">**보낼** 메서드 여러 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-208">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="2c92c-209">클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-209">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="2c92c-210">사용 하 여는 **Microsoft.AspNet.SignalR.Hub.Clients** 이 허브에 연결 된 동적 속성을 모든 클라이언트에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-210">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="2c92c-211">클라이언트에서 함수를 호출 (예:는 `broadcastMessage` 함수) 클라이언트를 업데이트 하려면.</span><span class="sxs-lookup"><span data-stu-id="2c92c-211">Call a function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="2c92c-212">SignalR 및 jQuery</span><span class="sxs-lookup"><span data-stu-id="2c92c-212">SignalR and jQuery</span></span>

<span data-ttu-id="2c92c-213">코드 샘플에서 HTML 페이지에는 SignalR 허브와 통신 하는 SignalR jQuery 라이브러리를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-213">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="2c92c-214">필수 작업 코드에 대 한 프록시 서버를 클라이언트에 대 한 밀어넣기 콘텐츠를 호출할 수 있는 함수를 선언 하 고 연결을 시작 하는 허브에 메시지를 보낼 허브 참조를 선언 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-214">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="2c92c-215">다음 코드는 허브 프록시에 대 한 참조를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-215">The following code declares a reference to a hub proxy.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="2c92c-216">JavaScript에서 카멜식 대 /에서 서버 클래스 및 해당 멤버에 대 한 참조는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-216">In JavaScript the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="2c92c-217">코드 샘플 참조는 C# **ChatHub** 으로 JavaScript에서 클래스 **chatHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-217">The code sample references the C# **ChatHub** class in JavaScript as **chatHub**.</span></span>


<span data-ttu-id="2c92c-218">다음 코드는 스크립트에 콜백 함수를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="2c92c-218">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="2c92c-219">서버에서 허브 클래스에는 각 클라이언트에 콘텐츠 업데이트 적용 하려면이 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-219">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="2c92c-220">HTML을 표시 하기 전에 콘텐츠를 인코딩하는 두 줄은 선택 사항이 며 스크립트 삽입을 방지 하는 간단한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-220">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="2c92c-221">다음 코드에는 허브에 대 한 연결을 여는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-221">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="2c92c-222">연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 하는 코드는 **보낼** HTML 페이지에는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-222">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="2c92c-223">이 방법을 사용 하면 이벤트 처리기 실행 되기 전에 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-223">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="2c92c-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c92c-224">Next Steps</span></span>

<span data-ttu-id="2c92c-225">SignalR은 실시간 웹 응용 프로그램을 구축 하기 위한 프레임 워크는 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-225">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="2c92c-226">여러 가지 SignalR 개발 작업에 배웠습니다: SignalR ASP.NET 응용 프로그램에 추가 하는 방법, 허브 클래스를 만드는 방법 및 보내고 허브에서 메시지를 수신 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-226">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="2c92c-227">샘플 SignalR 응용 프로그램을 Azure에 배포 하는 방법에 대 한 연습을을 참조 하십시오. [Azure 앱 서비스의 웹 앱과 함께 사용 하 여 SignalR](../deployment/using-signalr-with-azure-web-sites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-227">For a walkthrough on how to deploy the sample SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="2c92c-228">Visual Studio 웹 프로젝트는 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 앱 서비스에서 ASP.NET 웹 앱을 만들](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c92c-228">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<span data-ttu-id="2c92c-229">SignalR 개발 보다 발전된 된 개념을 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2c92c-229">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="2c92c-230">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2c92c-230">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="2c92c-231">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="2c92c-231">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="2c92c-232">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="2c92c-232">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
