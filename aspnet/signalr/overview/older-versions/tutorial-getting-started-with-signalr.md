---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: "자습서: SignalR 시작 1.x | Microsoft Docs"
author: pfletcher
description: "ASP.NET SignalR을 사용 하 여 HTML 페이지에 실시간 채팅 응용 프로그램을 빌드합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: ce4953a0abf64af28ef4dbc5a62bb2d989343d99
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="71a55-103">자습서: SignalR 시작 1.x</span><span class="sxs-lookup"><span data-stu-id="71a55-103">Tutorial: Getting Started with SignalR 1.x</span></span>
====================
<span data-ttu-id="71a55-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="71a55-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

> <span data-ttu-id="71a55-105">이 자습서에는 SignalR을 사용하여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="71a55-106">SignalR 빈 ASP.NET 웹 응용 프로그램에 추가 되며를 보내고 메시지를 표시 합니다. HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>


## <a name="overview"></a><span data-ttu-id="71a55-107">개요</span><span class="sxs-lookup"><span data-stu-id="71a55-107">Overview</span></span>

<span data-ttu-id="71a55-108">이 자습서에서는 간단한 브라우저 기반 채팅 응용 프로그램을 빌드하는 방법을 보여 SignalR 개발을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="71a55-109">빈 ASP.NET 웹 응용 프로그램에 SignalR 라이브러리를 추가, 메시지를 보내는 클라이언트에 허브 클래스 만들고 사용자가 채팅 메시지를 주고받을 수 있는 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="71a55-110">MVC 뷰를 사용 하 여 MVC 4의 채팅 응용 프로그램을 만드는 방법을 보여 주는 유사한 자습서를 참조 하십시오. [SignalR 및 MVC 4 시작](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="71a55-111">이 자습서에서는 SignalR의 릴리스 (1.x) 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="71a55-112">SignalR 간의 변경 사항에 대 한 자세한 내용은 1.x 및 2.0의 경우 참조 [업그레이드 SignalR 1.x 프로젝트](../releases/upgrading-signalr-1x-projects-to-20.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="71a55-113">SignalR은 오픈 소스.NET 라이브러리를 사용 하 여 실시간 사용자 조작 또는 실시간 데이터 업데이트를 필요로 하는 웹 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="71a55-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="71a55-114">소셜 응용 프로그램, 다중 사용자 게임, 비즈니스 공동 작업 및 뉴스, 날씨, 또는 재무 업데이트 응용 프로그램을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="71a55-115">이러한 실시간 응용 프로그램 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-115">These are often called real-time applications.</span></span>

<span data-ttu-id="71a55-116">SignalR의 실시간 응용 프로그램을 작성 과정을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="71a55-117">ASP.NET 서버 라이브러리와 클라이언트 및 서버 연결을 관리 하 고 클라이언트에 대 한 푸시의 콘텐츠 업데이트를 쉽게 수행할 수 있도록 JavaScript 클라이언트 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="71a55-118">SignalR 라이브러리 실시간 기능을 사용 하려면 기존 ASP.NET 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="71a55-119">이 자습서에서는 다음 SignalR 개발 작업:</span><span class="sxs-lookup"><span data-stu-id="71a55-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="71a55-120">ASP.NET 웹 응용 프로그램에 SignalR 라이브러리에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="71a55-121">클라이언트에 콘텐츠를 푸시 하려면 허브 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="71a55-122">웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="71a55-123">다음 스크린 샷에서 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="71a55-124">새 사용자가 의견을 게시 하 고 추가한 사용자의 채팅에 가입한 후 메모를 참조 수입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![채팅 인스턴스](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="71a55-126">섹션:</span><span class="sxs-lookup"><span data-stu-id="71a55-126">Sections:</span></span>

- [<span data-ttu-id="71a55-127">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="71a55-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="71a55-128">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="71a55-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="71a55-129">코드 검사</span><span class="sxs-lookup"><span data-stu-id="71a55-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="71a55-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71a55-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="71a55-131">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="71a55-131">Set up the Project</span></span>

<span data-ttu-id="71a55-132">이 섹션에는 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다 SignalR에 더하고 채팅 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="71a55-133">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="71a55-133">Prerequisites:</span></span>

- <span data-ttu-id="71a55-134">Visual Studio 2010 SP1 또는 2012입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="71a55-135">Visual Studio가 참조 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2012 Express 개발 도구를 얻으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="71a55-136">[Microsoft ASP.NET 및 웹 도구 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="71a55-137">Visual Studio 2012에 대 한이 설치 관리자는 Visual Studio로 SignalR 템플릿을 포함 하는 새로운 ASP.NET 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="71a55-138">Visual Studio 2010 s p 1에 대 한 설치 관리자를 사용할 수 있지만 설치 단계에 설명 된 대로 SignalR NuGet 패키지를 설치 하 여이 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="71a55-139">Visual Studio 2012를 사용 하 여 ASP.NET 빈 웹 응용 프로그램을 만들고 SignalR 라이브러리를 추가 하는 다음 단계:</span><span class="sxs-lookup"><span data-stu-id="71a55-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="71a55-140">Visual Studio에서 ASP.NET 빈 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![빈 웹 만들기](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="71a55-142">열기는 **패키지 관리자 콘솔** 선택 하 여 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-142">Open the **Package Manager Console** by selecting **Tools | Library Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="71a55-143">콘솔 창에 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="71a55-144">이 명령은 설치에서 최신 버전의 SignalR 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="71a55-145">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 선택 **추가 | 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="71a55-146">클래스의 새 이름을 **ChatHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="71a55-147">**솔루션 탐색기** 스크립트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="71a55-148">JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![라이브러리 참조](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="71a55-150">코드는 **ChatHub** 를 다음 코드로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="71a55-151">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가 | 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="71a55-152">에 **새 항목 추가** 대화 상자에서 **전역 응용 프로그램 클래스** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![전역 추가](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="71a55-154">다음 추가 `using` 제공 된 다음 문이 `using` Global.asax.cs 클래스에는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="71a55-155">코드의 다음 줄 추가 `Application_Start` SignalR 허브에 대 한 기본 경로 등록 하려면 글로벌 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="71a55-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="71a55-156">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가 | 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="71a55-157">에 **새 항목 추가** 대화 상자, Html 페이지 선택 및 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="71a55-158">**솔루션 탐색기**방금 만든 HTML 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="71a55-159">HTML 페이지의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="71a55-160">**모두 저장** 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="71a55-161">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="71a55-161">Run the Sample</span></span>

1. <span data-ttu-id="71a55-162">F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="71a55-163">HTML 페이지를 사용자 이름에 대 한 프롬프트 및 브라우저 인스턴스를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="71a55-165">사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-165">Enter a user name.</span></span>
3. <span data-ttu-id="71a55-166">브라우저의 주소 표시줄에서 URL을 복사 하 고 두 인스턴스를 열어 자세한 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="71a55-167">각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="71a55-168">각 브라우저 인스턴스에서 주석을 추가 하 고 클릭 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="71a55-169">모든 브라우저 인스턴스에 주석을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71a55-170">이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="71a55-171">허브 모든 현재 사용자에 게 의견을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="71a55-172">사용자에 게 채팅을 나중에 조인에 참여할 때부터 추가 된 메시지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="71a55-173">다음 스크린 샷에서 한 인스턴스 메시지를 보낼 때 업데이트 됩니다 인 모든 브라우저 인스턴스 3 개에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![채팅 브라우저](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="71a55-175">**솔루션 탐색기**, 검사는 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="71a55-176">라는 스크립트 파일이 **허브** SignalR 라이브러리를 런타임에 동적으로 생성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="71a55-177">이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="71a55-179">코드 검사</span><span class="sxs-lookup"><span data-stu-id="71a55-179">Examine the Code</span></span>

<span data-ttu-id="71a55-180">SignalR 채팅 응용 프로그램에서는 두 가지 기본 SignalR 개발 작업: 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 주고받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="71a55-181">SignalR 허브</span><span class="sxs-lookup"><span data-stu-id="71a55-181">SignalR Hubs</span></span>

<span data-ttu-id="71a55-182">코드 예제에서는 **ChatHub** 클래스에서 파생 되는 **Microsoft.AspNet.SignalR.Hub** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="71a55-183">파생 되는 **허브** 클래스는 SignalR 응용 프로그램을 작성 하는 유용한 방법은 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="71a55-184">허브 클래스에 공용 메서드를 만들고 그런 다음 웹 페이지의 jQuery 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="71a55-185">클라이언트 채팅 코드에서 호출할는 **ChatHub.Send** 메서드 새 메시지를 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="71a55-186">허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 **Clients.All.broadcastMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="71a55-187">**보낼** 메서드 여러 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="71a55-188">클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="71a55-189">사용 하 여는 **Microsoft.AspNet.SignalR.Hub.Clients** 이 허브에 연결 된 동적 속성을 모든 클라이언트에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="71a55-190">클라이언트에서 jQuery 함수 호출 (예:는 `broadcastMessage` 함수) 클라이언트를 업데이트 하려면.</span><span class="sxs-lookup"><span data-stu-id="71a55-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="71a55-191">SignalR 및 jQuery</span><span class="sxs-lookup"><span data-stu-id="71a55-191">SignalR and jQuery</span></span>

<span data-ttu-id="71a55-192">코드 샘플에서 HTML 페이지에는 SignalR 허브와 통신 하는 SignalR jQuery 라이브러리를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="71a55-193">필수 작업 코드에 대 한 프록시 서버를 클라이언트에 대 한 밀어넣기 콘텐츠를 호출할 수 있는 함수를 선언 하 고 연결을 시작 하는 허브에 메시지를 보낼 허브 참조를 선언 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="71a55-194">다음 코드를 허브에 대 한 프록시를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="71a55-195">JQuery 서버 클래스 및 해당 멤버에 대 한 참조에서 카멜식 대/소문자는입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="71a55-196">코드 샘플 참조는 C# **ChatHub** 으로 jQuery 클래스 **chatHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>


<span data-ttu-id="71a55-197">다음 코드는 스크립트에 콜백 함수를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="71a55-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="71a55-198">서버에서 허브 클래스에는 각 클라이언트에 콘텐츠 업데이트 적용 하려면이 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="71a55-199">HTML을 표시 하기 전에 콘텐츠를 인코딩하는 두 줄은 선택 사항이 며 스크립트 삽입을 방지 하는 간단한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="71a55-200">다음 코드에는 허브에 대 한 연결을 여는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="71a55-201">연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 하는 코드는 **보낼** HTML 페이지에는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="71a55-202">이 방법은 이벤트 처리기 실행 되기 전에 연결이 설정 된 시나리오.</span><span class="sxs-lookup"><span data-stu-id="71a55-202">This approach insures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="71a55-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71a55-203">Next Steps</span></span>

<span data-ttu-id="71a55-204">SignalR은 실시간 웹 응용 프로그램을 구축 하기 위한 프레임 워크는 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="71a55-205">여러 가지 SignalR 개발 작업에 배웠습니다: SignalR ASP.NET 응용 프로그램에 추가 하는 방법, 허브 클래스를 만드는 방법 및 보내고 허브에서 메시지를 수신 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="71a55-206">사용할 수 있습니다 샘플 응용 프로그램이이 자습서 또는 다른 SignalR 응용 프로그램에서 인터넷을 통해 호스팅 공급자에이 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="71a55-207">Microsoft에서 제공 하는 최대 10 개의 웹 사이트를 무료의 무료 웹 호스팅 [Windows Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="71a55-208">샘플 SignalR 응용 프로그램을 배포 하는 방법에 대 한 연습을을 참조 하십시오. [는 SignalR Getting Started 샘플으로 Windows Azure 웹 사이트 게시](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="71a55-209">Visual Studio 웹 프로젝트는 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Windows Azure 웹 사이트에 ASP.NET 응용 프로그램 배포](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="71a55-210">(참고: WebSocket 전송 Windows Azure 웹 사이트에 대 한 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71a55-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="71a55-211">SignalR의 전송 섹션에 설명 된 대로 다른 사용 가능한 전송 사용 하 여 때 WebSocket 전송에 사용할 수 없으면는 [SignalR 항목 소개](index.md).)</span><span class="sxs-lookup"><span data-stu-id="71a55-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="71a55-212">SignalR 개발 보다 발전된 된 개념을 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="71a55-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="71a55-213">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="71a55-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="71a55-214">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="71a55-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="71a55-215">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="71a55-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
