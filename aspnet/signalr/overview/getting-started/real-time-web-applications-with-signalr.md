---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: '랩 관련 한 실질적인: SignalR과 실시간 웹 응용 프로그램 | Microsoft Docs'
author: rick-anderson
description: 실시간 웹 응용 프로그램 서버 쪽으로 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠를 기능입니다. ASP는 ASP.NET 개발자를 위한...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 5a2bc120ded18ad2302fd6c5cde65a5323e86ca8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="hands-on-lab-real-time-web-applications-with-signalr"></a><span data-ttu-id="5aae1-104">SignalR과 실습 랩: 실시간 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5aae1-104">Hands On Lab: Real-Time Web Applications with SignalR</span></span>
====================
<span data-ttu-id="5aae1-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="5aae1-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="5aae1-106">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="5aae1-107">실시간 웹 응용 프로그램 서버 쪽으로 실시간으로 발생 하는 대로 연결 된 클라이언트에 콘텐츠를 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-107">Real-time Web applications feature the ability to push server-side content to the connected clients as it happens, in real-time.</span></span> <span data-ttu-id="5aae1-108">ASP.NET 개발자를 위한 **ASP.NET SignalR** 응용 프로그램에 실시간 웹 기능을 추가 하려면 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-108">For ASP.NET developers, **ASP.NET SignalR** is a library to add real-time web functionality to their applications.</span></span> <span data-ttu-id="5aae1-109">이용할 여러 전송의 경우 클라이언트 및 서버의 가장 사용 가능한 전송 가장 사용 가능한 전송을 자동으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-109">It takes advantage of several transports, automatically selecting the best available transport given the client and server's best available transport.</span></span> <span data-ttu-id="5aae1-110">에서는 활용 **WebSocket**, 브라우저와 서버 간의 양방향 통신을 허용 하는 HTML5 API입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-110">It takes advantage of **WebSocket**, an HTML5 API that enables bi-directional communication between the browser and server.</span></span>
> 
> <span data-ttu-id="5aae1-111">**SignalR** 클라이언트 RPC 서버를 수행 하는 데 간단 하 고 상위 수준 API를 제공 (서버 쪽.NET 코드에서 클라이언트의 브라우저에서 JavaScript 함수 호출) 연결 관리에 대 한 유용한 후크를 추가할 뿐 아니라 ASP.NET 응용 프로그램에서 같은 연결/연결 끊기 이벤트, 그룹화 연결 및 권한 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-111">**SignalR** also provides a simple, high-level API for doing server to client RPC (call JavaScript functions in your clients' browsers from server-side .NET code) in your ASP.NET application, as well as adding useful hooks for connection management, such as connect/disconnect events, grouping connections, and authorization.</span></span>
> 
> <span data-ttu-id="5aae1-112">**SignalR** 은 일부 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 전송을 통한 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-112">**SignalR** is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="5aae1-113">A **SignalR** 연결 HTTP로 시작 하 고 다음 수준으로 올린는 **WebSocket** 사용 가능한 경우 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-113">A **SignalR** connection starts as HTTP, and is then promoted to a **WebSocket** connection if available.</span></span> <span data-ttu-id="5aae1-114">**WebSocket** 는 대 한 이상적인 전송 **SignalR**이므로 서버 메모리의 가장 효율적으로 사용 하는 대기 시간이 가장 많고 가장 기본 기능 (클라이언트 간의 양방향 통신 등 및 서버)를 없지만 역시 가장 엄격한 요구 사항: **WebSocket** 서버 수를 사용 하 여를 **Windows Server 2012** 또는 **Windows 8**, 함께**.NET framework 4.5**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-114">**WebSocket** is the ideal transport for **SignalR**, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: **WebSocket** requires the server to be using **Windows Server 2012** or **Windows 8**, along with **.NET Framework 4.5**.</span></span> <span data-ttu-id="5aae1-115">이러한 요구 사항을 충족 되지 않는 경우 **SignalR** 다른 전송의 연결을 사용 하려고 합니다 (같은 *Ajax 긴 폴링과*).</span><span class="sxs-lookup"><span data-stu-id="5aae1-115">If these requirements are not met, **SignalR** will attempt to use other transports to make its connections (like *Ajax long polling*).</span></span>
> 
> <span data-ttu-id="5aae1-116">**SignalR** 클라이언트와 서버 간의 통신을 위해 두 개의 모델을 포함 하는 API: **영구 연결** 및 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-116">The **SignalR** API contains two models for communicating between clients and servers: **Persistent Connections** and **Hubs**.</span></span> <span data-ttu-id="5aae1-117">A **연결** -받는 사람, 단일 그룹화를 보내거나 전체 메시지에 대 한 간단한 끝점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-117">A **Connection** represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="5aae1-118">A **허브** 기반으로 클라이언트와 서버가 서로에서 메서드를 직접 호출할 수 있도록 연결 API 보다 높은 수준의 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="5aae1-118">A **Hub** is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span>
> 
> ![SignalR 아키텍처](real-time-web-applications-with-signalr/_static/image1.png)
> 
> <span data-ttu-id="5aae1-120">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-120">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="5aae1-121">개요</span><span class="sxs-lookup"><span data-stu-id="5aae1-121">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="5aae1-122">목표</span><span class="sxs-lookup"><span data-stu-id="5aae1-122">Objectives</span></span>

<span data-ttu-id="5aae1-123">이 실습 랩에서 배웁니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="5aae1-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="5aae1-124">SignalR을 사용 하 여 클라이언트에 서버에서 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-124">Send notifications from server to client using SignalR.</span></span>
- <span data-ttu-id="5aae1-125">사용 하 여 SignalR 응용 프로그램 확장 **SQL Server**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-125">Scale Out your SignalR application using **SQL Server**.</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="5aae1-126">전제 조건</span><span class="sxs-lookup"><span data-stu-id="5aae1-126">Prerequisites</span></span>

<span data-ttu-id="5aae1-127">다음은이 실습 랩을 완료 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="5aae1-128">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="5aae1-128">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="5aae1-129">설정</span><span class="sxs-lookup"><span data-stu-id="5aae1-129">Setup</span></span>

<span data-ttu-id="5aae1-130">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-130">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="5aae1-131">Windows 탐색기 창을 열고 다음을 찾아보기에 랩 **소스** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-131">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="5aae1-132">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택 **관리자 권한으로 실행** 환경을 구성 되며이 랩에 대 한 Visual Studio 코드 조각을 설치 하는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-132">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="5aae1-133">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-133">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="5aae1-134">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-134">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="5aae1-135">코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5aae1-135">Using the Code Snippets</span></span>

<span data-ttu-id="5aae1-136">랩 문서를 통해 코드 블록을 삽입 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-136">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="5aae1-137">사용자 편의 위해이 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-137">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="5aae1-138">각 연습에는 시작 솔루션 동반 되는 **시작** 개별적으로 각 연습에 따라 할 수 있는 작업의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-138">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="5aae1-139">주의 하십시오 연습 하는 동안 추가 된 코드 조각은 솔루션 시작이 항목에서 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-139">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="5aae1-140">실행에 대 한 소스 코드에서 찾아볼 수 있습니다는 **끝** 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-140">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="5aae1-141">이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-141">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="5aae1-142">연습</span><span class="sxs-lookup"><span data-stu-id="5aae1-142">Exercises</span></span>

