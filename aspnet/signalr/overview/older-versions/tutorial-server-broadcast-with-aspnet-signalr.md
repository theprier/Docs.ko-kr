---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: '자습서: ASP.NET SignalR을 사용 하 여 서버 브로드캐스트 1.x | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 ASP.NET SignalR을 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스트는 communic 의미 하는 중...
ms.author: riande
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 7d604af11ade848358e291d1df25f2f8df850132
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48911983"
---
<a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a><span data-ttu-id="a755c-104">자습서: ASP.NET SignalR을 사용 하 여 서버 브로드캐스트 1.x</span><span class="sxs-lookup"><span data-stu-id="a755c-104">Tutorial: Server Broadcast with ASP.NET SignalR 1.x</span></span>
====================
<span data-ttu-id="a755c-105">하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a755c-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="a755c-106">이 자습서에는 ASP.NET SignalR을 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide server broadcast functionality.</span></span> <span data-ttu-id="a755c-107">서버 브로드캐스트 클라이언트로 전송 되는 통신 서버에서 시작 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-107">Server broadcast means that communications sent to clients are initiated by the server.</span></span> <span data-ttu-id="a755c-108">이 시나리오에는 클라이언트로 전송 되는 통신 클라이언트 중 하나 이상으로 시작 되는 채팅 응용 프로그램과 같은 피어-투-피어 시나리오 보다 다른 프로그래밍 접근 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-108">This scenario requires a different programming approach than peer-to-peer scenarios such as chat applications, in which communications sent to clients are initiated by one or more of the clients.</span></span>
> 
> <span data-ttu-id="a755c-109">이 자습서에서 만들어야 하는 응용 프로그램 주식 시세 표시기, 서버 브로드캐스트 기능에 대 한 일반적인 시나리오를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-109">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span>
> 
> <span data-ttu-id="a755c-110">이 자습서에 대 한 의견을 기다리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-110">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="a755c-111">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-111">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>


## <a name="overview"></a><span data-ttu-id="a755c-112">개요</span><span class="sxs-lookup"><span data-stu-id="a755c-112">Overview</span></span>

<span data-ttu-id="a755c-113">합니다 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지는 Visual Studio 프로젝트에 시뮬레이션 된 샘플 주식 시세 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-113">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package installs a sample simulated stock ticker application in a Visual Studio project.</span></span> <span data-ttu-id="a755c-114">이 자습서의 첫 번째 부분에서는 해당 응용 프로그램의 단순화 된 버전부터에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-114">In the first part of this tutorial, you'll create a simplified version of that application from scratch.</span></span> <span data-ttu-id="a755c-115">자습서의 나머지 부분에서는 NuGet 패키지를 설치 하 고 추가 기능 및 생성 된 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-115">In the remainder of the tutorial, you'll install the NuGet package and review the additional features and code that it creates.</span></span>

<span data-ttu-id="a755c-116">주식 시세 응용 프로그램이 하려는 "푸시" 또는 브로드캐스트 알림 주기적으로 모든 연결 된 클라이언트에 서버에서 실시간 응용 프로그램의 종류를 대표 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-116">The stock ticker application is a representative of a kind of real-time application in which you want to periodically "push," or broadcast, notifications from the server to all connected clients.</span></span>

<span data-ttu-id="a755c-117">이 자습서의 첫 번째 부분에서 빌드할 응용 프로그램 주식 데이터를 사용 하 여 표를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-117">The application that you'll build in the first part of this tutorial displays a grid with stock data.</span></span>

