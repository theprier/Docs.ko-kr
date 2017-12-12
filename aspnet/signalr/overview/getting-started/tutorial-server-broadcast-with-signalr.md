---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: "자습서: 서버 2 SignalR과 브로드캐스트 | Microsoft Docs"
author: tdykstra
description: "이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 다음은 해당 commun을 서버 브로드캐스트가 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/13/2014
ms.topic: article
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: cd800062e87c07a0ef1d8d3d32c910aaf3e683cc
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="c4c72-104">자습서: 서버 2 SignalR과 브로드캐스트</span><span class="sxs-lookup"><span data-stu-id="c4c72-104">Tutorial: Server Broadcast with SignalR 2</span></span>
====================
<span data-ttu-id="c4c72-105">여 [Tom Dykstra](https://github.com/tdykstra), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c4c72-105">by [Tom Dykstra](https://github.com/tdykstra), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c4c72-106">이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-106">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="c4c72-107">서버 브로드캐스트 클라이언트에 전달 되는 통신 서버에 의해 시작 된 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-107">Server broadcast means that communications sent to clients are initiated by the server.</span></span> <span data-ttu-id="c4c72-108">이 시나리오는 클라이언트에 전달 되는 통신 하나 이상의 클라이언트에 의해 시작 됩니다 채팅 응용 프로그램과 같은 피어 투 피어 시나리오 보다 다른 프로그래밍 방식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-108">This scenario requires a different programming approach than peer-to-peer scenarios such as chat applications, in which communications sent to clients are initiated by one or more of the clients.</span></span>
> 
> <span data-ttu-id="c4c72-109">이 자습서에서 만들 수 있는 응용 프로그램은 주식 시세를, 서버 브로드캐스트 기능에 대 한 일반적인 시나리오를 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-109">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span>
> 
> <span data-ttu-id="c4c72-110">이 항목 원래 Patrick Fletcher 썼습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-110">This topic was originally written by Patrick Fletcher.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c4c72-111">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c4c72-111">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="c4c72-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c4c72-112">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="c4c72-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c4c72-113">.NET 4.5</span></span>
> - <span data-ttu-id="c4c72-114">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="c4c72-114">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="c4c72-115">이 자습서와 함께 Visual Studio 2012를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c4c72-115">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="c4c72-116">이 자습서와 함께 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-116">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="c4c72-117">업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 를 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-117">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="c4c72-118">설치는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-118">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="c4c72-119">웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-119">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="c4c72-120">SignalR 클래스에 대 한 Visual Studio 템플릿을와 같은 설치 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-120">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="c4c72-121">일부 서식 파일 (와 같은 **OWIN 시작 클래스**)은 사용할 수 없습니다; 이러한 경우에 대 한 클래스 파일을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-121">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="c4c72-122">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="c4c72-122">Tutorial Versions</span></span>
> 
> <span data-ttu-id="c4c72-123">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-123">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="c4c72-124">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="c4c72-124">Questions and comments</span></span>
> 
> <span data-ttu-id="c4c72-125">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="c4c72-125">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c4c72-126">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-126">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="c4c72-127">개요</span><span class="sxs-lookup"><span data-stu-id="c4c72-127">Overview</span></span>

<span data-ttu-id="c4c72-128">이 자습서에서는 정기적으로 "푸시" 하려는 실시간 응용 프로그램의 대표가 주식 시세 응용 프로그램 만들기 또는 브로드캐스트, 연결 된 모든 클라이언트에 서버에서 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-128">In this tutorial, you'll create a stock ticker application that is representative of real-time applications in which you want to periodically "push," or broadcast, notifications from the server to all connected clients.</span></span> <span data-ttu-id="c4c72-129">이 자습서의 첫 번째 부분에서는 처음부터 해당 응용 프로그램의 단순화 된 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-129">In the first part of this tutorial, you'll create a simplified version of that application from scratch.</span></span> <span data-ttu-id="c4c72-130">자습서의 나머지 부분에서는 추가 기능을 포함 하는 NuGet 패키지를 설치 하 고 이러한 기능에 대 한 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-130">In the remainder of the tutorial, you'll install a NuGet package that contains additional features, and review the code for those features.</span></span>

<span data-ttu-id="c4c72-131">이 자습서의 첫 번째 부분을 만들 것인지를 응용 프로그램에는 주식 데이터로 구성 된 표가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-131">The application that you'll build in the first part of this tutorial displays a grid with stock data.</span></span>

![StockTicker 초기 버전](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="c4c72-133">정기적으로 서버 임의로 주가 업데이트 되 고 모든 연결 된 클라이언트에 업데이트를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-133">Periodically the server randomly updates stock prices and pushes the updates to all connected clients.</span></span> <span data-ttu-id="c4c72-134">브라우저 숫자 및 기호는 **변경** 및  **%**  열 서버에서 알림에 대 한 응답으로 동적으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-134">In the browser the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="c4c72-135">모두 동일한 데이터 및 표시 된 데이터에 동일한 변경 내용을 동시에 동일한 URL로 브라우저를 추가로 열고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-135">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

<span data-ttu-id="c4c72-136">이 자습서에는 다음 섹션이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-136">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="c4c72-137">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4c72-137">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="c4c72-138">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c4c72-138">Create the project</span></span>](#createproject)
- [<span data-ttu-id="c4c72-139">서버 코드를 설정</span><span class="sxs-lookup"><span data-stu-id="c4c72-139">Set up the server code</span></span>](#server)
- [<span data-ttu-id="c4c72-140">클라이언트 코드를 설정</span><span class="sxs-lookup"><span data-stu-id="c4c72-140">Set up the client code</span></span>](#client)
- [<span data-ttu-id="c4c72-141">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="c4c72-141">Test the application</span></span>](#test)
- [<span data-ttu-id="c4c72-142">로깅을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="c4c72-142">Enable logging</span></span>](#enablelogging)
- [<span data-ttu-id="c4c72-143">설치 하 고 전체 StockTicker 샘플을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-143">Install and review the full StockTicker sample</span></span>](#fullsample)
- [<span data-ttu-id="c4c72-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4c72-144">Next steps</span></span>](#nextsteps)

<span data-ttu-id="c4c72-145">[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지는 Visual Studio 프로젝트에 샘플 시뮬레이션 주식 시세 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-145">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package installs a sample simulated stock ticker application in a Visual Studio project.</span></span>

> [!NOTE]
> <span data-ttu-id="c4c72-146">응용 프로그램을 작성 하는 단계를 진행 하도록 않으려면 새 빈 ASP.NET 웹 응용 프로그램 프로젝트에서 SignalR.Sample 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-146">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="c4c72-147">이 자습서의 단계를 수행 하지 않고 NuGet 패키지를 설치 하면 **readme.txt 파일에 지침을 따라야**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-147">If you install the NuGet package without performing the steps in this tutorial, **you must follow the instructions in the readme.txt file**.</span></span> <span data-ttu-id="c4c72-148">패키지를 실행 하려면 설치 패키지의 ConfigureSignalR 메서드를 호출 하는 OWIN 시작 클래스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-148">To run the package you need to add an OWIN startup class which calls the ConfigureSignalR method in the installed package.</span></span> <span data-ttu-id="c4c72-149">OWIN 시작 클래스를 추가 하지 않으면 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-149">You will receive an error if you do not add the OWIN startup class.</span></span>


<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="c4c72-150">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c4c72-150">Prerequisites</span></span>

<span data-ttu-id="c4c72-151">시작 하기 전에 Visual Studio 2013을 컴퓨터에 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-151">Before you start, make sure that you have Visual Studio 2013 installed on your computer.</span></span> <span data-ttu-id="c4c72-152">Visual Studio가 없는 경우 참조 [ASP.NET 다운로드](https://www.asp.net/downloads) 는 무료 Visual Studio 2013 Express 얻으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-152">If you don't have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express.</span></span>

<a id="createproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="c4c72-153">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-153">Create the project</span></span>

1. <span data-ttu-id="c4c72-154">**파일** 메뉴를 클릭 하 여 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-154">From the **File** menu, click **New Project**.</span></span>
2. <span data-ttu-id="c4c72-155">에 **새 프로젝트** 대화 상자에서 **C#** 아래 **템플릿** 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-155">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="c4c72-156">선택 된 **ASP.NET 빈 웹 응용 프로그램** 서식 파일을 프로젝트 이름 *SignalR.StockTicker*를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-156">Select the **ASP.NET Empty Web Application** template, name the project *SignalR.StockTicker*, and click **OK**.</span></span>

    ![새 프로젝트 대화 상자](tutorial-server-broadcast-with-signalr/_static/image2.png)
4. <span data-ttu-id="c4c72-158">에 **새 ASP.NET** 프로젝트 창, leave **빈** 선택한 클릭 **프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-158">In the **New ASP.NET** Project window, leave **Empty** selected and click **Create Project**.</span></span>

    ![새 ASP 프로젝트 대화 상자](tutorial-server-broadcast-with-signalr/_static/image3.png)

<a id="server"></a>

## <a name="set-up-the-server-code"></a><span data-ttu-id="c4c72-160">서버 코드를 설정</span><span class="sxs-lookup"><span data-stu-id="c4c72-160">Set up the server code</span></span>

<span data-ttu-id="c4c72-161">이 섹션에서는 서버에서 실행 하는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-161">In this section you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="c4c72-162">스톡 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="c4c72-162">Create the Stock class</span></span>

<span data-ttu-id="c4c72-163">사용 하 여 저장 하 고는 재고에 대 한 정보를 전송 하는 재고 모델 클래스를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-163">You begin by creating the Stock model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="c4c72-164">프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *Stock.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-164">Create a new class file in the project folder, name it *Stock.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="c4c72-165">주식을 만들 때 설정 하는 두 속성은 기호 (예를 들어 microsoft MSFT) 및 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-165">The two properties that you'll set when you create stocks are the Symbol (for example, MSFT for Microsoft) and the Price.</span></span> <span data-ttu-id="c4c72-166">다른 속성 가격 설정 하는 방법 및 시기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-166">The other properties depend on how and when you set Price.</span></span> <span data-ttu-id="c4c72-167">처음에 가격을 설정할 때 값을 가져옵니다 DayOpen에 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-167">The first time you set Price, the value gets propagated to DayOpen.</span></span> <span data-ttu-id="c4c72-168">DayOpen 가격 간의 차이 기반으로 후속 경우가 가격 변경 설정 PercentChange 속성 값을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-168">Subsequent times when you set Price, the Change and PercentChange property values are calculated based on the difference between Price and DayOpen.</span></span>

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a><span data-ttu-id="c4c72-169">StockTicker 및 StockTickerHub 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="c4c72-169">Create the StockTicker and StockTickerHub classes</span></span>

<span data-ttu-id="c4c72-170">서버-클라이언트 상호 작용을 처리 하는 SignalR 허브 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-170">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="c4c72-171">SignalR 허브 클래스에서 파생 되는 StockTickerHub 클래스는 클라이언트에서 연결 및 메서드 호출을 받고 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-171">A StockTickerHub class that derives from the SignalR Hub class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="c4c72-172">주식 데이터를 유지 관리 하 고 실행을 주기적으로 클라이언트 연결 독립적으로 가격 업데이트를 트리거하는 타이머 개체에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-172">You also need to maintain stock data and run a Timer object to periodically trigger price updates, independently of client connections.</span></span> <span data-ttu-id="c4c72-173">허브 인스턴스를 일시적으로 하기 때문에 허브 클래스에 이러한 함수를 넣을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-173">You can't put these functions in a Hub class, because Hub instances are transient.</span></span> <span data-ttu-id="c4c72-174">허브 클래스 인스턴스를 연결 및 클라이언트에서 호출을 서버와 같은 허브에 각 작업에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-174">A Hub class instance is created for each operation on the hub, such as connections and calls from the client to the server.</span></span> <span data-ttu-id="c4c72-175">따라서 StockTicker 이름을 지정 하는 별도 클래스에서 실행 하는 주식 데이터를 유지 하 고, 가격을 업데이트, 브로드캐스트하 price 업데이트 메커니즘에서.</span><span class="sxs-lookup"><span data-stu-id="c4c72-175">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class, which you'll name StockTicker.</span></span>

![StockTicker에서 브로드캐스트](tutorial-server-broadcast-with-signalr/_static/image5.png)

<span data-ttu-id="c4c72-177">까다롭기 때문에 각 StockTickerHub 인스턴스로부터 단일 StockTicker 인스턴스에 대 한 참조를 설정 하는 서버에서 실행 되도록 StockTicker 클래스의 인스턴스가 하나씩 하려는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-177">You only want one instance of the StockTicker class to run on the server, so you'll need to set up a reference from each StockTickerHub instance to the singleton StockTicker instance.</span></span> <span data-ttu-id="c4c72-178">StockTicker 클래스에서 StockTicker 허브 클래스가 아닙니다. 하지만 주식 데이터 개이고 업데이트 트리거 때문에 클라이언트에 브로드캐스트할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-178">The StockTicker class has to be able to broadcast to clients because it has the stock data and triggers updates, but StockTicker is not a Hub class.</span></span> <span data-ttu-id="c4c72-179">따라서 StockTicker 클래스는 SignalR 허브 연결 컨텍스트 개체에 대 한 참조를 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-179">Therefore, the StockTicker class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="c4c72-180">클라이언트에 브로드캐스트하는 SignalR 연결 컨텍스트 개체를 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-180">It can then use the SignalR connection context object to broadcast to clients.</span></span>

1. <span data-ttu-id="c4c72-181">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **추가 | SignalR 허브 클래스 (v2)**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-181">In **Solution Explorer**, right-click the project and click **Add | SignalR Hub Class (v2)**.</span></span>
2. <span data-ttu-id="c4c72-182">새 허브 이름을 *StockTickerHub.cs*, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-182">Name the new hub *StockTickerHub.cs*, and then click **Add**.</span></span> <span data-ttu-id="c4c72-183">SignalR NuGet 패키지를 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-183">SignalR NuGet packages will be added to your project.</span></span>
3. <span data-ttu-id="c4c72-184">템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-184">Replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

    <span data-ttu-id="c4c72-185">[허브](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스는 클라이언트가 서버에서 호출할 수 있는 메서드를 정의 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-185">The [Hub](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class is used to define methods the clients can call on the server.</span></span> <span data-ttu-id="c4c72-186">메서드가 두 개를 정의 하는: `GetAllStocks()`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-186">You are defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="c4c72-187">클라이언트가 서버에 처음 연결을 주식의 현재 가격으로 모든 목록을 가져오려면이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-187">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="c4c72-188">메서드는 동기적으로 실행 하 고 반환할 수 `IEnumerable<Stock>` 메모리에서 연결 된 데이터를 반환 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-188">The method can execute synchronously and return `IEnumerable<Stock>` because it is returning data from memory.</span></span> <span data-ttu-id="c4c72-189">대기 데이터베이스를 조회 하는 웹 서비스 호출 등을 포함 하는 방법을 사용 하면 데이터를 가져올 메서드를 갖는 경우 지정 하는 경우 `Task<IEnumerable<Stock>>` 비동기 처리를 사용할 경우 반환 값으로.</span><span class="sxs-lookup"><span data-stu-id="c4c72-189">If the method had to get the data by doing something that would involve waiting, such as a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="c4c72-190">자세한 내용은 참조 [ASP.NET SignalR 허브 API 가이드-서버-을 비동기적으로 실행할 때](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-190">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

    <span data-ttu-id="c4c72-191">HubName 특성 허브 클라이언트에 JavaScript 코드에서 참조 되는 방식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-191">The HubName attribute specifies how the Hub will be referenced in JavaScript code on the client.</span></span> <span data-ttu-id="c4c72-192">이 특성을 사용 하지 않는 경우 클라이언트의 기본 이름 카멜식 대/소문자를 사용의 버전이 예제의 stockTickerHub 수 있는 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-192">The default name on the client if you don't use this attribute is a camel-cased version of the class name, which in this case would be stockTickerHub.</span></span>

    <span data-ttu-id="c4c72-193">StockTicker 클래스를 만들 때 나중에 표시 됩니다, 해당 클래스의 singleton 인스턴스를 정적 인스턴스 속성에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-193">As you'll see later when you create the StockTicker class, a singleton instance of that class is created in its static Instance property.</span></span> <span data-ttu-id="c4c72-194">얼마나 많은 클라이언트가 연결 또는 연결 끊기에 관계 없이 메모리에 유지 됩니다 StockTicker의 singleton 인스턴스를 해당 인스턴스는 GetAllStocks 메서드 현재 주식 정보를 반환 하는 데 사용 하는 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-194">That singleton instance of StockTicker remains in memory no matter how many clients connect or disconnect, and that instance is what the GetAllStocks method uses to return current stock information.</span></span>
4. <span data-ttu-id="c4c72-195">프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *StockTicker.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-195">Create a new class file in the project folder, name it *StockTicker.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="c4c72-196">여러 스레드에서 StockTicker 코드의 같은 인스턴스를 실행 하므로 StockTicker 클래스는 threadsafe를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-196">Since multiple threads will be running the same instance of StockTicker code, the StockTicker class has to be threadsafe.</span></span>

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="c4c72-197">정적 필드에 단일 인스턴스를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-197">Storing the singleton instance in a static field</span></span>

    <span data-ttu-id="c4c72-198">코드를 정적 초기화 \_인스턴스 필드는 클래스와이 인스턴스가 있는 인스턴스 속성을 지 원하는 유일한 인스턴스인 만들 수 있는 클래스의 생성자를 private으로 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-198">The code initializes the static \_instance field that backs the Instance property with an instance of the class, and this is the only instance of the class that can be created, because the constructor is marked as private.</span></span> <span data-ttu-id="c4c72-199">[초기화 지연](https://msdn.microsoft.com/en-us/library/dd997286.aspx) 에 사용 되는 \_인스턴스 필드를 인스턴스 생성 threadsafe 인지를 확인 하지만 성능 향상을 위해 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-199">[Lazy initialization](https://msdn.microsoft.com/en-us/library/dd997286.aspx) is used for the \_instance field, not for performance reasons but to ensure that the instance creation is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

    <span data-ttu-id="c4c72-200">클라이언트가 서버에 연결 될 때마다 별도의 스레드에서 실행 StockTickerHub 클래스의 새 인스턴스 StockTicker singleton 인스턴스를 가져옵니다 StockTicker.Instance 정적 속성에서 StockTickerHub 클래스 앞에서 보았듯이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-200">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the StockTicker.Instance static property, as you saw earlier in the StockTickerHub class.</span></span>

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="c4c72-201">ConcurrentDictionary 주식 데이터를 저장</span><span class="sxs-lookup"><span data-stu-id="c4c72-201">Storing stock data in a ConcurrentDictionary</span></span>

    <span data-ttu-id="c4c72-202">생성자가 초기화 하는 \_일부 샘플 주식 데이터 및 GetAllStocks를 사용 하 여 주식 컬렉션 주식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-202">The constructor initializes the \_stocks collection with some sample stock data, and GetAllStocks returns the stocks.</span></span> <span data-ttu-id="c4c72-203">앞서 살펴본 것 처럼 주가이 컬렉션에 클라이언트가 호출할 수 있는 허브 클래스에 서버 메서드로 StockTickerHub.GetAllStocks에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-203">As you saw earlier, this collection of stocks is in turn returned by StockTickerHub.GetAllStocks which is a server method in the Hub class that clients can call.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

    <span data-ttu-id="c4c72-204">주식 컬렉션으로 정의 됩니다는 [ConcurrentDictionary](https://msdn.microsoft.com/en-us/library/dd287191.aspx) 스레드로부터의 안전성에 대 한 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-204">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/en-us/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="c4c72-205">사용할 수 있습니다는 [사전](https://msdn.microsoft.com/en-us/library/xfhwa508.aspx) 개체를 명시적으로 변경 하는 경우 사전을 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-205">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/en-us/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

    <span data-ttu-id="c4c72-206">이 샘플 응용 프로그램에 대 한 좋다고 확인 메모리에 응용 프로그램 데이터를 저장 하 고 StockTicker 인스턴스가 삭제 될 때 데이터가 손실 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-206">For this sample application, it's OK to store application data in memory and to lose the data when the StockTicker instance is disposed.</span></span> <span data-ttu-id="c4c72-207">실제 응용 프로그램에서 데이터베이스와 같은 백 엔드 데이터 저장소와 함께 작동할 것 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-207">In a real application you would work with a back-end data store such as a database.</span></span>

    ### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="c4c72-208">주가 주기적으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="c4c72-208">Periodically updating stock prices</span></span>

    <span data-ttu-id="c4c72-209">생성자는 주기적으로 임의의 무휴로 주가 업데이트 하는 메서드를 호출 하는 타이머 개체를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-209">The constructor starts up a Timer object that periodically calls methods that update stock prices on a random basis.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

    <span data-ttu-id="c4c72-210">UpdateStockPrices는 state 매개 변수에서 null을 전달 하 고 타이머를 통해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-210">UpdateStockPrices is called by the Timer, which passes in null in the state parameter.</span></span> <span data-ttu-id="c4c72-211">사용 된 잠금이 가격을 업데이트 하기 전에 \_updateStockPricesLock 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-211">Before updating prices, a lock is taken on the \_updateStockPricesLock object.</span></span> <span data-ttu-id="c4c72-212">코드는 다른 스레드를 가격을 업데이트 하 고 목록에서 각 주식의 TryUpdateStockPrice 호출 다음 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-212">The code checks if another thread is already updating prices, and then it calls TryUpdateStockPrice on each stock in the list.</span></span> <span data-ttu-id="c4c72-213">TryUpdateStockPrice 메서드 주가 변경할지 여부를 결정 및 양을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-213">The TryUpdateStockPrice method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="c4c72-214">주식 가격이 변경 된 경우 연결 된 모든 클라이언트에 브로드캐스트 주가 변경 BroadcastStockPrice 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-214">If the stock price is changed, BroadcastStockPrice is called to broadcast the stock price change to all connected clients.</span></span>

    <span data-ttu-id="c4c72-215">\_updatingStockPrices 플래그로 표시 되어 [휘발성](https://msdn.microsoft.com/en-us/library/x13ttww7.aspx) 에 대 한 액세스 threadsafe 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-215">The \_updatingStockPrices flag is marked as [volatile](https://msdn.microsoft.com/en-us/library/x13ttww7.aspx) to ensure that access to it is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

    <span data-ttu-id="c4c72-216">실제 응용 프로그램에서 TryUpdateStockPrice 메서드; 가격을 조회 하는 웹 서비스 호출 것 이 코드에서 임의로 변경 하는 난수 생성기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-216">In a real application, the TryUpdateStockPrice method would call a web service to look up the price; in this code it uses a random number generator to make changes randomly.</span></span>

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="c4c72-217">클라이언트에 StockTicker 클래스 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기</span><span class="sxs-lookup"><span data-stu-id="c4c72-217">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

    <span data-ttu-id="c4c72-218">가격 변경을 여기 StockTicker 개체 들어오므로 모든 연결 된 클라이언트에서 updateStockPrice 메서드를 호출 해야 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-218">Because the price changes originate here in the StockTicker object, this is the object that needs to call an updateStockPrice method on all connected clients.</span></span> <span data-ttu-id="c4c72-219">허브 클래스 클라이언트 메서드 호출을 위한 API가 있지만 StockTicker 허브 클래스에서 파생 되지 않은 않으며 허브 개체에 대 한 참조를 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-219">In a Hub class you have an API for calling client methods, but StockTicker does not derive from the Hub class and does not have a reference to any Hub object.</span></span> <span data-ttu-id="c4c72-220">따라서 연결 된 클라이언트에 브로드캐스트용 하려면 SignalR 컨텍스트 인스턴스 StockTickerHub 클래스에 대 한 가져오고 하는 클라이언트에서 메서드를 호출할 StockTicker 클래스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-220">Therefore, in order to broadcast to connected clients, the StockTicker class has to get the SignalR context instance for the StockTickerHub class and use that to call methods on clients.</span></span>

    <span data-ttu-id="c4c72-221">코드 SignalR 컨텍스트에 대 한 참조의 패스를 참조 하는 생성자를 단일 항목 클래스 인스턴스를 만들 때 가져오고 생성자 클라이언트 속성에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-221">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the Clients property.</span></span>

    <span data-ttu-id="c4c72-222">다음 두 가지 컨텍스트를 한 번만 이유: 컨텍스트를 얻는 것은 비용이 많이 드는 작업 및 클라이언트에 전송 된 메시지의 의도 한 순서는 유지 하는 사용 하면 한 번 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-222">There are two reasons why you want to get the context just once: getting the context is an expensive operation, and getting it once ensures that the intended order of messages sent to clients is preserved.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="c4c72-223">컨텍스트의 클라이언트 속성을 가져오고 StockTickerClient 속성에 넣으면 허브 클래스에서와 같이 동일한 검색 하는 메서드를 호출할 클라이언트 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-223">Getting the Clients property of the context and putting it in the StockTickerClient property lets you write code to call client methods that looks the same as it would in a Hub class.</span></span> <span data-ttu-id="c4c72-224">예를 들어, 모든 클라이언트에 브로드캐스트하 Clients.All.updateStockPrice(stock)를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-224">For instance, to broadcast to all clients you can write Clients.All.updateStockPrice(stock).</span></span>

    <span data-ttu-id="c4c72-225">아직; BroadcastStockPrice를 호출 하는 updateStockPrice 메서드 없음 클라이언트에서 실행 되는 코드를 작성 하는 경우 나중에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-225">The updateStockPrice method that you are calling in BroadcastStockPrice doesn't exist yet; you'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="c4c72-226">Clients.All 런타임에 식을 평가할 수는 동적 이므로 updateStockPrice 여기를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-226">You can refer to updateStockPrice here because Clients.All is dynamic, which means the expression will be evaluated at runtime.</span></span> <span data-ttu-id="c4c72-227">이 메서드 호출이 실행 되 면 SignalR에서 메서드 이름과 매개 변수 값에 클라이언트에 보내고 클라이언트에 updateStockPrice 라는 메서드를 해당 메서드는 호출 되 고 매개 변수 값에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-227">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named updateStockPrice, that method will be called and the parameter value will be passed to it.</span></span>

    <span data-ttu-id="c4c72-228">Clients.All 모든 클라이언트에 보내는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-228">Clients.All means send to all clients.</span></span> <span data-ttu-id="c4c72-229">SignalR은 클라이언트 또는에 보내도록 클라이언트 그룹을 지정할 다른 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-229">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="c4c72-230">자세한 내용은 참조 [HubConnectionContext](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-230">For more information, see [HubConnectionContext](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="c4c72-231">SignalR 경로 등록</span><span class="sxs-lookup"><span data-stu-id="c4c72-231">Register the SignalR route</span></span>

<span data-ttu-id="c4c72-232">서버를 가로채 고 SignalR에 액세스 하는 URL을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-232">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="c4c72-233">에 추가할 do 및 OWIN 시작 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-233">To do that you'll add and OWIN startup class.</span></span>

1. <span data-ttu-id="c4c72-234">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **추가 | OWIN 시작 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-234">In **Solution Explorer**, right-click the project, and then click **Add | OWIN Startup Class**.</span></span> <span data-ttu-id="c4c72-235">클래스의 이름을 **Startup.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-235">Name the class **Startup.cs**.</span></span>
2. <span data-ttu-id="c4c72-236">코드 **Startup.cs** 다음으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-236">Replace the code in **Startup.cs** with the following.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="c4c72-237">이제 서버 코드를 설정을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-237">You have now completed setting up the server code.</span></span> <span data-ttu-id="c4c72-238">다음 섹션에서 클라이언트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-238">In the next section you'll set up the client.</span></span>

<a id="client"></a>

## <a name="set-up-the-client-code"></a><span data-ttu-id="c4c72-239">클라이언트 코드를 설정</span><span class="sxs-lookup"><span data-stu-id="c4c72-239">Set up the client code</span></span>

1. <span data-ttu-id="c4c72-240">프로젝트 폴더에 새 HTML 파일을 만들고 이름을 *StockTicker.html*합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-240">Create a new HTML file in the project folder, and name it *StockTicker.html*.</span></span>
2. <span data-ttu-id="c4c72-241">템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-241">Replace the template code with the following code.</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html)]

    <span data-ttu-id="c4c72-242">HTML 5 개의 열, 머리글 행 및 모든 5 개의 열에 걸쳐 있는 하나의 셀에 데이터 행이 있는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-242">The HTML creates a table with 5 columns, a header row, and a data row with a single cell that spans all 5 columns.</span></span> <span data-ttu-id="c4c72-243">데이터 행 "로드 중..."를 표시 하 고 일시적으로 응용 프로그램을 시작 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-243">The data row displays "loading..." and will only be shown momentarily when the application starts.</span></span> <span data-ttu-id="c4c72-244">JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 하는 주식 데이터를 사용 하 여의 전체 행에 추가할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-244">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="c4c72-245">스크립트 태그는 jQuery 스크립트 파일, SignalR core 스크립트 파일, SignalR 프록시 스크립트 파일 및 나중에 만드는 StockTicker 스크립트 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-245">The script tags specify the jQuery script file, the SignalR core script file, the SignalR proxies script file, and a StockTicker script file that you'll create later.</span></span> <span data-ttu-id="c4c72-246">"/ Signalr/허브" URL을 지정 하는 SignalR 프록시 스크립트 파일을 동적으로 생성 및 StockTickerHub.GetAllStocks에 대 한이 예에서 허브 클래스에 메서드에 대 한 프록시 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-246">The SignalR proxies script file, which specifies the "/signalr/hubs" URL, is dynamically generated and defines proxy methods for the methods on the Hub class, in this case for StockTickerHub.GetAllStocks.</span></span> <span data-ttu-id="c4c72-247">원하는 경우 생성할 수 있습니다이 JavaScript 파일을 수동으로 사용 하 여 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) MapHubs 메서드 호출에서 동적 파일 만들기를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-247">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) and disable dynamic file creation in the MapHubs method call.</span></span>
3. > [!IMPORTANT]
 > <span data-ttu-id="c4c72-248">JavaScript 파일에 참조 하는지 확인 *StockTicker.html* 올바른지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-248">Make sure that the JavaScript file references in *StockTicker.html* are correct.</span></span> <span data-ttu-id="c4c72-249">즉, 인지 확인 하거나 스크립트 태그 (예제에서 1.10.2)에서 jQuery 버전을 프로젝트의 jQuery 버전과 같은 *스크립트* 폴더 인지 확인 하거나 스크립트 태그의 SignalR 버전 SignalR과 동일 하 고 프로젝트의 버전 *스크립트* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-249">That is, make sure that the jQuery version in your script tag (1.10.2 in the example) is the same as the jQuery version in your project's *Scripts* folder, and make sure that the SignalR version in your script tag is the same as the SignalR version in your project's *Scripts* folder.</span></span> <span data-ttu-id="c4c72-250">필요에 따라 스크립트 태그의 파일 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-250">Change the file names in the script tags if necessary.</span></span>
4. <span data-ttu-id="c4c72-251">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *StockTicker.html*, 클릭 하 고 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-251">In **Solution Explorer**, right-click *StockTicker.html*, and then click **Set as Start Page**.</span></span>
5. <span data-ttu-id="c4c72-252">프로젝트 폴더에 새 JavaScript 파일을 만들고 이름을 *StockTicker.js*...</span><span class="sxs-lookup"><span data-stu-id="c4c72-252">Create a new JavaScript file in the project folder and name it *StockTicker.js*..</span></span>
6. <span data-ttu-id="c4c72-253">템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-253">Replace the template code with the following code:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

    <span data-ttu-id="c4c72-254">$.connection SignalR 프록시를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-254">$.connection refers to the SignalR proxies.</span></span> <span data-ttu-id="c4c72-255">코드는 StockTickerHub 클래스에 대 한 프록시에 대 한 참조를 가져오고 주식 종목 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-255">The code gets a reference to the proxy for the StockTickerHub class and puts it in the ticker variable.</span></span> <span data-ttu-id="c4c72-256">프록시 이름은 [HubName] 특성으로 설정 된 이름:</span><span class="sxs-lookup"><span data-stu-id="c4c72-256">The proxy name is the name that was set by the [HubName] attribute:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

    <span data-ttu-id="c4c72-257">모든 변수 및 함수를 정의한 후 파일에 코드의 마지막 줄 SignalR 시작 함수를 호출 하 여 SignalR 연결을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-257">After all the variables and functions are defined, the last line of code in the file initializes the SignalR connection by calling the SignalR start function.</span></span> <span data-ttu-id="c4c72-258">비동기적으로 실행 하 고 반환 하는 시작 함수는 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/), 비동기 작업이 완료 될 때 호출할 함수를 지정 완료 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-258">The start function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means you can call the done function to specify the function to call when the asynchronous operation is completed..</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

    <span data-ttu-id="c4c72-259">Init 함수는 서버에서 getAllStocks 함수를 호출 하 고 주식 테이블을 업데이트 하려면 서버를 반환 하는 정보를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-259">The init function calls the getAllStocks function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="c4c72-260">것을 확인할 기본적으로 카멜식 대/소문자 클라이언트 메서드 이름은 파스칼식 대 서버에 있지만 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-260">Notice that by default, you have to use camel casing on the client although the method name is pascal-cased on the server.</span></span> <span data-ttu-id="c4c72-261">카멜식 대 / 소문자 규칙은 개체가 아니라 방법에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-261">The camel-casing rule only applies to methods, not objects.</span></span> <span data-ttu-id="c4c72-262">예를 들어 재고를 참조할 수도 있습니다. 기호 및 stock 합니다. 가격, stock.symbol 말거나 stock.price 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-262">For example, you refer to stock.Symbol and stock.Price, not stock.symbol or stock.price.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

    <span data-ttu-id="c4c72-263">완전히 다른 메서드 이름을 사용 하려는 경우 수 데코레이팅되 HubMethodName 특성을 사용 하는 허브 메서드를 같은 방식으로 또는 클라이언트에서 파스칼식 대/소문자를 사용 하려는 경우 허브 클래스 자체 HubName 특성으로 데코레이팅된 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-263">If you wanted to use pascal casing on the client, or if you wanted to use a completely different method name, you could decorate the Hub method with the HubMethodName attribute the same way you decorated the Hub class itself with the HubName attribute.</span></span>

    <span data-ttu-id="c4c72-264">Init 메서드에 테이블 행에 대 한 HTML 스톡 개체의 서식 속성을 호출 formatStock 하 여 서버에서 받은 각 스톡 개체에 대해 만들어지고 다음 호출 하며 (맨 위에 있는 정의 된 *StockTicker.js*) 자리 표시자를 대체할 rowTemplate 변수에 스톡 개체 속성 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-264">In the init method, HTML for a table row is created for each stock object received from the server by calling formatStock to format properties of the stock object, and then by calling supplant (which is defined at the top of *StockTicker.js*) to replace placeholders in the rowTemplate variable with the stock object property values.</span></span> <span data-ttu-id="c4c72-265">결과 HTML 스톡 테이블에 다음 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-265">The resulting HTML is then appended to the stock table.</span></span>

    <span data-ttu-id="c4c72-266">비동기 시작 함수가 완료 된 후에 실행 되는 콜백 함수로 전달 하 여 초기화를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-266">You call init by passing it in as a callback function that executes after the asynchronous start function completes.</span></span> <span data-ttu-id="c4c72-267">시작을 호출한 후 별도 JavaScript 문으로 초기화를 호출 하는 경우 함수를 오류가 발생 시작 함수는 연결 구성 완료를 기다리지 않고 즉시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-267">If you called init as a separate JavaScript statement after calling start, the function would fail because it would execute immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="c4c72-268">이 경우 init 함수 서버 연결을 설정 하기 전에 getAllStocks 함수를 호출 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-268">In that case, the init function would try to call the getAllStocks function before the server connection is established.</span></span>

    <span data-ttu-id="c4c72-269">서버는 주식 가격 변경 되 면 연결 된 클라이언트에는 updateStockPrice를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-269">When the server changes a stock's price, it calls the updateStockPrice on connected clients.</span></span> <span data-ttu-id="c4c72-270">함수는 사용할 수 있도록 호출 하는 서버에서 stockTicker 프록시의 클라이언트 속성에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-270">The function is added to the client property of the stockTicker proxy in order to make it available to calls from the server.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

    <span data-ttu-id="c4c72-271">UpdateStockPrice 함수 init 함수에서와 같이 동일한 방식으로 테이블 행에는 서버에서 받은 스톡 개체의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-271">The updateStockPrice function formats a stock object received from the server into a table row the same way as in the init function.</span></span> <span data-ttu-id="c4c72-272">그러나 테이블에 행을 추가 하는 대신 재고의 현재 행 테이블에서 찾아 해당 행을 새 항목으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-272">However, instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

<a id="test"></a>

## <a name="test-the-application"></a><span data-ttu-id="c4c72-273">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="c4c72-273">Test the application</span></span>

1. <span data-ttu-id="c4c72-274">F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-274">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="c4c72-275">스톡 테이블의 "로드 중..." 줄을 다음 초기 주식 데이터를 표시 하는 짧은 지연 후 처음에 표시 하 고 변경 하려면 주식 가격을 시작 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-275">The stock table initially displays the "loading..." line, then after a short delay the initial stock data is displayed, and then the stock prices start to change.</span></span>

    ![로드](tutorial-server-broadcast-with-signalr/_static/image6.png)

    ![초기 스톡 테이블](tutorial-server-broadcast-with-signalr/_static/image7.png)

    ![서버에서 변경 내용을 수신할 주식 테이블](tutorial-server-broadcast-with-signalr/_static/image8.png)
2. <span data-ttu-id="c4c72-279">브라우저 주소 표시줄에서 URL을 복사 하 고 하나 이상의 새 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-279">Copy the URL from the browser address bar and paste it into one or more new browser window(s).</span></span>

    <span data-ttu-id="c4c72-280">초기 스톡 표시 된 첫 번째 브라우저와 같으면 이며 변경이 동시에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-280">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>
3. <span data-ttu-id="c4c72-281">모든 브라우저를 닫고 하 고 새 브라우저를 연 다음 동일한 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-281">Close all browsers and open a new browser, then go to the same URL.</span></span>

    <span data-ttu-id="c4c72-282">StockTicker singleton 개체는 서버에서 실행 스톡 테이블 디스플레이 주식 변경 하려면 계속 해 서 표시 되므로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-282">The StockTicker singleton object has continued to run in the server, so the stock table display shows that the stocks have continued to change.</span></span> <span data-ttu-id="c4c72-283">(숫자 값 변경에 0이 초기 표를 참조 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="c4c72-283">(You don't see the initial table with zero change figures.)</span></span>
4. <span data-ttu-id="c4c72-284">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-284">Close the browser.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="c4c72-285">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="c4c72-285">Enable logging</span></span>

<span data-ttu-id="c4c72-286">SignalR은 클라이언트에서 문제 해결에 도움이 되도록 설정할 수 있는 기본 제공 로깅 기능을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-286">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="c4c72-287">이 섹션의 로깅을 사용 하도록 설정 및 어떻게 로그 알려 SignalR를 사용 하는 다음 전송 방법을 보여 주는 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4c72-287">In this section you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

- <span data-ttu-id="c4c72-288">[Websocket](http://en.wikipedia.org/wiki/WebSocket), IIS 8와 현재 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-288">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>
- <span data-ttu-id="c4c72-289">[서버에서 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events)Internet Explorer 이외의 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-289">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>
- <span data-ttu-id="c4c72-290">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)Internet Explorer에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-290">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>
- <span data-ttu-id="c4c72-291">[Ajax 긴 폴링과](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)모든 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-291">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="c4c72-292">지정된 된 연결에 대 한 SignalR을 지 원하는 서버와 클라이언트 모두 최상의 전송 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-292">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="c4c72-293">열기 *StockTicker.js* 파일의 끝에 있는 연결을 초기화 하는 코드 바로 앞의 로깅을 사용 하도록 설정 하는 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-293">Open *StockTicker.js* and add a line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js)]
2. <span data-ttu-id="c4c72-294">F5 키를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-294">Press F5 to run the project.</span></span>
3. <span data-ttu-id="c4c72-295">브라우저의 개발자 도구 창을 열고 로그를 참조 하 고 콘솔을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-295">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="c4c72-296">Signalr에 대 한 새 연결 전송 방법을 협상의 로그를 보려면 페이지를 새로 고쳐야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-296">You might have to refresh the page to see the logs of Signalr negotiating the transport method for a new connection.</span></span>

    <span data-ttu-id="c4c72-297">Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 Websocket입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-297">If you are running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![IE 10 IIS 8 콘솔](tutorial-server-broadcast-with-signalr/_static/image9.png)

    <span data-ttu-id="c4c72-299">Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 iframe 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-299">If you are running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is iframe.</span></span>

    ![IE 10 콘솔, IIS 7.5](tutorial-server-broadcast-with-signalr/_static/image10.png)

    <span data-ttu-id="c4c72-301">Firefox에서 Firebug 추가 기능 설치 콘솔 창에 얻으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-301">In Firefox, install the Firebug add-in to get a Console window.</span></span> <span data-ttu-id="c4c72-302">Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 Websocket입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-302">If you are running Firefox 19 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-signalr/_static/image11.png)

    <span data-ttu-id="c4c72-304">Windows 7 (IIS 7.5) Firefox 19를 실행 하는 경우 전송 방법은 서버에서 전송 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-304">If you are running Firefox 19 on Windows 7 (IIS 7.5), the transport method is server-sent events.</span></span>

    ![Firefox 19 IIS 7.5 콘솔](tutorial-server-broadcast-with-signalr/_static/image12.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a><span data-ttu-id="c4c72-306">설치 하 고 전체 StockTicker 샘플을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-306">Install and review the full StockTicker sample</span></span>

<span data-ttu-id="c4c72-307">StockTicker 응용 프로그램으로 설치 되는 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지를 처음부터 방금 만든 단순화 된 버전 보다 더 많은 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-307">The StockTicker application that is installed by the [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package includes more features than the simplified version that you just created from scratch.</span></span> <span data-ttu-id="c4c72-308">자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새로운 기능 및 해당 구현 하는 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-308">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span> <span data-ttu-id="c4c72-309">이 자습서의 이전 단계를 수행 하지 않고 패키지를 설치 하는 경우 프로젝트에는 OWIN 시작 클래스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-309">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="c4c72-310">이 단계는 NuGet 패키지의 readme.txt 파일에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-310">This step is explained in the readme.txt file for the NuGet package.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="c4c72-311">SignalR.Sample NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="c4c72-311">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="c4c72-312">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-312">In **Solution Explorer**, right-click the project and click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c4c72-313">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **온라인**, 입력 *SignalR.Sample* 에 **온라인 검색** 상자를 선택한 다음 클릭 **설치** 에 **SignalR.Sample** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-313">In the **Manage NuGet Packages** dialog box, click **Online**, enter *SignalR.Sample* in the **Search Online** box, and then click **Install** in the **SignalR.Sample** package.</span></span>

    ![SignalR.Sample 패키지 설치](tutorial-server-broadcast-with-signalr/_static/image13.png)
3. <span data-ttu-id="c4c72-315">**솔루션 탐색기**를 확장 하 고는 *SignalR.Sample* SignalR.Sample 패키지를 설치 하 여 생성 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-315">In **Solution Explorer**, expand the *SignalR.Sample* folder which was created by installing the SignalR.Sample package.</span></span>
4. <span data-ttu-id="c4c72-316">에 *SignalR.Sample* 폴더를 마우스 오른쪽 단추로 클릭 *StockTicker.html*, 클릭 하 고 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-316">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then click **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4c72-317">SignalR.Sample NuGet 설치 패키지 변경 될 수 있습니다는 버전의 jQuery에서 사용 하 여 *스크립트* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-317">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="c4c72-318">새 *StockTicker.html* 패키지에 설치 하는 파일의 *SignalR.Sample* 폴더가 원래의실행하려면패키지를설치하는jQuery버전와동기화됩니다.*StockTicker.html* 파일을 다시, jQuery 참조는 스크립트 태그를 먼저 업데이트 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-318">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="c4c72-319">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c4c72-319">Run the application</span></span>

1. <span data-ttu-id="c4c72-320">F5 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-320">Press F5 to run the application.</span></span>

    <span data-ttu-id="c4c72-321">표에서 했 듯이 외에도 전체 주식 시세 응용 프로그램에 동일한 주식 데이터를 표시 하는 가로 스크롤 막대가 창을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-321">In addition to the grid that you saw earlier, the full stock ticker application shows a horizontally scrolling window that displays the same stock data.</span></span> <span data-ttu-id="c4c72-322">처음으로 응용 프로그램을 실행 하면 "시장"는 "닫힘" 있는데 정적 그리드 및 없는 스크롤 하는 주식 종목 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-322">When you run the application for the first time, the "market" is "closed" and you see a static grid and a ticker window that isn't scrolling.</span></span>

    ![StockTicker 화면 시작](tutorial-server-broadcast-with-signalr/_static/image14.png)

    <span data-ttu-id="c4c72-324">클릭할 때 **시장**, **주식 시세 라이브** 가로로 스크롤할 수 상자 시작 하 고 서버에 임의의 으로만 주가 변경 사항을 브로드캐스트하는 주기적으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-324">When you click **Open Market**, the **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span> <span data-ttu-id="c4c72-325">주식 시세에서 사용자가 둘 다 변경는 **재고 테이블 라이브** 그리드 및 **주식 시세 라이브** 상자 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-325">Each time a stock price changes, both the **Live Stock Table** grid and the **Live Stock Ticker** box are updated.</span></span> <span data-ttu-id="c4c72-326">특정 주식 가격 변경을 양수 이면 재고는 면 녹색 배경을 표시 및 변경이 음수 이면 재고가 하면 빨간색 배경을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-326">When a stock's price change is positive, the stock is shown with a green background, and when the change is negative, the stock is shown with a red background.</span></span>

    ![StockTicker 앱 시장 열](tutorial-server-broadcast-with-signalr/_static/image15.png)

    <span data-ttu-id="c4c72-328">**닫기 시장** 단추는 변경 내용을 중지 하 고 주식 종목 스크롤 중지 및 **재설정** 가격 시작 되기 전에 단추를 초기 상태로 모든 주식 데이터를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-328">The **Close Market** button stops the changes and stops the ticker scrolling, and the **Reset** button resets all stock data to the initial state before price changes started.</span></span> <span data-ttu-id="c4c72-329">브라우저 창을 열고 동일한 URL로 이동 하는 경우 각 브라우저에서 같은 시간에 동적으로 업데이트 하는 같은 데이터 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-329">If you open more browser windows and go to the same URL, you see the same data dynamically updated at the same time in each browser.</span></span> <span data-ttu-id="c4c72-330">단추 중 하나를 클릭 하면 모든 브라우저 동시에 같은 방법으로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-330">When you click one of the buttons, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="c4c72-331">라이브 주식 종목 표시</span><span class="sxs-lookup"><span data-stu-id="c4c72-331">Live Stock Ticker display</span></span>

<span data-ttu-id="c4c72-332">**주식 시세 라이브** 은 CSS 스타일에 의해 단일 줄으로 포맷 된 div 요소에는 순서가 지정 되지 않은 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-332">The **Live Stock Ticker** display is an unordered list in a div element that is formatted into a single line by CSS styles.</span></span> <span data-ttu-id="c4c72-333">주식 종목 초기화 되 고 동일한 방식으로 테이블을 업데이트:의 자리 표시자를 대체 하 여는 &lt;li&gt; 템플릿 문자열을 동적으로 추가 하는 &lt;li&gt; 요소를 사용 하 여 &lt;ul&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-333">The ticker is initialized and updated the same way as the table: by replacing placeholders in a &lt;li&gt; template string and dynamically adding the &lt;li&gt; elements to the &lt;ul&gt; element.</span></span> <span data-ttu-id="c4c72-334">div. 내에서 순서가 지정 되지 않은 목록의 왼쪽 여백을 변경 하려면 jQuery 애니메이션 효과 주기 함수를 사용 하 여 수행 됩니다 스크롤</span><span class="sxs-lookup"><span data-stu-id="c4c72-334">The scrolling is performed by using the jQuery animate function to vary the margin-left of the unordered list within the div.</span></span>

<span data-ttu-id="c4c72-335">주식 시세 HTML:</span><span class="sxs-lookup"><span data-stu-id="c4c72-335">The stock ticker HTML:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

<span data-ttu-id="c4c72-336">주식 시세 CSS:</span><span class="sxs-lookup"><span data-stu-id="c4c72-336">The stock ticker CSS:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

<span data-ttu-id="c4c72-337">JQuery 코드를 사용 하면를 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-337">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="c4c72-338">클라이언트를 호출할 수 있는 서버에서 추가 메서드</span><span class="sxs-lookup"><span data-stu-id="c4c72-338">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="c4c72-339">StockTickerHub 클래스 클라이언트가 호출할 수 있는 4 개의 추가 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-339">The StockTickerHub class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="c4c72-340">OpenMarket, CloseMarket, 및 재설정 페이지 맨 위에 있는 단추에 대 한 응답으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-340">OpenMarket, CloseMarket, and Reset are called in response to the buttons at the top of the page.</span></span> <span data-ttu-id="c4c72-341">모든 클라이언트에 즉시 전파 되는 상태 변경 트리거 한 클라이언트의 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-341">They demonstrate the pattern of one client triggering a change in state that is immediately propagated to all clients.</span></span> <span data-ttu-id="c4c72-342">이러한 각 방법의에서 메서드를 호출 StockTicker 클래스 인해 영향을 주는 시장 상태 변경 및 새 상태를 다음 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-342">Each of these methods calls a method in the StockTicker class that effects the market state change and then broadcasts the new state.</span></span>

<span data-ttu-id="c4c72-343">StockTicker 클래스에서 시장 상태 MarketState 열거형 값을 반환 하는 MarketState 속성에 의해 유지 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-343">In the StockTicker class, the state of the market is maintained by a MarketState property that returns a MarketState enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="c4c72-344">각 시장 상태를 변경 하는 방법의 잠금 블록 안에 StockTicker 클래스는 threadsafe 해야 하기 때문에 다음과 같이</span><span class="sxs-lookup"><span data-stu-id="c4c72-344">Each of the methods that change the market state do so inside a lock block because the StockTicker class has to be threadsafe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="c4c72-345">이 코드를 threadsafe 되는지는 \_MarketState 속성을 지 원하는 marketState 필드를 volatile로 표시 됩니다</span><span class="sxs-lookup"><span data-stu-id="c4c72-345">To ensure that this code is threadsafe, the \_marketState field that backs the MarketState property is marked as volatile,</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="c4c72-346">BroadcastMarketStateChange 및 BroadcastMarketReset 메서드는 클라이언트에서 정의 된 다른 메서드를 호출 하는 제외 BroadcastStockPrice 메서드가 이미 본 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-346">The BroadcastMarketStateChange and BroadcastMarketReset methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="c4c72-347">서버를 호출할 수 있는 클라이언트에서 추가 기능</span><span class="sxs-lookup"><span data-stu-id="c4c72-347">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="c4c72-348">JQuery.Color를 사용 하 여 색을 빨간색 및 녹색 플래시 및 updateStockPrice 함수는 이제 주식 종목 표시와 눈금을 모두 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-348">The updateStockPrice function now handles both the grid and the ticker display, and it uses jQuery.Color to flash red and green colors.</span></span>

<span data-ttu-id="c4c72-349">새 기능은 *SignalR.StockTicker.js* 설정 / 해제 단추에 따라 상태를 홍보 하는 주식 종목 창 가로 스크롤을 시작 하거나 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-349">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state, and they stop or start the ticker window horizontal scrolling.</span></span> <span data-ttu-id="c4c72-350">여러 함수가 ticker.client에 추가 되 고 되는 [jQuery 확장 함수](http://api.jquery.com/jQuery.extend/) 에 추가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-350">Since multiple functions are being added to ticker.client, the [jQuery extend function](http://api.jquery.com/jQuery.extend/) is used to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="c4c72-351">연결을 설정한 후 추가 클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="c4c72-351">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="c4c72-352">몇 가지 추가 작업을 수행 해야 클라이언트는 연결 되 면, 있기: 시장을 열려 있거나 적절 한 marketOpened 또는 marketClosed 함수를 호출 하 고 단추에 대 한 서버 메서드 호출 연결 하기 위해 닫혀 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-352">After the client establishes the connection, it has some additional work to do: find out if the market is open or closed in order to call the appropriate marketOpened or marketClosed function, and attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="c4c72-353">서버 메서드 반드시 자리까지 나타날 때까지 단추는 연결이 설정 된 후 코드 없습니다 제공 되기 전에 서버 메서드를 호출 하려고 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-353">The server methods are not wired up to the buttons until after the connection is established, so that the code can't try to call the server methods before they are available.</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="c4c72-354">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4c72-354">Next steps</span></span>

<span data-ttu-id="c4c72-355">이 자습서에서는 모든 클라이언트에서 알림에 대 한 응답에서 및 주기적으로 연결 된 모든 클라이언트에 서버에서 메시지를 브로드캐스팅하는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-355">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients, both on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="c4c72-356">다중 스레드 singleton 인스턴스를 사용 하 여 서버 상태를 유지 하는 패턴 사용할 수도 있습니다도 멀티 플레이 온라인 게임 시나리오에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-356">The pattern of using a multi-threaded singleton instance to maintain server state can also be also used in multi-player online game scenarios.</span></span> <span data-ttu-id="c4c72-357">예를 들어 참조 [SignalR을 기반으로 하는 ShootR 게임](https://github.com/NTaylorMullen/ShootR)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-357">For an example, see [the ShootR game that is based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="c4c72-358">피어-투-피어 통신 시나리오를 보여 주는 자습서를 참조 하십시오. [SignalR 시작](introduction-to-signalr.md) 및 [SignalR로 실시간 업데이트](tutorial-high-frequency-realtime-with-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-358">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="c4c72-359">SignalR 개발 보다 발전된 된 개념을 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4c72-359">To learn more advanced SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="c4c72-360">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="c4c72-360">ASP.NET SignalR</span></span>](../../index.md)
- [<span data-ttu-id="c4c72-361">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c4c72-361">SignalR Project</span></span>](http://signalr.net/)
- [<span data-ttu-id="c4c72-362">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="c4c72-362">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="c4c72-363">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="c4c72-363">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

<span data-ttu-id="c4c72-364">SignalR 응용 프로그램을 Azure에 배포 하는 방법에 대 한 연습을을 참조 하십시오. [Azure 앱 서비스의 웹 앱과 함께 사용 하 여 SignalR](../deployment/using-signalr-with-azure-web-sites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-364">For a walkthrough on how to deploy a SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="c4c72-365">Visual Studio 웹 프로젝트는 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 앱 서비스에서 ASP.NET 웹 앱을 만들](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4c72-365">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/).</span></span>