<span data-ttu-id="5aae1-143">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-143">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="5aae1-144">SignalR을 사용 하 여 실시간 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="5aae1-144">Working with Real-Time Data Using SignalR</span></span>](#Exercise1)
2. [<span data-ttu-id="5aae1-145">SQL Server를 사용 하 여 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-145">Scaling Out Using SQL Server</span></span>](#Exercise2)

<span data-ttu-id="5aae1-146">예상 소요 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="5aae1-146">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="5aae1-147">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-147">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="5aae1-148">미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-148">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="5aae1-149">이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-149">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="5aae1-150">개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-150">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a><span data-ttu-id="5aae1-151">연습 1: SignalR을 사용 하 여 실시간 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="5aae1-151">Exercise 1: Working with Real-Time Data Using SignalR</span></span>

<span data-ttu-id="5aae1-152">채팅은 일반적으로 예를 들어 사용 되지만 할 수 있는 전체 실시간 웹 기능으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-152">While chat is often used as an example, you can do a whole lot more with real-time Web functionality.</span></span> <span data-ttu-id="5aae1-153">사용자를 새 데이터 나 페이지 구현 Ajax 긴 폴링과 새 데이터를 검색 하는 웹 페이지를 새로 고칩니다. 언제 든 지 SignalR를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-153">Any time a user refreshes a web page to see new data or the page implements Ajax long polling to retrieve new data, you can use SignalR.</span></span>

<span data-ttu-id="5aae1-154">SignalR 지원 **서버 푸시** 또는 **브로드캐스트** 기능을 자동으로 연결 관리 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-154">SignalR supports **server push** or **broadcasting** functionality; it handles connection management automatically.</span></span> <span data-ttu-id="5aae1-155">클라이언트-서버 통신에 대 한 기본 HTTP 연결에서 연결이 각 요청에 대 한 다시 설정 하지만 SignalR 클라이언트와 서버 간에 영구 연결을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-155">In classic HTTP connections for client-server communication, connection is re-established for each request, but SignalR provides persistent connection between the client and server.</span></span> <span data-ttu-id="5aae1-156">서버 코드가 원격 프로시저 호출 (RPC)을 사용 하 여 브라우저에서 클라이언트 코드를 호출할 SignalR에서 요청-응답 모델 대신 알고 오늘 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-156">In SignalR the server code calls out to a client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model we know today.</span></span>

<span data-ttu-id="5aae1-157">이 연습에서는 구성에서 **들은 퀴즈** 전체 페이지를 새로 고칠 하지 않고도 업데이트 된 메트릭 사용 하 여 통계 대시보드 표시 하려면 SignalR을 사용 하도록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-157">In this exercise, you will configure the **Geek Quiz** application to use SignalR to display the Statistics dashboard with the updated metrics without the need to refresh the entire page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a><span data-ttu-id="5aae1-158">작업 1-들은 퀴즈 통계 페이지 탐색</span><span class="sxs-lookup"><span data-stu-id="5aae1-158">Task 1 – Exploring the Geek Quiz Statistics Page</span></span>

<span data-ttu-id="5aae1-159">이 태스크에서는 응용 프로그램을 통해 이동 하 고 통계 페이지가 어떻게 표시 되는지 확인 하십시오 됩니다 고 방식으로 정보를 개선 하는 방법을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-159">In this task, you will go through the application and verify how the statistics page is shown and how you can improve the way the information is updated.</span></span>

1. <span data-ttu-id="5aae1-160">열고 **Visual Studio Express 2013 for Web** 엽니다는 **GeekQuiz.sln** 솔루션에 있는 **Source\Ex1 WorkingWithRealTimeData\Begin** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-160">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source\Ex1-WorkingWithRealTimeData\Begin** folder.</span></span>
2. <span data-ttu-id="5aae1-161">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-161">Press **F5** to run the solution.</span></span> <span data-ttu-id="5aae1-162">**로그인** 페이지가 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-162">The **Log in** page should appear in the browser.</span></span>

    <span data-ttu-id="5aae1-163">![솔루션을 실행](real-time-web-applications-with-signalr/_static/image2.png "솔루션 실행")</span><span class="sxs-lookup"><span data-stu-id="5aae1-163">![Running the solution](real-time-web-applications-with-signalr/_static/image2.png "Running the solution")</span></span>

    <span data-ttu-id="5aae1-164">*솔루션을 실행*</span><span class="sxs-lookup"><span data-stu-id="5aae1-164">*Running the solution*</span></span>
3. <span data-ttu-id="5aae1-165">클릭 **등록** 사용자를 만들려면 새 응용 프로그램에서 페이지의 오른쪽 위 모퉁이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-165">Click **Register** in the upper-right corner of the page to create a new user in the application.</span></span>

    <span data-ttu-id="5aae1-166">![등록 링크](real-time-web-applications-with-signalr/_static/image3.png "레지스터 링크")</span><span class="sxs-lookup"><span data-stu-id="5aae1-166">![Register link](real-time-web-applications-with-signalr/_static/image3.png "Register link")</span></span>

    <span data-ttu-id="5aae1-167">*링크를 등록 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5aae1-167">*Register link*</span></span>
4. <span data-ttu-id="5aae1-168">에 **등록** 페이지에서 입력 한 **사용자 이름** 및 **암호**, 클릭 하 고 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-168">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="5aae1-169">![사용자 등록](real-time-web-applications-with-signalr/_static/image4.png "사용자 등록")</span><span class="sxs-lookup"><span data-stu-id="5aae1-169">![Registering a user](real-time-web-applications-with-signalr/_static/image4.png "Registering a user")</span></span>

    <span data-ttu-id="5aae1-170">*사용자 등록*</span><span class="sxs-lookup"><span data-stu-id="5aae1-170">*Registering a user*</span></span>
5. <span data-ttu-id="5aae1-171">응용 프로그램에서 새 계정을 등록 하 고 사용자가 인증 되 고 첫 번째 퀴즈 질문을 보여 주는 홈 페이지로 다시 리디렉션되 며 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-171">The application registers the new account and the user is authenticated and redirected back to the home page showing the first quiz question.</span></span>
6. <span data-ttu-id="5aae1-172">열기는 **통계** 넣은 새 창에서 페이지는 **홈** 페이지 및 **통계** -나란히 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-172">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side.</span></span>

    <span data-ttu-id="5aae1-173">![Side-by-side-windows](real-time-web-applications-with-signalr/_static/image5.png "측 windows 쪽")</span><span class="sxs-lookup"><span data-stu-id="5aae1-173">![Side-by-side windows](real-time-web-applications-with-signalr/_static/image5.png "Side by side windows")</span></span>

    <span data-ttu-id="5aae1-174">*Side-by-side-windows*</span><span class="sxs-lookup"><span data-stu-id="5aae1-174">*Side-by-side windows*</span></span>
7. <span data-ttu-id="5aae1-175">에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-175">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="5aae1-176">![질문에 대답](real-time-web-applications-with-signalr/_static/image6.png "질문에 대답")</span><span class="sxs-lookup"><span data-stu-id="5aae1-176">![Answering a question](real-time-web-applications-with-signalr/_static/image6.png "Answering a question")</span></span>

    <span data-ttu-id="5aae1-177">*질문에 대답*</span><span class="sxs-lookup"><span data-stu-id="5aae1-177">*Answering a question*</span></span>
8. <span data-ttu-id="5aae1-178">단추 중 하나를 클릭 한 후에 대답 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-178">After clicking one of the buttons, the answer should appear.</span></span>

    <span data-ttu-id="5aae1-179">![질문에 대답할 올바른](real-time-web-applications-with-signalr/_static/image7.png "질문에 대답할 올바른")</span><span class="sxs-lookup"><span data-stu-id="5aae1-179">![Question answered correct](real-time-web-applications-with-signalr/_static/image7.png "Question answered correct")</span></span>

    <span data-ttu-id="5aae1-180">*올바르게 대답 질문*</span><span class="sxs-lookup"><span data-stu-id="5aae1-180">*Question answered correctly*</span></span>
9. <span data-ttu-id="5aae1-181">오래 된 통계 페이지에 제공 된 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-181">Notice that the information provided in the Statistics page is outdated.</span></span> <span data-ttu-id="5aae1-182">업데이트 된 결과 확인 하기 위해 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-182">Refresh the page in order to see the updated results.</span></span>

    <span data-ttu-id="5aae1-183">![통계 페이지](real-time-web-applications-with-signalr/_static/image8.png "통계 페이지")</span><span class="sxs-lookup"><span data-stu-id="5aae1-183">![Statistics page](real-time-web-applications-with-signalr/_static/image8.png "Statistics page")</span></span>

    <span data-ttu-id="5aae1-184">*통계 페이지*</span><span class="sxs-lookup"><span data-stu-id="5aae1-184">*Statistics page*</span></span>
10. <span data-ttu-id="5aae1-185">Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-185">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a><span data-ttu-id="5aae1-186">작업 2-온라인 차트를 표시 하 게 퀴즈를 추가 SignalR</span><span class="sxs-lookup"><span data-stu-id="5aae1-186">Task 2 – Adding SignalR to Geek Quiz to Show Online Charts</span></span>

<span data-ttu-id="5aae1-187">이 태스크에서는 SignalR 솔루션에 추가 하 고 때 업데이트 전송 되는 클라이언트에 자동으로 새 응답을 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-187">In this task, you will add SignalR to the solution and send updates to the clients automatically when a new answer is sent to the server.</span></span>

1. <span data-ttu-id="5aae1-188">**도구** 선택 Visual Studio에서 메뉴 **라이브러리 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-188">From the **Tools** menu in Visual Studio, select **Library Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="5aae1-189">에 **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-189">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="5aae1-190">![SignalR 패키지 설치](real-time-web-applications-with-signalr/_static/image9.png "SignalR 패키지 설치")</span><span class="sxs-lookup"><span data-stu-id="5aae1-190">![SignalR package installation](real-time-web-applications-with-signalr/_static/image9.png "SignalR package installation")</span></span>

    <span data-ttu-id="5aae1-191">*SignalR 패키지 설치*</span><span class="sxs-lookup"><span data-stu-id="5aae1-191">*SignalR package installation*</span></span>

   > [!NOTE]
   > <span data-ttu-id="5aae1-192">설치할 때 **SignalR** 를 수동으로 업데이트 해야 합니다는 완전히 새로운 MVC 5 응용 프로그램에서 NuGet 패키지 버전 2.0.2, **OWIN** 버전 2.0.1 패키지 (또는 이상) SignalR을 설치 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5aae1-192">When installing **SignalR** NuGet packages version 2.0.2 from a brand new MVC 5 application, you will need to manually update **OWIN** packages to version 2.0.1 (or higher) before installing SignalR.</span></span> <span data-ttu-id="5aae1-193">이 작업을 수행 하려면 다음 스크립트를 실행할 수 있습니다는 **패키지 관리자 콘솔**:</span><span class="sxs-lookup"><span data-stu-id="5aae1-193">To do this, you can execute the following script in the **Package Manager Console**:</span></span>
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > <span data-ttu-id="5aae1-194">SignalR의 이후 릴리스에서 OWIN 종속성 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-194">In a future release of SignalR, OWIN dependencies will be automatically updated.</span></span>
3. <span data-ttu-id="5aae1-195">**솔루션 탐색기**, 확장는 **스크립트** 폴더 및 표시 하는 SignalR *js* 솔루션에 추가 된 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-195">In **Solution Explorer**, expand the **Scripts** folder and notice that the SignalR *js* files were added to the solution.</span></span>

    <span data-ttu-id="5aae1-196">![SignalR JavaScript 참조](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 참조")</span><span class="sxs-lookup"><span data-stu-id="5aae1-196">![SignalR JavaScript references](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript references")</span></span>

    <span data-ttu-id="5aae1-197">*SignalR JavaScript 참조*</span><span class="sxs-lookup"><span data-stu-id="5aae1-197">*SignalR JavaScript references*</span></span>
4. <span data-ttu-id="5aae1-198">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **GeekQuiz** 프로젝트를 **추가** | **새 폴더**, 고 이름을 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-198">In **Solution Explorer**, right-click the **GeekQuiz** project, select **Add** | **New Folder**, and name it **Hubs**.</span></span>
5. <span data-ttu-id="5aae1-199">마우스 오른쪽 단추로 클릭는 **허브** 폴더를 선택 **추가 | 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-199">Right-click the **Hubs** folder and select **Add | New Item**.</span></span>

    <span data-ttu-id="5aae1-200">![새 항목 추가](real-time-web-applications-with-signalr/_static/image11.png "새 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="5aae1-200">![Add new item](real-time-web-applications-with-signalr/_static/image11.png "Add new item")</span></span>

    <span data-ttu-id="5aae1-201">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="5aae1-201">*Add new item*</span></span>
6. <span data-ttu-id="5aae1-202">에 **새 항목 추가** 대화 상자는 **Visual C# | 웹 | SignalR** 선택 왼쪽된 창에서 노드 **SignalR 허브 클래스 (v2)** 가운데 창에서 파일 이름을 **StatisticsHub.cs** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-202">In the **Add New Item** dialog box, select the **Visual C# | Web | SignalR** node in the left pane, select **SignalR Hub Class (v2)** from the center pane, name the file **StatisticsHub.cs** and click **Add**.</span></span>

    <span data-ttu-id="5aae1-203">![새 항목 추가 대화 상자](real-time-web-applications-with-signalr/_static/image12.png "새 항목 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="5aae1-203">![Add new item dialog box](real-time-web-applications-with-signalr/_static/image12.png "Add new item dialog box")</span></span>

    <span data-ttu-id="5aae1-204">*새 항목 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="5aae1-204">*Add new item dialog box*</span></span>
7. <span data-ttu-id="5aae1-205">코드는 **StatisticsHub** 를 다음 코드로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-205">Replace the code in the **StatisticsHub** class with the following code.</span></span>

    <span data-ttu-id="5aae1-206">(코드 조각- *RealTimeSignalR e x-1-StatisticsHubClass*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-206">(Code Snippet - *RealTimeSignalR - Ex1 - StatisticsHubClass*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. <span data-ttu-id="5aae1-207">열기 **Startup.cs** 에 다음 줄의 끝에 추가 하 고는 **구성** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5aae1-207">Open **Startup.cs** and add the following line at the end of the **Configuration** method.</span></span>

    <span data-ttu-id="5aae1-208">(코드 조각- *RealTimeSignalR e x-1-MapSignalR*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-208">(Code Snippet - *RealTimeSignalR - Ex1 - MapSignalR*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. <span data-ttu-id="5aae1-209">열기는 **StatisticsService.cs** 내 페이지는 **서비스** 폴더 다음 추가 using 지시문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-209">Open the **StatisticsService.cs** page inside the **Services** folder and add the following using directives.</span></span>

    <span data-ttu-id="5aae1-210">(코드 조각- *RealTimeSignalR e x-1-UsingDirectives*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-210">(Code Snippet - *RealTimeSignalR - Ex1 - UsingDirectives*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. <span data-ttu-id="5aae1-211">업데이트의 연결 된 클라이언트에 알리려면를 먼저 검색 한 **컨텍스트** 현재 연결에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-211">To notify connected clients of updates, you first retrieve a **Context** object for the current connection.</span></span> <span data-ttu-id="5aae1-212">**허브** 개체 단일 클라이언트 또는 브로드캐스트를 연결 된 모든 클라이언트에 메시지를 보낼 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-212">The **Hub** object contains methods to send messages to a single client or broadcast to all connected clients.</span></span> <span data-ttu-id="5aae1-213">다음 메서드를 추가 **StatisticsService** 통계 데이터를 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-213">Add the following method to the **StatisticsService** class to broadcast the statistics data.</span></span>

    <span data-ttu-id="5aae1-214">(코드 조각- *RealTimeSignalR e x-1-NotifyUpdatesMethod*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-214">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesMethod*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="5aae1-215">위의 코드에서 사용 하는 임의의 메서드 이름 클라이언트에서 함수를 호출할 수 (예:: *updateStatistics*).</span><span class="sxs-lookup"><span data-stu-id="5aae1-215">In the code above, you are using an arbitrary method name to call a function on the client (i.e.: *updateStatistics*).</span></span> <span data-ttu-id="5aae1-216">메서드 이름은 지정 하는 의미 없는 IntelliSense 또는 컴파일 타임 유효성 검사에 대 한 동적 개체로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-216">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="5aae1-217">식이 런타임 시 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-217">The expression is evaluated at run time.</span></span> <span data-ttu-id="5aae1-218">메서드 호출이 실행 되 면 SignalR 메서드 이름과 매개 변수 값을 클라이언트로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-218">When the method call executes, SignalR sends the method name and the parameter values to the client.</span></span> <span data-ttu-id="5aae1-219">클라이언트에 있는 경우 메서드가 호출 되 고 매개 변수 값이 전달 되는 이름과 일치 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="5aae1-219">If the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="5aae1-220">메서드가 클라이언트에서 발견 되는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-220">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="5aae1-221">자세한 내용은를 참조 [ASP.NET SignalR 허브 API 가이드](../guide-to-the-api/hubs-api-guide-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-221">For more information, refer to [ASP.NET SignalR Hubs API Guide](../guide-to-the-api/hubs-api-guide-server.md).</span></span>
11. <span data-ttu-id="5aae1-222">열기는 **TriviaController.cs** 내 페이지는 **컨트롤러** 폴더 다음 추가 using 지시문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-222">Open the **TriviaController.cs** page inside the **Controllers** folder and add the following using directives.</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. <span data-ttu-id="5aae1-223">다음 강조 표시 된 코드를 추가 하는 **Post** 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="5aae1-223">Add the following highlighted code to the **Post** action method.</span></span>

    <span data-ttu-id="5aae1-224">(코드 조각- *RealTimeSignalR e x-1-NotifyUpdatesCall*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-224">(Code Snippet - *RealTimeSignalR - Ex1 - NotifyUpdatesCall*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. <span data-ttu-id="5aae1-225">열기는 **Statistics.cshtml** 내 페이지는 **보기 | 홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-225">Open the **Statistics.cshtml** page inside the **Views | Home** folder.</span></span> <span data-ttu-id="5aae1-226">찾을 **스크립트** 섹션 및 섹션의 시작 부분에 다음 스크립트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-226">Locate the **Scripts** section and add the following script references at the beginning of the section.</span></span>

    <span data-ttu-id="5aae1-227">(코드 조각- *RealTimeSignalR e x-1-SignalRScriptReferences*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-227">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRScriptReferences*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="5aae1-228">SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자는이 항목에 표시 된 버전 보다 더 최신 SignalR 스크립트 파일의 버전을 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-228">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="5aae1-229">코드에서 스크립트 참조가 프로젝트에 설치 된 스크립트 라이브러리의 버전이 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-229">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>
14. <span data-ttu-id="5aae1-230">SignalR 허브에 클라이언트를 연결 하 고 허브에서 새 메시지를 받으면 통계 데이터를 업데이트 하려면 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-230">Add the following highlighted code to connect the client to the SignalR hub and update the statistics data when a new message is received from the hub.</span></span>

    <span data-ttu-id="5aae1-231">(코드 조각- *RealTimeSignalR e x-1-SignalRClientCode*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-231">(Code Snippet - *RealTimeSignalR - Ex1 - SignalRClientCode*)</span></span>

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    <span data-ttu-id="5aae1-232">이 코드에서는 허브 프록시를 만드는 하는 서버에서 보낸 메시지를 수신할 이벤트 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-232">In this code, you are creating a Hub Proxy and registering an event handler to listen for messages sent by the server.</span></span> <span data-ttu-id="5aae1-233">통해 전송 된 메시지를 수신 하는 경우에 *updateStatistics* 메서드.</span><span class="sxs-lookup"><span data-stu-id="5aae1-233">In this case, you listen for messages sent through the *updateStatistics* method.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="5aae1-234">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="5aae1-234">Task 3 – Running the Solution</span></span>

<span data-ttu-id="5aae1-235">이 태스크에서는 자동으로 SignalR을 사용 하 여 새 질문에 답변 한 후 통계 뷰가 업데이트 되어 있는지 확인 하려면 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-235">In this task, you will run the solution to verify that the statistics view is updated automatically using SignalR after answering a new question.</span></span>

1. <span data-ttu-id="5aae1-236">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-236">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5aae1-237">아직 응용 프로그램에 로그인 하는 경우 작업 1에서 만든 사용자를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-237">If not already logged in to the application, log in with the user you created in Task 1.</span></span>
2. <span data-ttu-id="5aae1-238">열기는 **통계** 넣은 새 창에서 페이지는 **홈** 페이지 및 **통계** 작업 1에서와 같이-나란히 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-238">Open the **Statistics** page in a new window and put the **Home** page and **Statistics** page side-by-side as you did in Task 1.</span></span>
3. <span data-ttu-id="5aae1-239">에 **홈** 페이지에서 옵션 중 하나를 클릭 하 여 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-239">In the **Home** page, answer the question by clicking one of the options.</span></span>

    <span data-ttu-id="5aae1-240">![다른 질문에 답하려면](real-time-web-applications-with-signalr/_static/image13.png "다른 질문에 응답")</span><span class="sxs-lookup"><span data-stu-id="5aae1-240">![Answering another question](real-time-web-applications-with-signalr/_static/image13.png "Answering another question")</span></span>

    <span data-ttu-id="5aae1-241">*다른 질문에 응답*</span><span class="sxs-lookup"><span data-stu-id="5aae1-241">*Answering another question*</span></span>
4. <span data-ttu-id="5aae1-242">단추 중 하나를 클릭 한 후에 대답 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-242">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="5aae1-243">알림 페이지에 대 한 통계 정보를 전체 페이지를 새로 고치려면 하지 않고도 업데이트 된 정보로 질문에 답변 한 후 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-243">Notice that the Statistics information on the page is updated automatically after answering the question with the updated information without the need to refresh the entire page.</span></span>

    <span data-ttu-id="5aae1-244">![응답 한 후 통계 페이지를 새로](real-time-web-applications-with-signalr/_static/image14.png "답변 후 새로 고침 통계 페이지")</span><span class="sxs-lookup"><span data-stu-id="5aae1-244">![Statistics page refreshed after answer](real-time-web-applications-with-signalr/_static/image14.png "Statistics page refreshed after answer")</span></span>

    <span data-ttu-id="5aae1-245">*응답 한 후 새로 고친된 통계 페이지*</span><span class="sxs-lookup"><span data-stu-id="5aae1-245">*Statistics page refreshed after answer*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a><span data-ttu-id="5aae1-246">연습 2: SQL Server를 사용 하 여 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-246">Exercise 2: Scaling Out Using SQL Server</span></span>

<span data-ttu-id="5aae1-247">웹 응용 프로그램을 확장 하는 경우 일반적으로 중 선택할 수 있습니다 *스케일 업* 및 *수평 확장* 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-247">When scaling a web application, you can generally choose between *scaling up* and *scaling out* options.</span></span> <span data-ttu-id="5aae1-248">*수직* 의미 하는 동안 더 많은 리소스 (CPU, RAM, 등)와 더 큰 서버를 사용 하 여 *확장할* 부하를 처리할 서버 추가 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-248">*Scale up* means using a larger server, with more resources (CPU, RAM, etc.) while *scale out* means adding more servers to handle the load.</span></span> <span data-ttu-id="5aae1-249">후자와 문제는 클라이언트가 서로 다른 서버에 라우팅될 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-249">The problem with the latter is that the clients can get routed to different servers.</span></span> <span data-ttu-id="5aae1-250">하나의 서버에 연결 된 클라이언트에서 다른 서버에서 보낸 메시지를 받지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-250">A client that is connected to one server will not receive messages sent from another server.</span></span>

<span data-ttu-id="5aae1-251">라는 구성 요소를 사용 하 여 이러한 문제를 해결할 수 *백플레인*, 서버 간에 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-251">You can solve these issues by using a component called *backplane*, to forward messages between servers.</span></span> <span data-ttu-id="5aae1-252">사용 하도록 설정 하는 백플레인에 각 응용 프로그램 인스턴스에 메시지를 백플레인에 보내고 백플레인에서 다른 응용 프로그램 인스턴스에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-252">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span>

<span data-ttu-id="5aae1-253">현재 세 가지 유형의 SignalR에 대 한 백플레인</span><span class="sxs-lookup"><span data-stu-id="5aae1-253">There are currently three types of backplanes for SignalR:</span></span>

- <span data-ttu-id="5aae1-254">**Windows Azure 서비스 버스**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-254">**Windows Azure Service Bus**.</span></span> <span data-ttu-id="5aae1-255">서비스 버스는 메시징 인프라 느슨하게 결합 된 메시지를 보내는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-255">Service Bus is a messaging infrastructure that allows components to send loosely coupled messages.</span></span>
- <span data-ttu-id="5aae1-256">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="5aae1-256">**SQL Server**.</span></span> <span data-ttu-id="5aae1-257">SQL Server 백플레인에서 SQL 테이블에 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-257">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="5aae1-258">백플레인에서 효율적인 메시징에 대 한 Service Broker를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-258">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="5aae1-259">그러나 해당 Service Broker를 사용 하지 않는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-259">However, it also works if Service Broker is not enabled.</span></span>
- <span data-ttu-id="5aae1-260">**Redis**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-260">**Redis**.</span></span> <span data-ttu-id="5aae1-261">Redis는 메모리에 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-261">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="5aae1-262">Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-262">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>

<span data-ttu-id="5aae1-263">모든 메시지가 메시지 버스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-263">Every message is sent through a message bus.</span></span> <span data-ttu-id="5aae1-264">메시지 버스 구현 하는 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스에는 게시/구독 추상화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-264">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="5aae1-265">기본 대체 하 여 작업의 백플레인 **IMessageBus** 는 버스 해당 백플레인에서 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-265">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span>

<span data-ttu-id="5aae1-266">버스를 통해 백플레인에서에 각 서버 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-266">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="5aae1-267">메시지를 보낼 때를 백플레인에 이동 하 고 백플레인에서 모든 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-267">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="5aae1-268">서버 백플레인에서 메시지를 받으면 해당 로컬 캐시에서 메시지를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-268">When a server receives a message from the backplane, it stores the message in its local cache.</span></span> <span data-ttu-id="5aae1-269">서버는 다음 로컬 캐시에서 클라이언트에 메시지를 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-269">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="5aae1-270">SignalR 백플레인에서 작동 방식, 여기에 대 한 자세한 내용은 [문서](../performance/scaleout-in-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-270">For more information about how the SignalR backplane works, read this [article](../performance/scaleout-in-signalr.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5aae1-271">백플레인에 병목이 될 수 있는 몇 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-271">There are some scenarios where a backplane can become a bottleneck.</span></span> <span data-ttu-id="5aae1-272">다음은 몇 가지 일반적인 SignalR 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-272">Here are some typical SignalR scenarios:</span></span>
> 
> - <span data-ttu-id="5aae1-273">[서버 브로드캐스트](tutorial-server-broadcast-with-signalr.md) (예: 주식 시세): 백플레인 서버 메시지를 보내는 속도 제어 하기 때문에이 시나리오에 대 한 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-273">[Server broadcast](tutorial-server-broadcast-with-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
> - <span data-ttu-id="5aae1-274">[클라이언트-](tutorial-getting-started-with-signalr.md) (예: 채트):이 시나리오에서는 클라이언트의 수와 크기와 메시지 수가 조정 백플레인에서 병목 지점이 될 수 있습니다; 그리고 즉, 증가 하는 메시지의 속도 비율에 따라 더 많은 클라이언트에 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-274">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
> - <span data-ttu-id="5aae1-275">[높은 주파수 실시간](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임): 백플레인에이 시나리오에 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-275">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>


<span data-ttu-id="5aae1-276">이 연습을 사용 하 여 **SQL Server** 간에 메시지를 분산는 **들은 퀴즈** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-276">In this exercise, you will use **SQL Server** to distribute messages across the **Geek Quiz** application.</span></span> <span data-ttu-id="5aae1-277">모든 결과 얻기 위해 하지만 구성을 설정 하는 방법은 단일 테스트 컴퓨터에서 이러한 작업을 실행 합니다, 그리고 SignalR 응용 프로그램 두 개 이상의 서버에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-277">You will run these tasks on a single test machine to learn how to set up the configuration, but in order to get the full effect, you will need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="5aae1-278">서버 중 하나 또는 별도 전용된 서버에도 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-278">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span>

![SQL Server 다이어그램을 사용 하 여 확장](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a><span data-ttu-id="5aae1-280">작업 1-시나리오 이해</span><span class="sxs-lookup"><span data-stu-id="5aae1-280">Task 1 - Understanding the Scenario</span></span>

<span data-ttu-id="5aae1-281">이 작업의 2 개의 인스턴스를 실행 합니다 **들은 퀴즈** 로컬 컴퓨터의 인스턴스를 여러 개의 IIS를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-281">In this task, you will run 2 instances of **Geek Quiz** simulating multiple IIS instances on your local machine.</span></span> <span data-ttu-id="5aae1-282">이 시나리오에서는 하나의 응용 프로그램에 trivia 질문에 대답 하는 경우, 업데이트는 두 번째 인스턴스의 통계 페이지에 알림이 발송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-282">In this scenario, when answering trivia questions on one application, update won't be notified on the statistics page of the second instance.</span></span> <span data-ttu-id="5aae1-283">이 시뮬레이션 유사한 여러 인스턴스에서 응용 프로그램를 배포할 환경을 부하 분산 장치를 사용 하 여 서로 통신 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-283">This simulation resembles an environment where your application is deployed on multiple instances and using a load balancer to communicate with them.</span></span>

1. <span data-ttu-id="5aae1-284">열기는 **Begin.sln** 솔루션에 있는 **소스/e x 2-ScalingOutWithSQLServer/시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-284">Open the **Begin.sln** solution located in the **Source/Ex2-ScalingOutWithSQLServer/Begin** folder.</span></span> <span data-ttu-id="5aae1-285">로드 되 고 나면 알게 될 것에 **서버 탐색기** 하지만 서로 다른 이름을 구조 솔루션에 동일한 두 개의 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5aae1-285">Once loaded, you will notice on the **Server Explorer** that the solution has two projects with identical structures but different names.</span></span> <span data-ttu-id="5aae1-286">로컬 컴퓨터에서 동일한 응용 프로그램의 두 인스턴스를 실행 중인 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-286">This will simulate running two instances of the same application on your local machine.</span></span>

    <span data-ttu-id="5aae1-287">![시작 이라는 말 퀴즈의 2 개의 인스턴스를 시뮬레이션 하는 솔루션](real-time-web-applications-with-signalr/_static/image16.png "들은 퀴즈의 2 개의 인스턴스를 시뮬레이션 하는 솔루션 시작")</span><span class="sxs-lookup"><span data-stu-id="5aae1-287">![Begin Solution Simulating 2 Instances of Geek Quiz](real-time-web-applications-with-signalr/_static/image16.png "Begin Solution Simulating 2 Instances of Geek Quiz")</span></span>

    <span data-ttu-id="5aae1-288">*2 개의 들은 퀴즈의 인스턴스를 시뮬레이션 하는 솔루션 시작*</span><span class="sxs-lookup"><span data-stu-id="5aae1-288">*Begin Solution Simulating 2 Instances of Geek Quiz*</span></span>
2. <span data-ttu-id="5aae1-289">솔루션 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 솔루션의 속성 페이지를 열고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-289">Open the properties page of the solution by right-clicking the solution node and selecting **Properties**.</span></span> <span data-ttu-id="5aae1-290">**시작 프로젝트**선택, **여러 개의 시작 프로젝트** 변경는 **동작** 두 프로젝트에 대 한 값 *시작*합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-290">Under **Startup Project**, select **Multiple startup projects** and change the **Action** value for both projects to *Start*.</span></span>

    <span data-ttu-id="5aae1-291">![여러 프로젝트를 시작](real-time-web-applications-with-signalr/_static/image17.png "여러 프로젝트를 시작")</span><span class="sxs-lookup"><span data-stu-id="5aae1-291">![Starting Multiple Projects](real-time-web-applications-with-signalr/_static/image17.png "Starting Multiple Projects")</span></span>

    <span data-ttu-id="5aae1-292">*여러 프로젝트를 시작*</span><span class="sxs-lookup"><span data-stu-id="5aae1-292">*Starting Multiple Projects*</span></span>
3. <span data-ttu-id="5aae1-293">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-293">Press **F5** to run the solution.</span></span> <span data-ttu-id="5aae1-294">두 인스턴스는 응용 프로그램이 시작 **들은 퀴즈** 서로 다른 포트를 동일한 응용 프로그램의 여러 인스턴스를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-294">The application will launch two instances of **Geek Quiz** in different ports, simulating multiple instances of the same application.</span></span> <span data-ttu-id="5aae1-295">왼쪽에 화면의 오른쪽에도 브라우저 중 하나를 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-295">Pin one of the browsers on left and the other on the right of your screen.</span></span> <span data-ttu-id="5aae1-296">자격 증명으로 로그인 하거나 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-296">Log in with your credentials or register a new user.</span></span> <span data-ttu-id="5aae1-297">로그인 한 Trivia 페이지 왼쪽에 유지 하 고 이동는 **통계** 오른쪽의 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-297">Once logged in, keep the Trivia page on the left and go to the **Statistics** page in the browser on the right.</span></span>

    ![나란히 들은 퀴즈](real-time-web-applications-with-signalr/_static/image18.png)

    <span data-ttu-id="5aae1-299">*나란히 들은 퀴즈*</span><span class="sxs-lookup"><span data-stu-id="5aae1-299">*Geek Quiz Side by Side*</span></span>

    ![서로 다른 포트에서 들은 퀴즈](real-time-web-applications-with-signalr/_static/image19.png)

    <span data-ttu-id="5aae1-301">*서로 다른 포트에서 들은 퀴즈*</span><span class="sxs-lookup"><span data-stu-id="5aae1-301">*Geek Quiz in Different Ports*</span></span>
4. <span data-ttu-id="5aae1-302">왼쪽된 브라우저에서 질문에 응답을 시작한 것을 확인할 수는 **통계** 오른쪽 브라우저에서 페이지 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-302">Start answering questions in the left browser and you will notice that the **Statistics** page in the right browser is not being updated.</span></span> <span data-ttu-id="5aae1-303">때문에 이것이 **SignalR** 해당 클라이언트에 메시지를 분산 하는 로컬 캐시에서 사용 하 여 및이 시나리오는 여러 인스턴스를 시뮬레이션 하 고, 따라서 캐시 간에 공유 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-303">This is because **SignalR** uses a local cache to distribute messages across their clients and this scenario is simulating multiple instances, therefore the cache is not shared between them.</span></span> <span data-ttu-id="5aae1-304">확인할 수 있습니다 **SignalR** 테스트 단계와 동일 하지만 단일 앱을 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-304">You can verify that **SignalR** is working by testing the same steps but using a single app.</span></span> <span data-ttu-id="5aae1-305">다음 태스크에서는 인스턴스 간에 메시지를 복제 하려면 백플레인을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-305">In the following tasks you will configure a backplane to replicate the messages across instances.</span></span>
5. <span data-ttu-id="5aae1-306">Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-306">Go back to Visual Studio and stop debugging.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a><span data-ttu-id="5aae1-307">작업 2-SQL Server 백플레인에서 만들기</span><span class="sxs-lookup"><span data-stu-id="5aae1-307">Task 2 – Creating the SQL Server Backplane</span></span>

<span data-ttu-id="5aae1-308">이 태스크에서는 역할에 대 한 백플레인을 할 데이터베이스가 만들어집니다는 **들은 퀴즈** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-308">In this task, you will create a database that will serve as a backplane for the **Geek Quiz** application.</span></span> <span data-ttu-id="5aae1-309">사용 하 여 **SQL Server 개체 탐색기** 서버를 찾아 데이터베이스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-309">You will use **SQL Server Object Explorer** to browse your server and initialize the database.</span></span> <span data-ttu-id="5aae1-310">또한 기능을 사용 하기는 **Service Broker**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-310">Additionally, you will enable the **Service Broker**.</span></span>

1. <span data-ttu-id="5aae1-311">**Visual Studio**, 열기 메뉴 **보기** 선택 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-311">In **Visual Studio**, open menu **View** and select **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="5aae1-312">마우스 오른쪽 단추로 클릭 하 여 LocalDB 인스턴스에 연결 된 **SQL Server** 노드를 선택 하 고 **SQL Server 추가...**  옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-312">Connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="5aae1-313">![SQL Server 인스턴스를 추가](real-time-web-applications-with-signalr/_static/image20.png "SQL Server 인스턴스를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5aae1-313">![Adding a SQL Server Instance](real-time-web-applications-with-signalr/_static/image20.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="5aae1-314">*SQL Server 인스턴스를 SQL Server 개체 탐색기에 추가*</span><span class="sxs-lookup"><span data-stu-id="5aae1-314">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
3. <span data-ttu-id="5aae1-315">설정의 **서버 이름** 를 *(localdb) \v11.0* 둡니다 **Windows 인증** 인증 모드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-315">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="5aae1-316">클릭 **연결** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-316">Click **Connect** to continue.</span></span>

    <span data-ttu-id="5aae1-317">![LocalDB에 연결](real-time-web-applications-with-signalr/_static/image21.png "LocalDB에 연결")</span><span class="sxs-lookup"><span data-stu-id="5aae1-317">![Connecting to LocalDB](real-time-web-applications-with-signalr/_static/image21.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="5aae1-318">*LocalDB에 연결*</span><span class="sxs-lookup"><span data-stu-id="5aae1-318">*Connecting to LocalDB*</span></span>
4. <span data-ttu-id="5aae1-319">LocalDB 인스턴스를 연결한 했으므로 나타내는 SQL Server 백플레인에서 SignalR에 대 한 데이터베이스 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-319">Now that you are connected to your LocalDB instance, you will need to create a database that will represent the SQL Server backplane for SignalR.</span></span> <span data-ttu-id="5aae1-320">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **데이터베이스** 노드 선택한 **새 데이터베이스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-320">To do this, right-click the **Databases** node and select **Add New Database**.</span></span>

    <span data-ttu-id="5aae1-321">![새 데이터베이스에 추가](real-time-web-applications-with-signalr/_static/image22.png "새 데이터베이스에 추가")</span><span class="sxs-lookup"><span data-stu-id="5aae1-321">![Adding a new database](real-time-web-applications-with-signalr/_static/image22.png "Adding a new database")</span></span>

    <span data-ttu-id="5aae1-322">*새 데이터베이스에 추가*</span><span class="sxs-lookup"><span data-stu-id="5aae1-322">*Adding a new database*</span></span>
5. <span data-ttu-id="5aae1-323">데이터베이스 이름을 설정 *SignalR* 클릭 **확인** 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-323">Set the database name to *SignalR* and click **OK** to create it.</span></span>

    <span data-ttu-id="5aae1-324">![SignalR 데이터베이스를 만드는](real-time-web-applications-with-signalr/_static/image23.png "SignalR 데이터베이스를 만드는 중")</span><span class="sxs-lookup"><span data-stu-id="5aae1-324">![Creating the SignalR database](real-time-web-applications-with-signalr/_static/image23.png "Creating the SignalR database")</span></span>

    <span data-ttu-id="5aae1-325">*SignalR 데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="5aae1-325">*Creating the SignalR database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5aae1-326">데이터베이스에 대 한 이름을 임의로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-326">You can choose any name for the database.</span></span>
6. <span data-ttu-id="5aae1-327">에서 업데이트를 받는 보다 효율적으로 백플레인에서, 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-327">To receive updates more efficiently from the backplane, it is recommended to enable Service Broker for the database.</span></span> <span data-ttu-id="5aae1-328">Service Broker는 메시징 및 SQL Server의 큐에 대 한 기본 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-328">Service Broker provides native support for messaging and queuing in SQL Server.</span></span> <span data-ttu-id="5aae1-329">백플레인에서는 Service Broker 없이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-329">The backplane also works without Service Broker.</span></span> <span data-ttu-id="5aae1-330">선택한 데이터베이스를 마우스 오른쪽 단추로 클릭 하 여 새 쿼리를 열고 **새 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-330">Open a new query by right-clicking the database and select **New Query**.</span></span>

    <span data-ttu-id="5aae1-331">![새 쿼리를 열면](real-time-web-applications-with-signalr/_static/image24.png "새 쿼리 열기")</span><span class="sxs-lookup"><span data-stu-id="5aae1-331">![Opening a New Query](real-time-web-applications-with-signalr/_static/image24.png "Opening a New Query")</span></span>

    <span data-ttu-id="5aae1-332">*새 쿼리 열기*</span><span class="sxs-lookup"><span data-stu-id="5aae1-332">*Opening a New Query*</span></span>
7. <span data-ttu-id="5aae1-333">Service Broker가 설정 여부를 확인 하려면 쿼리는 **은\_브로커\_활성화** 열에는 **sys.databases** 카탈로그 뷰.</span><span class="sxs-lookup"><span data-stu-id="5aae1-333">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span> <span data-ttu-id="5aae1-334">최근에 열어 쿼리 창에서 다음 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-334">Execute the following script in the recently opened query window.</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    <span data-ttu-id="5aae1-335">![Service Broker 상태를 쿼리](real-time-web-applications-with-signalr/_static/image25.png "Service Broker 상태를 쿼리 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5aae1-335">![Querying the Service Broker Status](real-time-web-applications-with-signalr/_static/image25.png "Querying the Service Broker Status")</span></span>

    <span data-ttu-id="5aae1-336">*Service Broker 상태를 쿼리합니다.*</span><span class="sxs-lookup"><span data-stu-id="5aae1-336">*Querying the Service Broker Status*</span></span>
8. <span data-ttu-id="5aae1-337">하는 경우의 값은 **은\_브로커\_활성화** 데이터베이스의 열은 &quot;0&quot;를 사용 하도록 설정 하려면 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-337">If the value of the **is\_broker\_enabled** column in your database is &quot;0&quot;, use the following command to enable it.</span></span> <span data-ttu-id="5aae1-338">대체 **&lt;귀하가 데이터베이스&gt;** 데이터베이스를 만들 때 설정한 이름 (예:: SignalR).</span><span class="sxs-lookup"><span data-stu-id="5aae1-338">Replace **&lt;YOUR-DATABASE&gt;** with the name you set when creating the database (e.g.: SignalR).</span></span>

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    <span data-ttu-id="5aae1-339">![Service Broker를 사용 하도록 설정](real-time-web-applications-with-signalr/_static/image26.png "Service Broker 사용")</span><span class="sxs-lookup"><span data-stu-id="5aae1-339">![Enabling Service Broker](real-time-web-applications-with-signalr/_static/image26.png "Enabling Service Broker")</span></span>

    <span data-ttu-id="5aae1-340">*Service Broker를 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="5aae1-340">*Enabling Service Broker*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5aae1-341">DB에 연결 하는 응용 프로그램이 없습니다 없으면이 쿼리 표시 하려면 교착 상태에 있는지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="5aae1-341">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a><span data-ttu-id="5aae1-342">작업 3 – SignalR 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="5aae1-342">Task 3 – Configuring the SignalR Application</span></span>

<span data-ttu-id="5aae1-343">이 태스크에서는 구성 **들은 퀴즈** 백플레인에서 SQL Server에 연결 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-343">In this task, you will configure **Geek Quiz** to connect to the SQL Server backplane.</span></span> <span data-ttu-id="5aae1-344">먼저 추가한는 **SignalR.SqlServer** 백플레인 데이터베이스에는 NuGet 패키지 및 연결 집합 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-344">You will first add the **SignalR.SqlServer** NuGet package and set the connection string to your backplane database.</span></span>

1. <span data-ttu-id="5aae1-345">열기는 **패키지 관리자 콘솔** 에서 **도구** | **라이브러리 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-345">Open the **Package Manager Console** from **Tools** | **Library Package Manager**.</span></span> <span data-ttu-id="5aae1-346">다음 사항을 확인 **GeekQuiz** 에서 프로젝트를 선택는 **기본 프로젝트** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-346">Make sure that **GeekQuiz** project is selected in the **Default project** drop-down list.</span></span> <span data-ttu-id="5aae1-347">설치 하려면 다음 명령을 입력 하 고 **Microsoft.AspNet.SignalR.SqlServer** NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-347">Type the following command to install the **Microsoft.AspNet.SignalR.SqlServer** NuGet package.</span></span>

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. <span data-ttu-id="5aae1-348">프로젝트에 대해 이전 단계 하지만이 이번 반복 **GeekQuiz2**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-348">Repeat the previous step but this time for project **GeekQuiz2**.</span></span>
3. <span data-ttu-id="5aae1-349">SQL Server 백플레인에서 구성 하려면 엽니다는 **Startup.cs** 의 파일은 **GeekQuiz** 프로젝트 및 다음 코드를 추가 하는 **구성** 메서드.</span><span class="sxs-lookup"><span data-stu-id="5aae1-349">To configure the SQL Server backplane, open the **Startup.cs** file of the **GeekQuiz** project and add the following code to the **Configure** method.</span></span> <span data-ttu-id="5aae1-350">대체 **&lt;귀하가 데이터베이스&gt;** 을 SQL Server 백플레인에서 만들 때 사용한 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-350">Replace **&lt;YOUR-DATABASE&gt;** with your database name you used when creating the SQL Server backplane.</span></span> <span data-ttu-id="5aae1-351">이 단계를 반복 하는 **GeekQuiz2** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5aae1-351">Repeat this step for the **GeekQuiz2** project.</span></span>

    <span data-ttu-id="5aae1-352">(코드 조각- *RealTimeSignalR-e x 2-StartupConfiguration*)</span><span class="sxs-lookup"><span data-stu-id="5aae1-352">(Code Snippet - *RealTimeSignalR - Ex2 - StartupConfiguration*)</span></span>

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. <span data-ttu-id="5aae1-353">키를 눌러 프로젝트를 모두 SQL Server 백플레인에서 사용 하도록 구성 된, 했으므로 **F5** 으로 동시에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-353">Now that both projects are configured to use the SQL Server backplane, press **F5** to run them simultaneously.</span></span>
5. <span data-ttu-id="5aae1-354">다시, **Visual Studio** 의 두 인스턴스가 시작 됩니다 **들은 퀴즈** 서로 다른 포트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-354">Again, **Visual Studio** will launch two instances of **Geek Quiz** in different ports.</span></span> <span data-ttu-id="5aae1-355">브라우저 중 하나는 왼쪽의 다른 사용자의 화면 오른쪽에 고정 및 사용자 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-355">Pin one of the browsers on the left and the other on the right of your screen and log in with your credentials.</span></span> <span data-ttu-id="5aae1-356">왼쪽에 퀴즈 페이지를 유지 하 고 이동 **통계** pagein 오른쪽 브라우저.</span><span class="sxs-lookup"><span data-stu-id="5aae1-356">Keep the Trivia page on the left and go to **Statistics** pagein the right browser.</span></span>
6. <span data-ttu-id="5aae1-357">왼쪽된 브라우저에서 질문에 대답을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-357">Start answering questions in the left browser.</span></span> <span data-ttu-id="5aae1-358">이 이번에는 **통계** 백플레인에서 덕분에 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-358">This time, the **Statistics** page is updated thanks to the backplane.</span></span> <span data-ttu-id="5aae1-359">응용 프로그램 간 전환 (**통계** 왼쪽에는 이제 및 **퀴즈** 오른쪽에 표시 됩니다) 하 고 두 인스턴스 모두에 대 한 작동 하는지 유효성을 검사 하는 테스트를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-359">Switch between applications (**Statistics** is now on the left, and **Trivia** is on the right) and repeat the test to validate that it is working for both instances.</span></span> <span data-ttu-id="5aae1-360">백플레인에서 역할을 한 *캐시 공유* 연결 된 클라이언트를 배포 하기 위한 자체 로컬 캐시에 메시지가 저장은 각 연결 된 서버와 각 서버에 대 한 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-360">The backplane serves as a *shared cache* of messages for each connected server, and each server will store the messages in their own local cache to distribute to connected clients.</span></span>
7. <span data-ttu-id="5aae1-361">Visual Studio로 다시 이동 하 고 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-361">Go back to Visual Studio and stop debugging.</span></span>
8. <span data-ttu-id="5aae1-362">SQL Server 백플레인 구성 요소는 자동으로 지정된 된 데이터베이스에 필요한 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-362">The SQL Server backplane component automatically generates the necessary tables on the specified database.</span></span> <span data-ttu-id="5aae1-363">에 **SQL Server 개체 탐색기** 패널에서 백플레인에서 대해 만든 데이터베이스를 엽니다 (예:: SignalR) 해당 테이블을 확장 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-363">In the **SQL Server Object Explorer** panel, open the database you created for the backplane (e.g.: SignalR) and expand its tables.</span></span> <span data-ttu-id="5aae1-364">다음 표에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-364">You should see the following tables:</span></span>

    ![백플레인 테이블 생성](real-time-web-applications-with-signalr/_static/image27.png)

    <span data-ttu-id="5aae1-366">*백플레인 테이블 생성*</span><span class="sxs-lookup"><span data-stu-id="5aae1-366">*Backplane Generated Tables*</span></span>
9. <span data-ttu-id="5aae1-367">마우스 오른쪽 단추로 클릭는 **SignalR.Messages\_0** 테이블을 선택한 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-367">Right-click the **SignalR.Messages\_0** table and select **View Data**.</span></span>

    ![SignalR 백플레인 메시지 테이블 보기](real-time-web-applications-with-signalr/_static/image28.png)

    <span data-ttu-id="5aae1-369">*SignalR 백플레인 메시지 테이블 보기*</span><span class="sxs-lookup"><span data-stu-id="5aae1-369">*View SignalR Backplane Messages Table*</span></span>
10. <span data-ttu-id="5aae1-370">로 전송 된 다른 메시지를 볼 수는 **허브** trivia 질문에 대답 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5aae1-370">You can see the different messages sent to the **Hub** when answering the trivia questions.</span></span> <span data-ttu-id="5aae1-371">백플레인에서이 메시지는 연결 된 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-371">The backplane distributes these messages to any connected instance.</span></span>

    ![백플레인 메시지 테이블](real-time-web-applications-with-signalr/_static/image29.png)

    <span data-ttu-id="5aae1-373">*백플레인 메시지 테이블*</span><span class="sxs-lookup"><span data-stu-id="5aae1-373">*Backplane Messages Table*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="5aae1-374">요약</span><span class="sxs-lookup"><span data-stu-id="5aae1-374">Summary</span></span>

<span data-ttu-id="5aae1-375">이 실습 랩에서 추가 하는 방법을 배웠습니다 **SignalR** 를 사용 하 여 연결 된 클라이언트에 서버에서 응용 프로그램 및 보내기 알림에 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-375">In this hands-on lab, you have learned how to add **SignalR** to your application and send notifications from the server to your connected clients using **Hubs**.</span></span> <span data-ttu-id="5aae1-376">사용 하 여 응용 프로그램을 확장 하는 방법을 배웠습니다 또한는 *백플레인* 여러 IIS 인스턴스에 응용 프로그램을 배포할 때 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5aae1-376">Additionally, you learned how to scale out your application by using a *backplane* component when your application is deployed in multiple IIS instances.</span></span>