![StockTicker 초기 버전](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

<span data-ttu-id="a755c-119">정기적으로 서버 임의로 주식 시세를 업데이트 하 고 모든 연결 된 클라이언트에 업데이트를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-119">Periodically the server randomly updates stock prices and pushes the updates to all connected clients.</span></span> <span data-ttu-id="a755c-120">브라우저 숫자 및 기호에는 **변경** 하 고 **%** 열 서버에서 알림에 대 한 응답으로 동적으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-120">In the browser the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="a755c-121">경우 모두 동일한 데이터 및 표시 데이터에 동일한 변경 내용을 동시에 동일한 URL로 브라우저를 추가로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-121">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

<span data-ttu-id="a755c-122">이 자습서는 다음 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-122">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="a755c-123">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a755c-123">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="a755c-124">프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="a755c-124">Create the project</span></span>](#createproject)
- [<span data-ttu-id="a755c-125">SignalR NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="a755c-125">Add the SignalR NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="a755c-126">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="a755c-126">Set up the server code</span></span>](#server)
- [<span data-ttu-id="a755c-127">클라이언트 코드를 설정 하기</span><span class="sxs-lookup"><span data-stu-id="a755c-127">Set up the client code</span></span>](#client)
- [<span data-ttu-id="a755c-128">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="a755c-128">Test the application</span></span>](#test)
- [<span data-ttu-id="a755c-129">로깅을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a755c-129">Enable logging</span></span>](#enablelogging)
- [<span data-ttu-id="a755c-130">설치 하 고 전체 StockTicker 샘플을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-130">Install and review the full StockTicker sample</span></span>](#fullsample)
- [<span data-ttu-id="a755c-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a755c-131">Next steps</span></span>](#nextsteps)

> [!NOTE]
> <span data-ttu-id="a755c-132">응용 프로그램을 구축 하는 단계를 진행 하지 않으려는 경우 새 SignalR.Sample 패키지를 설치할 수 있습니다 **빈 ASP.NET 웹 응용 프로그램** 프로젝트 및 코드를 설명 하려면 다음이 단계를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="a755c-132">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new **Empty ASP.NET Web Application** project, and read through these steps to get explanations of the code.</span></span> <span data-ttu-id="a755c-133">자습서의 첫 번째 부분에서는 SignalR.Sample 코드의 하위 집합 및 두 번째 부분은 SignalR.Sample 패키지에 추가 기능의 주요 기능에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-133">The first part of the tutorial covers a subset of the SignalR.Sample code, and the second part explains key features of the additional functionality in the SignalR.Sample package.</span></span>


<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="a755c-134">전제 조건</span><span class="sxs-lookup"><span data-stu-id="a755c-134">Prerequisites</span></span>

<span data-ttu-id="a755c-135">시작 하기 전에 Visual Studio 2012 또는 2010 SP1이 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-135">Before you start, make sure that you have Visual Studio 2012 or 2010 SP1 installed on your computer.</span></span> <span data-ttu-id="a755c-136">Visual Studio가 없는 경우 [ASP.NET 다운로드](https://www.asp.net/downloads) 웹에 대 한 무료 Visual Studio 2012 Express를 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-136">If you don't have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express for Web.</span></span>

<span data-ttu-id="a755c-137">Visual Studio 2010 경우 했는지 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-137">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="a755c-138">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-138">Create the project</span></span>

1. <span data-ttu-id="a755c-139">**파일** 메뉴 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-139">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="a755c-140">에 **새 프로젝트** 대화 상자에서 **C#** 아래에 있는 **템플릿** 선택한 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-140">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="a755c-141">선택 된 **ASP.NET 빈 웹 응용 프로그램** 서식 파일을 프로젝트의 이름 *SignalR.StockTicker*, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-141">Select the **ASP.NET Empty Web Application** template, name the project *SignalR.StockTicker*, and click **OK**.</span></span>

    ![새 프로젝트 대화 상자](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a><span data-ttu-id="a755c-143">SignalR NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="a755c-143">Add the SignalR NuGet Packages</span></span>

### <a name="add-the-signalr-and-jquery-nuget-packages"></a><span data-ttu-id="a755c-144">SignalR 및 JQuery NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="a755c-144">Add the SignalR and JQuery NuGet Packages</span></span>

<span data-ttu-id="a755c-145">프로젝트에 NuGet 패키지를 설치 하 여 SignalR 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-145">You can add SignalR functionality to a project by installing a NuGet package.</span></span>

1. <span data-ttu-id="a755c-146">클릭 **도구 | NuGet 패키지 관리자 | 패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-146">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="a755c-147">패키지 관리자에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-147">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    <span data-ttu-id="a755c-148">SignalR 패키지 종속성으로 다양 한 다른 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-148">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="a755c-149">설치가 완료 되는 경우 모든 ASP.NET 응용 프로그램에서 SignalR을 사용 하는 데 필요한 서버 및 클라이언트 구성 요소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-149">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>

<a id="server"></a>

## <a name="set-up-the-server-code"></a><span data-ttu-id="a755c-150">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="a755c-150">Set up the server code</span></span>

<span data-ttu-id="a755c-151">이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-151">In this section you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="a755c-152">재고 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="a755c-152">Create the Stock class</span></span>

<span data-ttu-id="a755c-153">저장 하 고 주식에 대 한 정보를 전송 하는 데 사용할 수 있는 재고 모델 클래스를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-153">You begin by creating the Stock model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="a755c-154">프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *Stock.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-154">Create a new class file in the project folder, name it *Stock.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    <span data-ttu-id="a755c-155">주식을 만들 때 설정 하는 두 속성은 기호 (예: microsoft MSFT) 및 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-155">The two properties that you'll set when you create stocks are the Symbol (for example, MSFT for Microsoft) and the Price.</span></span> <span data-ttu-id="a755c-156">다른 속성 가격을 설정 하는 방법 및 시기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-156">The other properties depend on how and when you set Price.</span></span> <span data-ttu-id="a755c-157">처음 가격을 설정할 값을 가져옵니다 DayOpen에 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-157">The first time you set Price, the value gets propagated to DayOpen.</span></span> <span data-ttu-id="a755c-158">가격 및 DayOpen 간의 차이 기반으로 이후 시간 변경 가격을 설정 하면 시간과 PercentChange 속성 값이 계산 되 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-158">Subsequent times when you set Price, the Change and PercentChange property values are calculated based on the difference between Price and DayOpen.</span></span>

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a><span data-ttu-id="a755c-159">StockTicker 및 StockTickerHub 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="a755c-159">Create the StockTicker and StockTickerHub classes</span></span>

<span data-ttu-id="a755c-160">서버와 클라이언트 간 상호 작용을 처리 하는 SignalR 허브 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-160">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="a755c-161">SignalR 허브 클래스에서 파생 된 StockTickerHub 클래스는 클라이언트에서 연결 및 메서드 호출 수신을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-161">A StockTickerHub class that derives from the SignalR Hub class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="a755c-162">또한 주식 데이터를 유지 관리 하 고 주기적으로 클라이언트 연결 독립적으로 가격 업데이트를 트리거하는 타이머 개체를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-162">You also need to maintain stock data and run a Timer object to periodically trigger price updates, independently of client connections.</span></span> <span data-ttu-id="a755c-163">허브 인스턴스는 일시적 이므로 허브 클래스에서 이러한 함수를 넣을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-163">You can't put these functions in a Hub class, because Hub instances are transient.</span></span> <span data-ttu-id="a755c-164">허브 클래스 인스턴스를 연결 및 서버에 클라이언트에서 호출 같은 허브에 대 한 각 작업에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-164">A Hub class instance is created for each operation on the hub, such as connections and calls from the client to the server.</span></span> <span data-ttu-id="a755c-165">따라서는 주식 데이터를 유지 하 고, 가격을 업데이트, 가격 업데이트 브로드캐스트 메커니즘 StockTicker 이름을 지정할 수 있는 별도 클래스에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-165">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class, which you'll name StockTicker.</span></span>

![StockTicker에서 브로드캐스트](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

<span data-ttu-id="a755c-167">Singleton StockTicker 인스턴스에 대 한 참조를 각 StockTickerHub 인스턴스에서 설정 해야 하므로 서버에서 실행 하려면 StockTicker 클래스의 인스턴스가 하나씩만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-167">You only want one instance of the StockTicker class to run on the server, so you'll need to set up a reference from each StockTickerHub instance to the singleton StockTicker instance.</span></span> <span data-ttu-id="a755c-168">StockTicker 클래스는 주식 데이터 수 있고 업데이트를 트리거 아닌 StockTicker 허브 클래스 때문에 클라이언트에 브로드캐스트할 수 있게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-168">The StockTicker class has to be able to broadcast to clients because it has the stock data and triggers updates, but StockTicker is not a Hub class.</span></span> <span data-ttu-id="a755c-169">따라서 StockTicker 클래스는 SignalR 허브 연결 컨텍스트 개체에 대 한 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-169">Therefore, the StockTicker class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="a755c-170">SignalR 연결 컨텍스트 개체 다음 클라이언트로 브로드캐스트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-170">It can then use the SignalR connection context object to broadcast to clients.</span></span>

1. <span data-ttu-id="a755c-171">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **새 항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-171">In **Solution Explorer**, right-click the project and click **Add New Item**.</span></span>
2. <span data-ttu-id="a755c-172">Visual Studio 2012을 사용 하는 경우는 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=279941), 클릭 **웹** 아래에서 **Visual C#** 선택 하 고는 **SignalR 허브 클래스** 항목 템플릿.</span><span class="sxs-lookup"><span data-stu-id="a755c-172">If you have Visual Studio 2012 with the [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=279941), click **Web** under **Visual C#** and select the **SignalR Hub Class** item template.</span></span> <span data-ttu-id="a755c-173">그렇지 않은 경우 선택 합니다 **클래스** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="a755c-173">Otherwise, select the **Class** template.</span></span>
3. <span data-ttu-id="a755c-174">새 클래스 이름을 *StockTickerHub.cs*를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-174">Name the new class *StockTickerHub.cs*, and then click **Add**.</span></span>

    ![StockTickerHub.cs 추가](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. <span data-ttu-id="a755c-176">템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-176">Replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    <span data-ttu-id="a755c-177">합니다 [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스는 클라이언트가 서버에서 호출할 수는 메서드를 정의 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-177">The [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class is used to define methods the clients can call on the server.</span></span> <span data-ttu-id="a755c-178">하나의 메서드를 정의 하는: `GetAllStocks()`합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-178">You are defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="a755c-179">처음에 클라이언트가 서버에 연결할 때 현재 가격을 사용 하 여 주식의 모든 목록을 가져오려면이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-179">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="a755c-180">메서드는 동기적으로 실행 하 고 반환할 수 `IEnumerable<Stock>` 메모리에서 데이터를 반환 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-180">The method can execute synchronously and return `IEnumerable<Stock>` because it is returning data from memory.</span></span> <span data-ttu-id="a755c-181">메서드를 대기 데이터베이스 조회 또는 웹 서비스 호출 등을 포함 하는 것을 수행 하 여 데이터를 가져올 해야 하는 경우 지정 `Task<IEnumerable<Stock>>` 비동기 처리를 사용 하도록 설정 하려면 반환 값으로.</span><span class="sxs-lookup"><span data-stu-id="a755c-181">If the method had to get the data by doing something that would involve waiting, such as a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="a755c-182">자세한 내용은 [ASP.NET SignalR 허브 API 가이드-서버-비동기적으로 실행 하는 경우](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-182">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](index.md).</span></span>

    <span data-ttu-id="a755c-183">HubName 특성 클라이언트에서 JavaScript 코드에서 허브를 참조 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-183">The HubName attribute specifies how the Hub will be referenced in JavaScript code on the client.</span></span> <span data-ttu-id="a755c-184">이 특성을 사용 하지 않는 경우 클라이언트의 기본 이름은 stockTickerHub 것이 경우 클래스 이름의 카멜식 대 / 소문자 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-184">The default name on the client if you don't use this attribute is a camel-cased version of the class name, which in this case would be stockTickerHub.</span></span>

    <span data-ttu-id="a755c-185">알 수 있듯이 나중 StockTicker 클래스를 만들 때, 정적 인스턴스 속성에 해당 클래스의 singleton 인스턴스로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-185">As you'll see later when you create the StockTicker class, a singleton instance of that class is created in its static Instance property.</span></span> <span data-ttu-id="a755c-186">얼마나 많은 클라이언트가 연결 또는 연결 끊기에 관계 없이 메모리에 유지 됩니다 StockTicker의 singleton 인스턴스를 해당 인스턴스에 GetAllStocks 메서드는 현재 주식 정보를 반환 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-186">That singleton instance of StockTicker remains in memory no matter how many clients connect or disconnect, and that instance is what the GetAllStocks method uses to return current stock information.</span></span>
5. <span data-ttu-id="a755c-187">프로젝트 폴더에 새 클래스 파일을 만들고, 이름을 *StockTicker.cs*, 다음 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-187">Create a new class file in the project folder, name it *StockTicker.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    <span data-ttu-id="a755c-188">여러 스레드가 동일한 인스턴스의 StockTicker 코드를 실행 하 고는, 있으므로 StockTicker 클래스는 threadsafe 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-188">Since multiple threads will be running the same instance of StockTicker code, the StockTicker class has to be threadsafe.</span></span>

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="a755c-189">정적 필드의 singleton 인스턴스를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-189">Storing the singleton instance in a static field</span></span>

    <span data-ttu-id="a755c-190">코드를 정적 초기화 \_클래스의이 인스턴스를 사용 하 여 인스턴스 속성을 지 원하는 인스턴스 필드 이므로 만들 수 있는 클래스의 유일한 인스턴스 생성자를 private로 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-190">The code initializes the static \_instance field that backs the Instance property with an instance of the class, and this is the only instance of the class that can be created, because the constructor is marked as private.</span></span> <span data-ttu-id="a755c-191">[초기화 지연](https://msdn.microsoft.com/library/dd997286.aspx) 에 사용 되는 \_없습니다 성능상의 이유로 인스턴스 생성 threadsafe 인지를 확인 하지만 인스턴스 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-191">[Lazy initialization](https://msdn.microsoft.com/library/dd997286.aspx) is used for the \_instance field, not for performance reasons but to ensure that the instance creation is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    <span data-ttu-id="a755c-192">클라이언트가 서버에 연결 될 때마다 별도 스레드에서 실행 StockTickerHub 클래스의 새 인스턴스를 StockTicker singleton 인스턴스를 가져옵니다 StockTicker.Instance 정적 속성에서 StockTickerHub 클래스 앞 부분에서 살펴본 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-192">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the StockTicker.Instance static property, as you saw earlier in the StockTickerHub class.</span></span>

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="a755c-193">ConcurrentDictionary 주식 데이터를 저장</span><span class="sxs-lookup"><span data-stu-id="a755c-193">Storing stock data in a ConcurrentDictionary</span></span>

    <span data-ttu-id="a755c-194">생성자는 초기화는 \_주식 컬렉션은 몇 가지 샘플 주식 데이터와 GetAllStocks 주식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-194">The constructor initializes the \_stocks collection with some sample stock data, and GetAllStocks returns the stocks.</span></span> <span data-ttu-id="a755c-195">앞서 살펴본 것 처럼이 컬렉션의 재고 StockTickerHub.GetAllStocks 클라이언트가 호출할 수 있는 허브 클래스에는 서버 메서드는에서 다시 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-195">As you saw earlier, this collection of stocks is in turn returned by StockTickerHub.GetAllStocks which is a server method in the Hub class that clients can call.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    <span data-ttu-id="a755c-196">주식 컬렉션으로 정의 되는 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 스레드로부터의 안전성에 대 한 형식.</span><span class="sxs-lookup"><span data-stu-id="a755c-196">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="a755c-197">사용할 수 있습니다는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 명시적으로 변경 되도록 하는 경우 사전을 잠금.</span><span class="sxs-lookup"><span data-stu-id="a755c-197">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

    <span data-ttu-id="a755c-198">이 샘플 응용 프로그램에 대 한 것이 확인 응용 프로그램 데이터를 메모리에 저장 하는 데 StockTicker 인스턴스가 삭제 될 때 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-198">For this sample application, it's OK to store application data in memory and to lose the data when the StockTicker instance is disposed.</span></span> <span data-ttu-id="a755c-199">실제 응용 프로그램에서 데이터베이스와 같은 백 엔드 데이터 저장소를 사용 하 여 작업할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-199">In a real application you would work with a back-end data store such as a database.</span></span>

    ### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="a755c-200">주식 시세를 정기적으로 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="a755c-200">Periodically updating stock prices</span></span>

    <span data-ttu-id="a755c-201">생성자를 주기적으로 임의 기준 주식 시세를 업데이트 하는 메서드를 호출 하는 타이머를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-201">The constructor starts up a Timer object that periodically calls methods that update stock prices on a random basis.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    <span data-ttu-id="a755c-202">UpdateStockPrices는 state 매개 변수에 null을 전달 하는 타이머에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-202">UpdateStockPrices is called by the Timer, which passes in null in the state parameter.</span></span> <span data-ttu-id="a755c-203">가격을 업데이트 하기 전에 잠금을에서 수행 되는 \_updateStockPricesLock 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-203">Before updating prices, a lock is taken on the \_updateStockPricesLock object.</span></span> <span data-ttu-id="a755c-204">코드를 다른 스레드를 가격을 업데이트 하 고 목록의 각 주식에 TryUpdateStockPrice 호출 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-204">The code checks if another thread is already updating prices, and then it calls TryUpdateStockPrice on each stock in the list.</span></span> <span data-ttu-id="a755c-205">TryUpdateStockPrice 메서드 주가 변경할지 여부를 결정 및 변경 하려면 얼마나 많은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-205">The TryUpdateStockPrice method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="a755c-206">주가 변경 되 면 모든 연결 된 클라이언트에 주식 가격 변동 브로드캐스트하 BroadcastStockPrice 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-206">If the stock price is changed, BroadcastStockPrice is called to broadcast the stock price change to all connected clients.</span></span>

    <span data-ttu-id="a755c-207">합니다 \_updatingStockPrices 플래그로 표시 됩니다 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) 액세스할 threadsafe 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-207">The \_updatingStockPrices flag is marked as [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to ensure that access to it is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    <span data-ttu-id="a755c-208">실제 응용 프로그램에서는 TryUpdateStockPrice 메서드; 가격을 조회 하는 웹 서비스 호출 이 코드에서 임의로 변경할 난수 생성기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-208">In a real application, the TryUpdateStockPrice method would call a web service to look up the price; in this code it uses a random number generator to make changes randomly.</span></span>

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="a755c-209">클라이언트에 StockTicker 클래스 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기</span><span class="sxs-lookup"><span data-stu-id="a755c-209">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

    <span data-ttu-id="a755c-210">가격이 변경 StockTicker 개체 여기 나오는, 때문에 연결 된 모든 클라이언트에서 updateStockPrice 메서드를 호출 해야 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-210">Because the price changes originate here in the StockTicker object, this is the object that needs to call an updateStockPrice method on all connected clients.</span></span> <span data-ttu-id="a755c-211">허브 클래스에서 클라이언트 메서드를 호출 하는 것에 대 한 API는 있지만 StockTicker 허브 클래스에서 파생 되지 않습니다 및 Hub 개체에 대 한 참조는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-211">In a Hub class you have an API for calling client methods, but StockTicker does not derive from the Hub class and does not have a reference to any Hub object.</span></span> <span data-ttu-id="a755c-212">따라서 연결 된 클라이언트에 브로드캐스트를 위해 StockTicker 클래스를 StockTickerHub 클래스에 대 한 SignalR 컨텍스트 인스턴스를 가져오고 클라이언트에서 메서드를 호출 하는 데는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-212">Therefore, in order to broadcast to connected clients, the StockTicker class has to get the SignalR context instance for the StockTickerHub class and use that to call methods on clients.</span></span>

    <span data-ttu-id="a755c-213">생성자에 전달 참조 하는 단일 클래스 인스턴스를 만들 때 코드는 SignalR 컨텍스트에 대 한 참조를 가져옵니다 하 고 생성자 클라이언트 속성에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-213">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the Clients property.</span></span>

    <span data-ttu-id="a755c-214">두 가지 컨텍스트를 한 번만 가져올 하려는 이유:은 비용이 많이 드는 작업 컨텍스트 가져오기 및 클라이언트에 전송 된 메시지의 의도 된 순서 유지는 하면 한 번 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-214">There are two reasons why you want to get the context just once: getting the context is an expensive operation, and getting it once ensures that the intended order of messages sent to clients is preserved.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    <span data-ttu-id="a755c-215">컨텍스트의 클라이언트 속성을 가져오고 StockTickerClient 속성에 배치 메서드를 호출할 클라이언트 허브 클래스에서와 동일 하 게 표시 하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-215">Getting the Clients property of the context and putting it in the StockTickerClient property lets you write code to call client methods that looks the same as it would in a Hub class.</span></span> <span data-ttu-id="a755c-216">예를 들어 모든 클라이언트에 브로드캐스트 Clients.All.updateStockPrice(stock) 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-216">For instance, to broadcast to all clients you can write Clients.All.updateStockPrice(stock).</span></span>

    <span data-ttu-id="a755c-217">BroadcastStockPrice를 호출 하는 updateStockPrice 메서드가 아직 존재 하지 않습니다. 클라이언트에서 실행 되는 코드를 작성 하는 경우 나중에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-217">The updateStockPrice method that you are calling in BroadcastStockPrice doesn't exist yet; you'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="a755c-218">Clients.All 런타임에 식을 평가할 즉 동적 이므로 여기 updateStockPrice를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-218">You can refer to updateStockPrice here because Clients.All is dynamic, which means the expression will be evaluated at runtime.</span></span> <span data-ttu-id="a755c-219">이 메서드 호출은 실행 되 면 SignalR 메서드 이름과 매개 변수 값을 클라이언트에 보내고 클라이언트 updateStockPrice 메서드가 있으면 해당 메서드가 호출 됩니다 및 매개 변수 값에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-219">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named updateStockPrice, that method will be called and the parameter value will be passed to it.</span></span>

    <span data-ttu-id="a755c-220">Clients.All 모든 클라이언트에 보내는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-220">Clients.All means send to all clients.</span></span> <span data-ttu-id="a755c-221">SignalR은 클라이언트 또는 클라이언트에 보낼 그룹 지정을 다른 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-221">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="a755c-222">자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-222">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="a755c-223">SignalR 경로 등록</span><span class="sxs-lookup"><span data-stu-id="a755c-223">Register the SignalR route</span></span>

<span data-ttu-id="a755c-224">서버를 가로채 고 signalr 직접 URL을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-224">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="a755c-225">일부 코드를 추가 하는 작업을 수행 하는 *Global.asax* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-225">To do that you'll add some code to the *Global.asax* file.</span></span>

1. <span data-ttu-id="a755c-226">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **새 항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-226">In **Solution Explorer**, right-click the project, and then click **Add New Item**.</span></span>
2. <span data-ttu-id="a755c-227">선택 된 **전역 응용 프로그램 클래스** 템플릿 항목을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-227">Select the **Global Application Class** item template, and then click **Add**.</span></span>

    ![Global.asax 추가](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. <span data-ttu-id="a755c-229">SignalR 경로 등록 코드를 응용 프로그램에 추가\_메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-229">Add the SignalR route registration code to the Application\_Start method:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    <span data-ttu-id="a755c-230">기본적으로 모든 SignalR 트래픽에 대 한 기본 URL은 "/ signalr", "/ signalr 허브"는 응용 프로그램에 있는 모든 허브에 대 한 프록시를 정의 하는 동적으로 생성 된 JavaScript 파일을 검색 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-230">By default, the base URL for all SignalR traffic is "/signalr", and "/signalr/hubs" is used to retrieve a dynamically generated JavaScript file that defines proxies for all the Hubs you have in your application.</span></span> <span data-ttu-id="a755c-231">MapHubs 메서드 인스턴스의 다양 한 기본 URL 및 특정 SignalR 옵션을 지정할 수 있는 오버 로드를 포함 합니다 [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-231">The MapHubs method includes overloads that let you specify a different base URL and certain SignalR options in an instance of the [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) class.</span></span>
4. <span data-ttu-id="a755c-232">추가 하 여 파일의 맨 위에 있는 문.</span><span class="sxs-lookup"><span data-stu-id="a755c-232">Add a using statement at the top of the file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. <span data-ttu-id="a755c-233">저장 후 닫기 합니다 *Global.asax* 파일과 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-233">Save and close the *Global.asax* file, and build the project.</span></span>

<span data-ttu-id="a755c-234">이제 서버 코드가 설정을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-234">You have now completed setting up the server code.</span></span> <span data-ttu-id="a755c-235">다음 섹션에서 클라이언트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-235">In the next section you'll set up the client.</span></span>

<a id="client"></a>

## <a name="set-up-the-client-code"></a><span data-ttu-id="a755c-236">클라이언트 코드를 설정 하기</span><span class="sxs-lookup"><span data-stu-id="a755c-236">Set up the client code</span></span>

1. <span data-ttu-id="a755c-237">프로젝트 폴더에 새 HTML 파일을 만들고 이름을 *StockTicker.html*합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-237">Create a new HTML file in the project folder, and name it *StockTicker.html*.</span></span>
2. <span data-ttu-id="a755c-238">템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-238">Replace the template code with the following code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    <span data-ttu-id="a755c-239">HTML 5 개 열, 하나의 머리글 행 및 5 개 열에 모두 걸친 단일 셀을 사용 하 여 데이터 행을 사용 하 여 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-239">The HTML creates a table with 5 columns, a header row, and a data row with a single cell that spans all 5 columns.</span></span> <span data-ttu-id="a755c-240">데이터 행 "로드 중..."를 표시 되 고 일시적으로 응용 프로그램을 시작 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-240">The data row displays "loading..." and will only be shown momentarily when the application starts.</span></span> <span data-ttu-id="a755c-241">JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 하는 주식 데이터를 사용 하 여 해당 내부 행에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="a755c-242">스크립트 태그는 jQuery 스크립트 파일, SignalR core 스크립트 파일, SignalR 프록시 스크립트 파일 및 나중에 만들 StockTicker 스크립트 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-242">The script tags specify the jQuery script file, the SignalR core script file, the SignalR proxies script file, and a StockTicker script file that you'll create later.</span></span> <span data-ttu-id="a755c-243">"/ Signalr 허브" URL을 지정 하는 SignalR 프록시 스크립트 파일을 동적으로 생성 및 StockTickerHub.GetAllStocks에 대 한이 경우 허브 클래스의 메서드에 대 한 프록시 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-243">The SignalR proxies script file, which specifies the "/signalr/hubs" URL, is dynamically generated and defines proxy methods for the methods on the Hub class, in this case for StockTickerHub.GetAllStocks.</span></span> <span data-ttu-id="a755c-244">원하는 경우 수동으로 생성할 수 있습니다이 JavaScript 파일을 사용 하 여 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) MapHubs 메서드 호출의 동적 파일 생성을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-244">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) and disable dynamic file creation in the MapHubs method call.</span></span>
3. > [!IMPORTANT]
   > <span data-ttu-id="a755c-245">JavaScript 파일에 참조 하는지 확인 *StockTicker.html* 올바릅니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-245">Make sure that the JavaScript file references in *StockTicker.html* are correct.</span></span> <span data-ttu-id="a755c-246">즉, jQuery 버전 스크립트 태그 (예에서 1.8.2)에서 프로젝트의 jQuery 버전과 동일 인지를 확인 *스크립트* 폴더, 스크립트 태그에서 SignalR 버전 SignalR 동일 인지 확인 하 고 프로젝트의 버전 *스크립트* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-246">That is, make sure that the jQuery version in your script tag (1.8.2 in the example) is the same as the jQuery version in your project's *Scripts* folder, and make sure that the SignalR version in your script tag is the same as the SignalR version in your project's *Scripts* folder.</span></span> <span data-ttu-id="a755c-247">필요한 경우 스크립트 태그의 파일 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-247">Change the file names in the script tags if necessary.</span></span>
4. <span data-ttu-id="a755c-248">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 클릭 하 고 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-248">In **Solution Explorer**, right-click *StockTicker.html*, and then click **Set as Start Page**.</span></span>
5. <span data-ttu-id="a755c-249">프로젝트 폴더에 새 JavaScript 파일을 만들고 이름을 *StockTicker.js*...</span><span class="sxs-lookup"><span data-stu-id="a755c-249">Create a new JavaScript file in the project folder and name it *StockTicker.js*..</span></span>
6. <span data-ttu-id="a755c-250">템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-250">Replace the template code with the following code:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    <span data-ttu-id="a755c-251">$.connection SignalR 프록시를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-251">$.connection refers to the SignalR proxies.</span></span> <span data-ttu-id="a755c-252">코드는 StockTickerHub 클래스에 대 한 프록시에 대 한 참조를 가져오고 전광판 변수에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-252">The code gets a reference to the proxy for the StockTickerHub class and puts it in the ticker variable.</span></span> <span data-ttu-id="a755c-253">프록시 이름은 [HubName] 특성으로 설정 된 이름:</span><span class="sxs-lookup"><span data-stu-id="a755c-253">The proxy name is the name that was set by the [HubName] attribute:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    <span data-ttu-id="a755c-254">모든 변수 및 함수를 정의한 후 파일의 코드의 마지막 줄 SignalR 시작 함수를 호출 하 여 SignalR 연결을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-254">After all the variables and functions are defined, the last line of code in the file initializes the SignalR connection by calling the SignalR start function.</span></span> <span data-ttu-id="a755c-255">시작 함수가 비동기적으로 실행 하 고 반환 된 [jQuery 지연 개체](http://api.jquery.com/category/deferred-object/), 비동기 작업이 완료 될 때 호출할 함수를 지정 하려면 완료 함수를 호출할 수 있다는 의미입니다...</span><span class="sxs-lookup"><span data-stu-id="a755c-255">The start function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means you can call the done function to specify the function to call when the asynchronous operation is completed..</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    <span data-ttu-id="a755c-256">Init 함수 서버의 getAllStocks 함수를 호출 하 고 서버 재고 테이블을 업데이트 하려면 반환 된 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-256">The init function calls the getAllStocks function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="a755c-257">기본적으로 사용 해야 카멜식 대/소문자 클라이언트에서 서버의 파스칼식 되어도 메서드 이름을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-257">Notice that by default, you have to use camel casing on the client although the method name is pascal-cased on the server.</span></span> <span data-ttu-id="a755c-258">카멜식 대/소문자 규칙 메서드를 개체가 아닌에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-258">The camel-casing rule only applies to methods, not objects.</span></span> <span data-ttu-id="a755c-259">예를 들어, 재고를 참조할 수도 있습니다. 기호 및 stock 합니다. 가격, stock.symbol 않거나 stock.price 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-259">For example, you refer to stock.Symbol and stock.Price, not stock.symbol or stock.price.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    <span data-ttu-id="a755c-260">클라이언트에서 파스칼식 대/소문자를 사용 하려는 경우 완전히 다른 메서드 이름을 사용 하려는 경우 있습니다 수 메서드를 데코레이팅합니다 허브 HubMethodName 특성을 사용 하 여 동일한 방식으로 HubName 특성을 사용 하 여 허브 클래스 자체 장식 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-260">If you wanted to use pascal casing on the client, or if you wanted to use a completely different method name, you could decorate the Hub method with the HubMethodName attribute the same way you decorated the Hub class itself with the HubName attribute.</span></span>

    <span data-ttu-id="a755c-261">Init 메서드에서 테이블 행에 대 한 HTML 주식 개체의 형식 속성을 호출 formatStock 하 여 서버에서 받은 각 주식 개체에 대해 생성 되 고 호출 하 여 다음 기능이 (맨 위에 있는 정의 된 *StockTicker.js*) 자리 표시자를 바꿔야 rowTemplate 변수에 주식 개체 속성 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-261">In the init method, HTML for a table row is created for each stock object received from the server by calling formatStock to format properties of the stock object, and then by calling supplant (which is defined at the top of *StockTicker.js*) to replace placeholders in the rowTemplate variable with the stock object property values.</span></span> <span data-ttu-id="a755c-262">그런 다음 결과 HTML은 주식 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-262">The resulting HTML is then appended to the stock table.</span></span>

    <span data-ttu-id="a755c-263">비동기 시작 함수가 완료 된 후 실행 되는 콜백 함수에 전달 하 여 init를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-263">You call init by passing it in as a callback function that executes after the asynchronous start function completes.</span></span> <span data-ttu-id="a755c-264">시작을 호출한 후는 별도 JavaScript 문으로 init를 호출 하면 함수는 연결을 완료 하는 시작 함수를 기다리지 않고 즉시 실행 됩니다 때문에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-264">If you called init as a separate JavaScript statement after calling start, the function would fail because it would execute immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="a755c-265">이런 경우는 init 함수 서버 연결이 설정 되기 전에 getAllStocks 함수를 호출 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-265">In that case, the init function would try to call the getAllStocks function before the server connection is established.</span></span>

    <span data-ttu-id="a755c-266">서버는 주식 가격 변경 되 면 연결 된 클라이언트는 updateStockPrice 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-266">When the server changes a stock's price, it calls the updateStockPrice on connected clients.</span></span> <span data-ttu-id="a755c-267">함수는 사용할 수 있도록 호출을 서버에서 stockTicker 프록시의 클라이언트 속성에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-267">The function is added to the client property of the stockTicker proxy in order to make it available to calls from the server.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    <span data-ttu-id="a755c-268">UpdateStockPrice 함수는 init 함수와 동일 하 게 테이블 행에 서버에서 받은 주식 개체의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-268">The updateStockPrice function formats a stock object received from the server into a table row the same way as in the init function.</span></span> <span data-ttu-id="a755c-269">그러나 테이블에 행을 추가 하는 대신 주식의 현재 행에서 테이블을 찾아 새 행을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-269">However, instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

<a id="test"></a>

## <a name="test-the-application"></a><span data-ttu-id="a755c-270">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="a755c-270">Test the application</span></span>

1. <span data-ttu-id="a755c-271">F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-271">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="a755c-272">주식은 처음에 "로드 중..." 줄을 다음 초기 주식 데이터를 표시 하는 짧은 지연 후 표시 하 고 변경 하는 주가 시작 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-272">The stock table initially displays the "loading..." line, then after a short delay the initial stock data is displayed, and then the stock prices start to change.</span></span>

    ![로드](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![초기 재고 테이블](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![서버에서 변경 내용을 수신할 주식 테이블](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. <span data-ttu-id="a755c-276">브라우저 주소 표시줄에서 URL을 복사 하 고 하나 이상의 새 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-276">Copy the URL from the browser address bar and paste it into one or more new browser window(s).</span></span>

    <span data-ttu-id="a755c-277">처음 주식 표시 된 첫 번째 브라우저와 동일 하 고 변경 내용을 동시에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-277">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>
3. <span data-ttu-id="a755c-278">모든 브라우저를 닫고 새 브라우저를 열고 하 고 동일한 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-278">Close all browsers and open a new browser, then go to the same URL.</span></span>

    <span data-ttu-id="a755c-279">StockTicker singleton 개체 지속적 주식 테이블 표시를 변경 하는 주식 계속 해 서 서버에서 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-279">The StockTicker singleton object has continued to run in the server, so the stock table display shows that the stocks have continued to change.</span></span> <span data-ttu-id="a755c-280">(그림 변경 0 사용 하 여 초기 표를 참조 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="a755c-280">(You don't see the initial table with zero change figures.)</span></span>
4. <span data-ttu-id="a755c-281">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-281">Close the browser.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="a755c-282">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="a755c-282">Enable logging</span></span>

<span data-ttu-id="a755c-283">SignalR 문제 해결에 도움이 되는 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-283">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="a755c-284">이 섹션에서는 로깅을 사용 하도록 설정 하 고 어떻게 로그를 알려 주는 다음 전송 방법 중 SignalR 사용 하 여 보여 주는 예제를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a755c-284">In this section you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

- <span data-ttu-id="a755c-285">[Websocket](http://en.wikipedia.org/wiki/WebSocket), IIS 8 및 최신 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-285">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>
- <span data-ttu-id="a755c-286">[서버에서 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events), Internet Explorer 이외의 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-286">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>
- <span data-ttu-id="a755c-287">[프레임 영원히](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), Internet Explorer에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-287">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>
- <span data-ttu-id="a755c-288">[긴 폴링 Ajax](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)모든 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-288">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="a755c-289">지정된 된 연결에 대 한 SignalR 서버와 클라이언트 모두 지 원하는 최상의 전송 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-289">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="a755c-290">오픈 *StockTicker.js* 파일의 끝에 있는 연결을 초기화 하는 코드 바로 앞의 로깅을 사용 하도록 설정 하는 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-290">Open *StockTicker.js* and add a line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. <span data-ttu-id="a755c-291">F5 키를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-291">Press F5 to run the project.</span></span>
3. <span data-ttu-id="a755c-292">브라우저의 개발자 도구 창을 열고 로그를 확인 하려면 콘솔을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-292">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="a755c-293">새 연결 전송 방법을 협상 Signalr의 로그를 보려면 페이지를 새로 고침 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-293">You might have to refresh the page to see the logs of Signalr negotiating the transport method for a new connection.</span></span>

    <span data-ttu-id="a755c-294">Windows 8 (IIS 8)에서 Internet Explorer 10를 실행 하는 경우 전송 방법은 Websocket입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-294">If you are running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![IE 10 IIS 8 콘솔](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    <span data-ttu-id="a755c-296">Windows 7 (IIS 7.5)에서 Internet Explorer 10를 실행 하는 경우 전송 방법은 iframe입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-296">If you are running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is iframe.</span></span>

    ![IE 10 콘솔 IIS 7.5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    <span data-ttu-id="a755c-298">Firefox에서 Firebug 추가 기능을 콘솔 창을 얻기를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-298">In Firefox, install the Firebug add-in to get a Console window.</span></span> <span data-ttu-id="a755c-299">Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 Websocket입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-299">If you are running Firefox 19 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    <span data-ttu-id="a755c-301">Windows 7 (IIS 7.5)에서 Firefox 19를 실행 하는 경우 전송 방법은 이벤트가 서버에서 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-301">If you are running Firefox 19 on Windows 7 (IIS 7.5), the transport method is server-sent events.</span></span>

    ![Firefox 19 IIS 7.5 콘솔](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a><span data-ttu-id="a755c-303">설치 하 고 전체 StockTicker 샘플을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-303">Install and review the full StockTicker sample</span></span>

<span data-ttu-id="a755c-304">StockTicker 응용 프로그램으로 설치 되는 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 패키지를 처음부터 방금 만든 단순화 된 버전 보다 더 많은 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-304">The StockTicker application that is installed by the [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package includes more features than the simplified version that you just created from scratch.</span></span> <span data-ttu-id="a755c-305">이 자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새로운 기능 및 구현 하는 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-305">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="a755c-306">SignalR.Sample NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-306">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="a755c-307">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-307">In **Solution Explorer**, right-click the project and click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a755c-308">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **온라인**, 입력 *SignalR.Sample* 에 **온라인 검색** 상자를 선택한 다음 를클릭 **설치할** 에 **SignalR.Sample** 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-308">In the **Manage NuGet Packages** dialog box, click **Online**, enter *SignalR.Sample* in the **Search Online** box, and then click **Install** in the **SignalR.Sample** package.</span></span>

    ![SignalR.Sample 패키지 설치](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. <span data-ttu-id="a755c-310">에 *Global.asax* 파일을 주석으로 처리 된 RouteTable.Routes.MapHubs(); 응용 프로그램의 앞부분에서 추가한 줄\_메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-310">In the *Global.asax* file, comment out the RouteTable.Routes.MapHubs(); line that you added earlier in the Application\_Start method.</span></span>

    <span data-ttu-id="a755c-311">코드 *Global.asax* SignalR.Sample 패키지 등록에 SignalR 경로 때문에 더 이상 필요 합니다 *앱\_Start/RegisterHubs.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="a755c-311">The code in *Global.asax* is no longer needed because the SignalR.Sample package registers the SignalR route in the *App\_Start/RegisterHubs.cs* file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    <span data-ttu-id="a755c-312">어셈블리 특성에 의해 참조 되는 WebActivator 클래스 SignalR.Sample 패키지의 종속성으로 설치 되는 WebActivatorEx NuGet 패키지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-312">The WebActivator class that is referenced by the assembly attribute is included in the WebActivatorEx NuGet package, which is installed as a dependency of the SignalR.Sample package.</span></span>
4. <span data-ttu-id="a755c-313">**솔루션 탐색기**를 확장 합니다 *SignalR.Sample* SignalR.Sample 패키지를 설치 하 여 생성 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-313">In **Solution Explorer**, expand the *SignalR.Sample* folder which was created by installing the SignalR.Sample package.</span></span>
5. <span data-ttu-id="a755c-314">에 *SignalR.Sample* 폴더를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 클릭 하 고 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-314">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then click **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a755c-315">SignalR.Sample NuGet 설치 패키지 변경 될 수 있습니다에 있는 jQuery 버전은 프로그램 *스크립트* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-315">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="a755c-316">새 *StockTicker.html* 패키지에서 설치 하는 파일을 *SignalR.Sample* 폴더 하지만 원래 실행하려는경우패키지를설치하는jQuery버전을사용하여동기화됩니다*StockTicker.html* 다시 파일, 스크립트 태그에서 jQuery 참조를 먼저 업데이트 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-316">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="a755c-317">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="a755c-317">Run the application</span></span>

1. <span data-ttu-id="a755c-318">F5 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-318">Press F5 to run the application.</span></span>

    <span data-ttu-id="a755c-319">앞서 살펴본는 그리드 외에도 전체 주식 시세 응용 프로그램에 동일한 주식 데이터를 표시 하는 가로 스크롤 창을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-319">In addition to the grid that you saw earlier, the full stock ticker application shows a horizontally scrolling window that displays the same stock data.</span></span> <span data-ttu-id="a755c-320">처음으로 응용 프로그램을 실행 하면 "시장"는 "closed" 및 정적 표 및 되지 스크롤 하는 주식 종목 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-320">When you run the application for the first time, the "market" is "closed" and you see a static grid and a ticker window that isn't scrolling.</span></span>

    ![StockTicker 화면 시작](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    <span data-ttu-id="a755c-322">클릭 하면 **공개 시장**, **실시간 주식 시세 표시기** 가로로 스크롤할 수 상자 시작 하 고 서버 주기적으로 임의 기준 주가 변경 브로드캐스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-322">When you click **Open Market**, the **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span> <span data-ttu-id="a755c-323">주가 될 때마다 둘 다 변경 합니다 **재고 테이블 Live** 표 및 **실시간 주식 시세 표시기** 상자가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-323">Each time a stock price changes, both the **Live Stock Table** grid and the **Live Stock Ticker** box are updated.</span></span> <span data-ttu-id="a755c-324">주식의 가격 변동 양수 이면 주식 면 녹색 배경을 표시 됩니다 하 고 변경 하는 것이 음수 이면 주식 배경이 빨간색으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-324">When a stock's price change is positive, the stock is shown with a green background, and when the change is negative, the stock is shown with a red background.</span></span>

    ![StockTicker 앱 시장 열기](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    <span data-ttu-id="a755c-326">**닫기 시장** 변경을 중지 하 고 주식 종목 스크롤이 중지 하는 단추 및 **재설정** 가격 변경을 시작 하기 전에 단추를 초기 상태로 모든 주식 데이터를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-326">The **Close Market** button stops the changes and stops the ticker scrolling, and the **Reset** button resets all stock data to the initial state before price changes started.</span></span> <span data-ttu-id="a755c-327">자세한 브라우저 창을 열고 동일한 URL로 이동 하는 경우 각 브라우저에서 동시에 동적으로 업데이트 하는 같은 데이터 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-327">If you open more browser windows and go to the same URL, you see the same data dynamically updated at the same time in each browser.</span></span> <span data-ttu-id="a755c-328">단추 중 하나를 클릭 하면 모든 브라우저를 동시에 동일한 방식으로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-328">When you click one of the buttons, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="a755c-329">실시간 주식 시세 표시기 표시</span><span class="sxs-lookup"><span data-stu-id="a755c-329">Live Stock Ticker display</span></span>

<span data-ttu-id="a755c-330">합니다 **실시간 주식 시세 표시기** 표시는 CSS 스타일으로 한 줄으로 포맷 된 div 요소에는 순서가 지정 되지 않은 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-330">The **Live Stock Ticker** display is an unordered list in a div element that is formatted into a single line by CSS styles.</span></span> <span data-ttu-id="a755c-331">전광판 초기화 되 고 동일한 방식으로 테이블을 업데이트:의 자리 표시자를 대체 하 여를 &lt;li&gt; 템플릿 문자열을 동적으로 추가 합니다 &lt;li&gt; 요소를 사용 하는 &lt;ul&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-331">The ticker is initialized and updated the same way as the table: by replacing placeholders in a &lt;li&gt; template string and dynamically adding the &lt;li&gt; elements to the &lt;ul&gt; element.</span></span> <span data-ttu-id="a755c-332">div. 내에서 순서가 지정 되지 않은 목록의 왼쪽 여백 변경 하려면 jQuery 애니메이션 효과 주기 함수를 사용 하 여 수행 됩니다 스크롤</span><span class="sxs-lookup"><span data-stu-id="a755c-332">The scrolling is performed by using the jQuery animate function to vary the margin-left of the unordered list within the div.</span></span>

<span data-ttu-id="a755c-333">주식 시세 HTML:</span><span class="sxs-lookup"><span data-stu-id="a755c-333">The stock ticker HTML:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

<span data-ttu-id="a755c-334">주식 시세 CSS:</span><span class="sxs-lookup"><span data-stu-id="a755c-334">The stock ticker CSS:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

<span data-ttu-id="a755c-335">이 jQuery 코드를 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-335">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="a755c-336">클라이언트를 호출할 수 있는 서버에서 추가 메서드</span><span class="sxs-lookup"><span data-stu-id="a755c-336">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="a755c-337">StockTickerHub 클래스를 클라이언트가 호출할 수는 4 개의 추가 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-337">The StockTickerHub class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

<span data-ttu-id="a755c-338">OpenMarket, CloseMarket, 및 재설정 페이지의 맨 위에 있는 단추에 대 한 응답으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-338">OpenMarket, CloseMarket, and Reset are called in response to the buttons at the top of the page.</span></span> <span data-ttu-id="a755c-339">모든 클라이언트에 즉시 전파 되는 상태의 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-339">They demonstrate the pattern of one client triggering a change in state that is immediately propagated to all clients.</span></span> <span data-ttu-id="a755c-340">이러한 메서드의 메서드를 호출 StockTicker 클래스에 해당 효과 시장 상태 변경 및 다음 새 상태를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-340">Each of these methods calls a method in the StockTicker class that effects the market state change and then broadcasts the new state.</span></span>

<span data-ttu-id="a755c-341">StockTicker 클래스에서 시장 상태의 MarketState 열거형 값을 반환 하는 MarketState 속성으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-341">In the StockTicker class, the state of the market is maintained by a MarketState property that returns a MarketState enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

<span data-ttu-id="a755c-342">각 시장 상태를 변경 하는 방법 때문에 이와 같이 잠금 블록 안에 threadsafe 되도록 StockTicker 클래스에:</span><span class="sxs-lookup"><span data-stu-id="a755c-342">Each of the methods that change the market state do so inside a lock block because the StockTicker class has to be threadsafe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

<span data-ttu-id="a755c-343">이 코드는 threadsafe, 확인 된 \_MarketState 속성을 지 원하는 marketState 필드를 volatile로 표시 됩니다</span><span class="sxs-lookup"><span data-stu-id="a755c-343">To ensure that this code is threadsafe, the \_marketState field that backs the MarketState property is marked as volatile,</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

<span data-ttu-id="a755c-344">BroadcastMarketStateChange 및 BroadcastMarketReset 메서드를 클라이언트에서 정의 된 다른 메서드를 호출 하는 제외는 이미 살펴보았습니다 BroadcastStockPrice 메서드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-344">The BroadcastMarketStateChange and BroadcastMarketReset methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="a755c-345">서버를 호출할 수 있는 클라이언트에서 추가 기능</span><span class="sxs-lookup"><span data-stu-id="a755c-345">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="a755c-346">UpdateStockPrice 함수는 이제 표 및 주식 종목 표시를 모두 처리 하 고 jQuery.Color 빨간색 및 녹색 플래시를 사용 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-346">The updateStockPrice function now handles both the grid and the ticker display, and it uses jQuery.Color to flash red and green colors.</span></span>

<span data-ttu-id="a755c-347">새 함수 *SignalR.StockTicker.js* 설정 / 해제 단추에 따라 상태를 홍보 하는 주식 종목 창 가로 스크롤이 시작 하거나 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-347">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state, and they stop or start the ticker window horizontal scrolling.</span></span> <span data-ttu-id="a755c-348">여러 함수 ticker.client에 추가 되는 합니다 [함수를 확장 하는 jQuery](http://api.jquery.com/jQuery.extend/) 추가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-348">Since multiple functions are being added to ticker.client, the [jQuery extend function](http://api.jquery.com/jQuery.extend/) is used to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="a755c-349">연결을 설정한 후 추가 클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="a755c-349">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="a755c-350">있기 위해 몇 가지 추가 작업 후 클라이언트 연결을 설정 합니다: 시장 열림 또는 닫힘 적절 한 marketOpened 또는 marketClosed 함수를 호출 하 고 단추에 대 한 server 메서드 호출을 연결 하기 위해 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-350">After the client establishes the connection, it has some additional work to do: find out if the market is open or closed in order to call the appropriate marketOpened or marketClosed function, and attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

<span data-ttu-id="a755c-351">서버 메서드 반드시 자리까지 단추까지 연결이 설정 되 면 제공 되기 전에 서버 메서드를 호출 하려면 코드를 시도할 수 없습니다 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-351">The server methods are not wired up to the buttons until after the connection is established, so that the code can't try to call the server methods before they are available.</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="a755c-352">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a755c-352">Next steps</span></span>

<span data-ttu-id="a755c-353">이 자습서에서는 정기적으로와 모든 클라이언트에서 알림 응답에서 연결 된 모든 클라이언트에 게 서버에서 메시지를 브로드캐스트하는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-353">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients, both on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="a755c-354">다중 스레드 singleton 인스턴스를 사용 하 여 서버 상태를 유지 하는 패턴 멀티 플레이어 온라인 게임 시나리오에도 수. 있습니다</span><span class="sxs-lookup"><span data-stu-id="a755c-354">The pattern of using a multi-threaded singleton instance to maintain server state can also be also used in multi-player online game scenarios.</span></span> <span data-ttu-id="a755c-355">예를 들어 참조 [SignalR을 기반으로 하는 ShootR 게임](https://github.com/NTaylorMullen/ShootR)합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-355">For an example, see [the ShootR game that is based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="a755c-356">피어-투-피어 통신 시나리오를 보여 주는 자습서를 참조 하세요. [Getting Started with SignalR](index.md) 하 고 [SignalR을 사용 하 여 실시간 업데이트](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a755c-356">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](index.md) and [Real-Time Updating with SignalR](index.md).</span></span>

<span data-ttu-id="a755c-357">고급 SignalR 개발 개념에 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a755c-357">To learn more advanced SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="a755c-358">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="a755c-358">ASP.NET SignalR</span></span>](https://asp.net/signalr/)
- [<span data-ttu-id="a755c-359">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="a755c-359">SignalR Project</span></span>](http://signalr.net/)
- [<span data-ttu-id="a755c-360">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="a755c-360">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="a755c-361">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="a755c-361">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
