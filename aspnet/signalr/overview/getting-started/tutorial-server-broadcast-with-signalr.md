---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '자습서: SignalR 2를 사용 하 여 서버 브로드캐스트 | Microsoft Docs'
author: tdykstra
description: 이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: a243c78c7d552f1c82a88c6083871fcd16538618
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837431"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="576e6-103">자습서: SignalR 2를 사용 하 여 브로드캐스트 서버</span><span class="sxs-lookup"><span data-stu-id="576e6-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="576e6-104">이 자습서에는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="576e6-105">서버 브로드캐스트 서버가 클라이언트로 보낸 통신을 시작 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="576e6-106">이 자습서에서 만들어야 하는 응용 프로그램 주식 시세 표시기, 서버 브로드캐스트 기능에 대 한 일반적인 시나리오를 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="576e6-107">정기적으로 서버 임의로 주식 시세를 업데이트 및 모든 연결 된 클라이언트에 업데이트를 방송 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="576e6-108">브라우저, 숫자 및 기호를 **변경** 하 고 **%** 열 서버에서 알림에 대 한 응답으로 동적으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="576e6-109">경우 모두 동일한 데이터 및 표시 데이터에 동일한 변경 내용을 동시에 동일한 URL로 브라우저를 추가로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="576e6-111">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="576e6-112">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-112">Create the project</span></span>
> * <span data-ttu-id="576e6-113">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="576e6-113">Set up the server code</span></span>
> * <span data-ttu-id="576e6-114">서버 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-114">Examine the server code</span></span>
> * <span data-ttu-id="576e6-115">클라이언트 코드를 설정 하기</span><span class="sxs-lookup"><span data-stu-id="576e6-115">Set up the client code</span></span>
> * <span data-ttu-id="576e6-116">클라이언트 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-116">Examine the client code</span></span>
> * <span data-ttu-id="576e6-117">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="576e6-117">Test the application</span></span>
> * <span data-ttu-id="576e6-118">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="576e6-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="576e6-119">응용 프로그램을 구축 하는 단계를 진행 하지 않으려는 경우에 새 빈 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR.Sample 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="576e6-120">이 자습서의 단계를 수행 하지 않고 NuGet 패키지를 설치 하는 경우의 지침에 따라야 합니다 *readme.txt* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="576e6-121">OWIN 시작을 추가 해야 패키지를 실행 하려면 호출 하는 클래스는 `ConfigureSignalR` 설치 패키지에는 메서드.</span><span class="sxs-lookup"><span data-stu-id="576e6-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="576e6-122">OWIN startup 클래스를 추가 하지 않은 경우 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="576e6-123">참조 된 [StockTicker 샘플 설치](#install-the-stockticker-sample) 이 문서의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="576e6-124">전제 조건</span><span class="sxs-lookup"><span data-stu-id="576e6-124">Prerequisites</span></span>

 * <span data-ttu-id="576e6-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 사용 하 여 합니다 **ASP.NET 및 웹 개발** 워크 로드.</span><span class="sxs-lookup"><span data-stu-id="576e6-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="576e6-126">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-126">Create the project</span></span>

<span data-ttu-id="576e6-127">이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="576e6-128">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="576e6-130">에 **새 ASP.NET 웹 응용 프로그램-SignalR.StockTicker** 창에서 유지 **빈** 선택 하 고 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="576e6-131">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="576e6-131">Set up the server code</span></span>

<span data-ttu-id="576e6-132">이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="576e6-133">재고 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-133">Create the Stock class</span></span>

<span data-ttu-id="576e6-134">만들어 시작 합니다 *재고* 모델 저장 하 고 주식에 대 한 정보를 전송 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="576e6-135">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="576e6-136">클래스의 이름을 *재고* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="576e6-137">코드를 대체 합니다 *Stock.cs* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="576e6-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="576e6-138">주식을 만들 때 설정 하는 두 속성은 `Symbol` (예: microsoft MSFT) 및 `Price`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="576e6-139">다른 속성을 설정 하는 방법 및 시기에 따라 달라 집니다 `Price`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="576e6-140">처음 설정한 `Price`에 값을 가져옵니다 전파 `DayOpen`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="576e6-141">그 후 설정한 경우 `Price`, 앱을 계산 합니다 `Change` 및 `PercentChange` 속성 값의 차이에 따라 `Price` 및 `DayOpen`.</span><span class="sxs-lookup"><span data-stu-id="576e6-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="576e6-142">StockTickerHub 및 StockTicker 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="576e6-143">서버와 클라이언트 간 상호 작용을 처리 하는 SignalR 허브 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="576e6-144">`StockTickerHub` 에서 파생 된 클래스는 `SignalRHub` 클래스 처리할 클라이언트에서 연결 및 메서드 호출을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-144">A `StockTickerHub` class that derives from the `SignalRHub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="576e6-145">주식 데이터를 유지 관리를 실행 해야는 `Timer` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="576e6-146">`Timer` 개체는 주기적으로 클라이언트 연결의 독립적인 가격 업데이트를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="576e6-147">이러한 함수 넣을 수 없습니다는 `Hub` 허브는 일시적인 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="576e6-148">앱을 만듭니다는 `Hub` 허브 연결 서버에 클라이언트에서 호출 등의 각 작업에 대 한 클래스 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="576e6-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="576e6-149">따라서 주식 데이터를 유지 하 고, 가격을 업데이트, 브로드캐스트 가격 업데이트 하는 메커니즘은 별도 클래스에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="576e6-150">클래스의 이름을 지정할 수 `StockTicker`입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-150">You'll name the class `StockTicker`.</span></span>

![StockTicker에서 브로드캐스트](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="576e6-152">원하는 인스턴스를 `StockTicker` 각 참조를 설정 해야 하므로 서버에서 실행 하는 클래스 `StockTickerHub` singleton 인스턴스 `StockTicker` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="576e6-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="576e6-153">`StockTicker` 클래스는 주식 데이터 며 업데이트 트리거 하므로 클라이언트에 브로드캐스트 하지만 `StockTicker` 되지 않습니다는 `Hub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="576e6-154">`StockTicker` 클래스에는 SignalR 허브 연결 컨텍스트 개체에 대 한 참조를 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="576e6-155">SignalR 연결 컨텍스트 개체 다음 클라이언트로 브로드캐스트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="576e6-156">StockTickerHub.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="576e6-157">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="576e6-158">**새 항목 추가-SignalR.StockTicker**를 선택 **설치 됨** > **시각적 C#**   >  **Web**  >  **SignalR** 선택한 후 **SignalR 허브 클래스 (v2)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="576e6-159">클래스의 이름을 *StockTickerHub* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="576e6-160">이 단계에서는 합니다 *StockTickerHub.cs* 클래스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="576e6-161">동시에 프로젝트에 SignalR을 지 원하는 스크립트 파일 및 어셈블리 참조의 집합을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="576e6-162">코드를 대체 합니다 *StockTickerHub.cs* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="576e6-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="576e6-163">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-163">Save the file.</span></span>

<span data-ttu-id="576e6-164">앱에서는 합니다 [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클라이언트는 서버에서 호출할 수 있습니다 하는 메서드를 정의 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="576e6-165">한 가지 방법은 정의할: `GetAllStocks()`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="576e6-166">처음에 클라이언트가 서버에 연결할 때 현재 가격을 사용 하 여 주식의 모든 목록을 가져오려면이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="576e6-167">메서드를 동기적으로 실행 반환 `IEnumerable<Stock>` 메모리에서 데이터를 반환 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="576e6-168">메서드를 대기 데이터베이스 조회 또는 웹 서비스 호출 등을 포함 하는 것을 수행 하 여 데이터를 가져올 해야 하는 경우 지정 `Task<IEnumerable<Stock>>` 비동기 처리를 사용 하도록 설정 하려면 반환 값으로.</span><span class="sxs-lookup"><span data-stu-id="576e6-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="576e6-169">자세한 내용은 [ASP.NET SignalR 허브 API 가이드-서버-비동기적으로 실행 하는 경우](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="576e6-170">`HubName` 특성 앱 허브 클라이언트에서 JavaScript 코드에는 참조 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="576e6-171">기본 클라이언트에서이 특성을 사용 하지 않으면 이름은 경우 클래스 이름의 camelCase 버전 `stockTickerHub`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="576e6-172">나중에 볼 수 있듯이 만들면 합니다 `StockTicker` 클래스인 앱 해당 클래스의 singleton 인스턴스를 해당 정적에서 만듭니다 `Instance` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="576e6-173">단일 인스턴스의 `StockTicker` 얼마나 많은 클라이언트가 연결 또는 연결 끊기에 관계 없이 메모리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="576e6-174">해당 인스턴스를 `GetAllStocks()` 메서드 사용 하 여 현재 주식 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="576e6-175">StockTicker.cs 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="576e6-176">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="576e6-177">클래스의 이름을 *StockTicker* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="576e6-178">코드를 대체 합니다 *StockTicker.cs* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="576e6-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="576e6-179">모든 스레드가 동일한 인스턴스의 StockTicker 코드를 실행 하 고는, 있으므로 StockTicker 클래스는 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="576e6-180">서버 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-180">Examine the server code</span></span>

<span data-ttu-id="576e6-181">서버 코드를 검사 하 여 앱의 작동 원리를 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="576e6-182">정적 필드의 singleton 인스턴스를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="576e6-183">코드를 정적 초기화 `_instance` 지 원하는 필드를 `Instance` 클래스의 인스턴스를 사용 하 여 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="576e6-184">생성자는 private 이므로 앱을 만들 수 있는 클래스의 유일한 인스턴스인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="576e6-185">앱 사용 [초기화 지연](/dotnet/framework/performance/lazy-initialization) 에 대 한는 `_instance` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="576e6-186">성능상의 이유로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-186">It's not for performance reasons.</span></span> <span data-ttu-id="576e6-187">인스턴스 만들기는 스레드로부터 안전 해야 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="576e6-188">클라이언트가 서버에 연결 될 때마다 별도 스레드에서 실행 StockTickerHub 클래스의 새 인스턴스를 StockTicker singleton 인스턴스를 가져옵니다 합니다 `StockTicker.Instance` 정적 속성으로 앞에서 확인을 `StockTickerHub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="576e6-189">ConcurrentDictionary 주식 데이터를 저장</span><span class="sxs-lookup"><span data-stu-id="576e6-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="576e6-190">생성자가 초기화 하는 `_stocks` 일부 예제 주식 데이터 컬렉션 및 `GetAllStocks` 주식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="576e6-191">이 컬렉션의 재고 반환한 앞서 살펴본 `StockTickerHub.GetAllStocks`에 서버 메서드는는 `Hub` 클라이언트가 호출할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="576e6-192">주식 컬렉션으로 정의 되는 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 스레드로부터의 안전성에 대 한 형식.</span><span class="sxs-lookup"><span data-stu-id="576e6-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="576e6-193">사용할 수 있습니다는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 명시적으로 변경 되도록 하는 경우 사전을 잠금.</span><span class="sxs-lookup"><span data-stu-id="576e6-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="576e6-194">이 샘플 응용 프로그램에 대 한 것이 확인 응용 프로그램 데이터를 메모리에 저장 하는 데 앱을 삭제 하는 경우 데이터가 손실 된 `StockTicker` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="576e6-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="576e6-195">실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소를 사용 하 여 작업할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="576e6-196">주식 시세를 정기적으로 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="576e6-196">Periodically updating stock prices</span></span>

<span data-ttu-id="576e6-197">생성자는 시작을 `Timer` 주기적으로 임의 기준 주식 시세를 업데이트 하는 메서드를 호출 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="576e6-198">`Timer` 호출 `UpdateStockPrices`를 전달 하는 state 매개 변수에 null입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="576e6-199">앱에서 잠금을 사용 가격을 업데이트 하기 전에 `_updateStockPricesLock` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="576e6-200">코드에서는 다른 스레드를 가격을 업데이트 하 고 호출한 다음 `TryUpdateStockPrice` 목록의 각 주식에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="576e6-201">`TryUpdateStockPrice` 주가 변경할지 여부를 결정 하는 메서드 및 변경 하려면 얼마나 많은 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="576e6-202">앱을 호출 하는 주가 변경 되 면 `BroadcastStockPrice` 브로드캐스트 모든 주가 변경 하려면 클라이언트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="576e6-203">`_updatingStockPrices` 지정 된 플래그 [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) 는 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="576e6-204">실제 응용 프로그램에서는 `TryUpdateStockPrice` 메서드는 가격을 조회 하는 웹 서비스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="576e6-205">이 코드에서는 앱 난수 생성기를 사용 하 여 임의로 변경.</span><span class="sxs-lookup"><span data-stu-id="576e6-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="576e6-206">클라이언트에 StockTicker 클래스 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기</span><span class="sxs-lookup"><span data-stu-id="576e6-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="576e6-207">가격 변경 내용을 여기 발생 하기 때문에 합니다 `StockTicker` 개체를 호출 해야 하는 개체는 `updateStockPrice` 메서드 연결 된 모든 클라이언트를 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="576e6-208">에 `Hub` 클래스는 API가 있다고 클라이언트 메서드를 호출 하지만 `StockTicker` 에서 파생 되지 합니다 `Hub` 클래스 고 대 한 참조를 `Hub` 개체.</span><span class="sxs-lookup"><span data-stu-id="576e6-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="576e6-209">연결 된 클라이언트에 브로드캐스트하는 `StockTicker` 클래스에는 SignalR 컨텍스트 인스턴스를 가져오려고는 `StockTickerHub` 클래스를 사용 하는 클라이언트에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="576e6-210">생성자에 전달 참조 하는 단일 클래스 인스턴스를 만들 때 코드는 SignalR 컨텍스트에 대 한 참조를 가져옵니다 하 고 생성자에 배치 된 `Clients` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="576e6-211">두 가지 컨텍스트를 한 번만 가져올 하려는 이유: 컨텍스트 가져오기 이며 비용이 많이 드는 작업을 앱 설정 클라이언트에 전송 된 메시지의 의도 한 순서를 유지 한 후 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="576e6-212">가져오기는 `Clients` 컨텍스트와 배치 속성을 `StockTickerClient` 속성이 있는 것 처럼 동일 하 게 표시 하는 메서드를 호출할 클라이언트 코드를 작성할 수 있습니다는 `Hub` 클래스.</span><span class="sxs-lookup"><span data-stu-id="576e6-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="576e6-213">예를 들어 모든 클라이언트에 브로드캐스트를 작성할 수 `Clients.All.updateStockPrice(stock)`입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="576e6-214">합니다 `updateStockPrice` 메서드를 호출 하는 `BroadcastStockPrice` 아직 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="576e6-215">클라이언트에서 실행 되는 코드를 작성 하는 경우 나중에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="576e6-216">참조할 수 있습니다 `updateStockPrice` 여기 하므로 `Clients.All` 가 동적 이므로 앱 런타임에 식을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="576e6-217">이 메서드 호출은 실행 되 면 SignalR 전송할 메서드 이름과 매개 변수 값을 클라이언트에 클라이언트 라는 메서드를 포함 하는 경우 `updateStockPrice`, 앱 메서드를 호출 하 고 매개 변수 값을 전달할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="576e6-218">`Clients.All` 이면 모든 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="576e6-219">SignalR은 클라이언트 또는 클라이언트에 보낼 그룹 지정을 다른 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="576e6-220">자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="576e6-221">SignalR 경로 등록</span><span class="sxs-lookup"><span data-stu-id="576e6-221">Register the SignalR route</span></span>

<span data-ttu-id="576e6-222">서버를 가로채 고 signalr 직접 URL을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="576e6-223">이렇게 하려면 OWIN 시작 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="576e6-224">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="576e6-225">**새 항목 추가-SignalR.StockTicker** 선택 **설치 됨** > **시각적 C#**   >  **Web** 및 선택한 **OWIN Startup 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="576e6-226">클래스의 이름을 *시동* 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="576e6-227">기본 코드를 대체 합니다 *Startup.cs* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="576e6-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="576e6-228">이제 서버 코드가 설정 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="576e6-229">다음 섹션에서는 클라이언트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="576e6-230">클라이언트 코드를 설정 하기</span><span class="sxs-lookup"><span data-stu-id="576e6-230">Set up the client code</span></span>

<span data-ttu-id="576e6-231">이 섹션에서는 클라이언트에서 실행 되는 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="576e6-232">HTML 페이지 및 JavaScript 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="576e6-233">HTML 페이지에 데이터가 표시 됩니다 및 JavaScript 파일에서 데이터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="576e6-234">StockTicker.html 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-234">Create StockTicker.html</span></span>

<span data-ttu-id="576e6-235">먼저 HTML 클라이언트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="576e6-236">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **HTML 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="576e6-237">파일 이름을 *StockTicker* 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="576e6-238">기본 코드를 대체 합니다 *StockTicker.html* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="576e6-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="576e6-239">HTML 5 개의 열, 하나의 머리글 행 및 5 개 열에 모두 걸친 단일 셀을 사용 하 여 데이터 행을 사용 하 여 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="576e6-240">데이터 행 "로드 중..." 앱을 시작 하는 경우에 일시적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="576e6-241">JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 하는 주식 데이터를 사용 하 여 해당 내부 행에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="576e6-242">스크립트 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-242">The script tags specify:</span></span>

    * <span data-ttu-id="576e6-243">JQuery 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-243">The jQuery script file.</span></span>

    * <span data-ttu-id="576e6-244">SignalR core 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="576e6-245">SignalR 프록시 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="576e6-246">나중에 만드는 StockTicker 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="576e6-247">앱은 SignalR 프록시 스크립트 파일을 동적으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="576e6-248">"/ Signalr 허브" URL을 지정 하 고에 대 한이 경우 허브 클래스에서 메서드에 대 한 프록시 메서드를 정의 `StockTickerHub.GetAllStocks`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="576e6-249">원하는 경우 수동으로 생성할 수 있습니다이 JavaScript 파일을 사용 하 여 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="576e6-250">동적 파일 생성을 사용 하지 않도록 설정 해야 합니다 `MapHubs` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="576e6-251">**솔루션 탐색기**를 확장 하 고 **스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="576e6-252">JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="576e6-253">패키지 관리자 SignalR 스크립트의 이후 버전이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="576e6-254">프로젝트에서 스크립트 파일의 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="576e6-255">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 선택한 후 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="576e6-256">StockTicker.js 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-256">Create StockTicker.js</span></span>

<span data-ttu-id="576e6-257">이제 JavaScript 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="576e6-258">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **JavaScript 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="576e6-259">파일 이름을 *StockTicker* 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="576e6-260">이 코드를 추가 합니다 *StockTicker.js* 파일:</span><span class="sxs-lookup"><span data-stu-id="576e6-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="576e6-261">클라이언트 코드를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-261">Examine the client code</span></span>

<span data-ttu-id="576e6-262">클라이언트 코드를 검사 하 여 클라이언트 코드는 앱이 작동 하려면 서버 코드를 상호 작용 하는 방법을 배우는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="576e6-263">연결을 시작</span><span class="sxs-lookup"><span data-stu-id="576e6-263">Starting the connection</span></span>

<span data-ttu-id="576e6-264">`$.connection` SignalR 프록시를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="576e6-265">코드에 대 한 프록시에 대 한 참조를 가져옵니다 합니다 `StockTickerHub` 클래스 넣습니다는 `ticker` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="576e6-266">설정 된 이름인 프록시 이름을 `HubName` 특성:</span><span class="sxs-lookup"><span data-stu-id="576e6-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="576e6-267">파일의 코드의 마지막 줄을 SignalR을 호출 하 여 SignalR 연결을 초기화 하는 모든 변수 및 함수를 정의한 후 `start` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="576e6-268">합니다 `start` 비동기적으로 실행 하 고 반환 하는 함수를 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/)합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="576e6-269">앱에는 비동기 작업을 완료 될 때 호출할 함수를 지정 하는 완료 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="576e6-270">모든 스톡 가져오기</span><span class="sxs-lookup"><span data-stu-id="576e6-270">Getting all the stocks</span></span>

<span data-ttu-id="576e6-271">합니다 `init` 함수 호출을 `getAllStocks` 서버 기능에 재고 테이블을 업데이트 하려면 서버를 반환 하는 정보를 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="576e6-272">기본적으로 사용 해야 camelCasing 클라이언트에서 메서드 이름은 서버의 파스칼식도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="576e6-273">CamelCasing 규칙 메서드를 개체가 아닌에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="576e6-274">참조 하는 예를 들어 `stock.Symbol` 하 고 `stock.Price`가 아닌 `stock.symbol` 또는 `stock.price`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="576e6-275">에 `init` 메서드 앱은 호출 하 여 서버에서 받은 각 주식 개체에 대 한 테이블 행에 대 한 HTML을 생성 `formatStock` 의 형식 속성에는 `stock` 개체를 호출 하 여 다음 `supplant` 합니다 의자리표시자를바꾸려면`rowTemplate` 변수는 `stock` 개체 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="576e6-276">그런 다음 결과 HTML은 주식 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="576e6-277">문의할 `init` 에 전달 하 여는 `callback` 비동기 이후에 실행 하는 함수 `start` 함수 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="576e6-278">호출 하면 `init` 호출한 후는 별도 JavaScript 문으로 `start`를 설정 하 고 연결을 완료 하는 시작 함수를 기다리지 않고 즉시 실행 함수를 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="576e6-279">이런 경우는 `init` 함수를 호출 하려고 합니다.는 `getAllStocks` 함수 앱 서버 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="576e6-280">업데이트 된 주식 시세 가져오기</span><span class="sxs-lookup"><span data-stu-id="576e6-280">Getting updated stock prices</span></span>

<span data-ttu-id="576e6-281">서버는 주식 가격을 변경 하는 경우 호출 하는 `updateStockPrice` 연결 된 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="576e6-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="576e6-282">앱의 클라이언트 속성에 함수를 추가 합니다 `stockTicker` 사용할 수 있도록 호출을 서버에서 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="576e6-283">합니다 `updateStockPrice` 함수 형식 테이블로 서버에서 받은 스톡 개체 행에서 동일한 방법으로 `init` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="576e6-284">테이블에 행을 추가 하는 대신이 클래스는 테이블에서 주식의 현재 행을 찾습니다을 새 행을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="576e6-285">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="576e6-285">Test the application</span></span>

<span data-ttu-id="576e6-286">확인 하기 위해 앱을 테스트할 수 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="576e6-287">주가 변동를 사용 하 여 라이브 재고 테이블을 표시 하는 모든 브라우저 창을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="576e6-288">도구 모음에서 설정 **스크립트 디버깅** 다음 디버그 모드에서 앱을 실행 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![디버깅 모드 켜기 재생을 선택 하는 사용자의 스크린샷.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="576e6-290">표시 하는 브라우저 창이 열립니다는 **재고 테이블 Live**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="576e6-291">주식은 처음에 줄을 표시 "로드 중...", 그런 다음 잠시 후 앱은 초기 주식 데이터 표시 및 변경 하는 주가 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="576e6-292">브라우저에서 URL을 복사 하 고 다른 두 브라우저를 열고 주소 표시줄에 Url을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="576e6-293">처음 주식 표시 된 첫 번째 브라우저와 동일 하 고 변경 내용을 동시에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="576e6-294">모든 브라우저를 닫고 새 브라우저를 열고 동일한 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="576e6-295">StockTicker singleton 개체 서버에서 실행을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="576e6-296">합니다 **재고 테이블 Live** 주식 계속 해 서 변경에 함을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="576e6-297">그림 변경 0 사용 하 여 초기 표를 참조 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="576e6-298">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="576e6-299">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="576e6-299">Enable logging</span></span>

<span data-ttu-id="576e6-300">SignalR 문제 해결에 도움이 되는 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="576e6-301">이 섹션에서는 로깅을 사용 하도록 설정 하 고 어떻게 로그를 알려 주는 다음 전송 방법 중 SignalR 사용 하 여 보여 주는 예제를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="576e6-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="576e6-302">[Websocket](http://en.wikipedia.org/wiki/WebSocket), IIS 8 및 최신 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="576e6-303">[서버에서 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events), Internet Explorer 이외의 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="576e6-304">[프레임 영원히](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), Internet Explorer에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="576e6-305">[긴 폴링 Ajax](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)모든 브라우저에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="576e6-306">지정된 된 연결에 대 한 SignalR 서버와 클라이언트 모두 지 원하는 최상의 전송 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="576e6-307">오픈 *StockTicker.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="576e6-308">이 강조 표시 된 파일의 끝에 있는 연결을 초기화 하는 코드 바로 앞의 로깅을 사용 하도록 설정 하는 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="576e6-309">**F5** 키를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="576e6-310">브라우저의 개발자 도구 창을 열고 로그를 확인 하려면 콘솔을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="576e6-311">새 연결 전송 방법을 협상 SignalR의 로그를 보려면 페이지를 새로 고침 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="576e6-312">Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 중인 경우 전송 메서드는 **Websocket**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="576e6-313">Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 중인 경우 전송 메서드는 **iframe**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="576e6-314">전송 메서드는 Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 **Websocket**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="576e6-315">Firefox에서 Firebug 추가 기능을 콘솔 창을 얻기를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="576e6-316">Firefox 19 (IIS 7.5) Windows 7을 실행 중인 경우 전송 메서드는 **서버에서 전송** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="576e6-317">StockTicker 샘플 설치</span><span class="sxs-lookup"><span data-stu-id="576e6-317">Install the StockTicker sample</span></span>

<span data-ttu-id="576e6-318">합니다 [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) StockTicker 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="576e6-319">NuGet 패키지를 처음부터 만든 단순화 된 버전 보다 더 많은 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="576e6-320">이 자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새로운 기능 및 구현 하는 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="576e6-321">이 자습서의 이전 단계를 수행 하지 않고 패키지를 설치 하는 경우에 프로젝트에 OWIN 시작 클래스를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="576e6-322">NuGet 패키지의 readme.txt 파일에서는이 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="576e6-323">SignalR.Sample NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="576e6-324">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="576e6-325">**NuGet 패키지 관리자: SignalR.StockTicker**을 선택 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="576e6-326">**패키지 소스**를 선택 **nuget.org**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="576e6-327">입력 *SignalR.Sample* 검색 상자에 선택 **Microsoft.AspNet.SignalR.Sample** > **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="576e6-328">**솔루션 탐색기**를 확장 합니다 *SignalR.Sample* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="576e6-329">폴더 및 해당 콘텐츠를 만든 SignalR.Sample 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="576e6-330">에 *SignalR.Sample* 폴더를 마우스 오른쪽 단추로 클릭 *StockTicker.html*를 선택한 후 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="576e6-331">SignalR.Sample NuGet 설치 패키지 변경 될 수 있습니다에 있는 jQuery 버전은 프로그램 *스크립트* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="576e6-332">새 *StockTicker.html* 패키지에서 설치 하는 파일을 *SignalR.Sample* 폴더 하지만 원래 실행하려는경우패키지를설치하는jQuery버전을사용하여동기화됩니다*StockTicker.html* 다시 파일, 스크립트 태그에서 jQuery 참조를 먼저 업데이트 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="576e6-333">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="576e6-333">Run the application</span></span>

 <span data-ttu-id="576e6-334">첫 번째 앱에서 볼 수 있는 테이블에는 유용한 기능이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="576e6-335">전체 주식 시세 응용 프로그램이 새 기능을 보여 줍니다: 주식 증가 하 고 해당 색을 변경 하 고 주식 데이터를 표시 하는 가로 스크롤 창을 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="576e6-336">**F5** 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="576e6-337">처음으로 앱을 실행 하는 경우 "시장"는 "closed" 및 정적 테이블 및 되지 스크롤 하는 주식 종목 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="576e6-338">선택 **Open Market**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-338">Select **Open Market**.</span></span>

    ![실시간 주식 종목 스크린샷입니다.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="576e6-340">**실시간 주식 시세 표시기** 가로로 스크롤할 수 상자 시작 하 고 서버 주기적으로 임의 기준 주가 변경 브로드캐스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="576e6-341">때마다 주가 변경, 앱 모두를 업데이트 합니다 **재고 테이블 Live** 및 **실시간 주식 시세 표시기**.</span><span class="sxs-lookup"><span data-stu-id="576e6-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="576e6-342">주식의 가격 변동 양수 이면 앱 주식 면 녹색 배경을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="576e6-343">변경이 음수 이면 앱에는 빨간색 배경의 주식 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="576e6-344">선택 **시장 닫습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="576e6-345">테이블 업데이트 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-345">The table updates stop.</span></span>

    * <span data-ttu-id="576e6-346">전광판 스크롤이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="576e6-347">선택 **재설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-347">Select **Reset**.</span></span>

    * <span data-ttu-id="576e6-348">모든 주식 데이터 다시 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-348">All stock data is reset.</span></span>

    * <span data-ttu-id="576e6-349">앱 가격 변경 내용 시작 하기 전에 초기 상태를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="576e6-350">브라우저에서 URL을 복사 하 고 다른 두 브라우저를 열고 주소 표시줄에 Url을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="576e6-351">각 브라우저에서 동시에 동적으로 업데이트 하는 동일한 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="576e6-352">컨트롤 중 하나를 선택 하면 모든 브라우저를 동시에 동일한 방식으로 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="576e6-353">실시간 주식 시세 표시기 표시</span><span class="sxs-lookup"><span data-stu-id="576e6-353">Live Stock Ticker display</span></span>

<span data-ttu-id="576e6-354">합니다 **실시간 주식 시세 표시기** 표시 되는 순서가 지정 되지 않은 목록의 `<div>` CSS 스타일에서 요소를 단일 줄으로 형식이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="576e6-355">앱 초기화 하 고 전광판 테이블과 동일한 방식으로 업데이트:의 자리 표시자를 대체 하 여는 `<li>` 템플릿 문자열을 동적으로 추가 합니다 `<li>` 요소를 사용 하는 `<ul>` 요소.</span><span class="sxs-lookup"><span data-stu-id="576e6-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="576e6-356">JQuery를 사용 하 여 스크롤 포함 `animate` 내에서 순서가 지정 되지 않은 목록의 왼쪽 여백 변경 하는 함수는 `<div>`합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="576e6-357">SignalR.Sample StockTicker.html</span><span class="sxs-lookup"><span data-stu-id="576e6-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="576e6-358">주식 시세 HTML 코드:</span><span class="sxs-lookup"><span data-stu-id="576e6-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="576e6-359">SignalR.Sample StockTicker.css</span><span class="sxs-lookup"><span data-stu-id="576e6-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="576e6-360">주식 시세 CSS 코드:</span><span class="sxs-lookup"><span data-stu-id="576e6-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="576e6-361">SignalR.Sample SignalR.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="576e6-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="576e6-362">이 jQuery 코드를 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="576e6-363">클라이언트를 호출할 수 있는 서버에서 추가 메서드</span><span class="sxs-lookup"><span data-stu-id="576e6-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="576e6-364">앱에 유연성을 추가할 추가 메서드는 앱에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="576e6-365">SignalR.Sample StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="576e6-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="576e6-366">`StockTickerHub` 클래스는 클라이언트를 호출할 수 있는 네 가지 추가 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="576e6-367">앱 호출 `OpenMarket`, `CloseMarket`, 및 `Reset` 페이지의 맨 위에 있는 단추에 대 한 응답에서입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="576e6-368">모든 클라이언트에 즉시 전파 상태 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="576e6-369">이러한 각 방법에서 메서드를 호출 합니다 `StockTicker` 클래스는 시장 상태 변경이 발생 한 다음 새 상태를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="576e6-370">SignalR.Sample StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="576e6-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="576e6-371">에 `StockTicker` 클래스를 앱으로 시장의 상태를 유지 관리를 `MarketState` 반환 하는 속성을 `MarketState` 열거형 값:</span><span class="sxs-lookup"><span data-stu-id="576e6-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="576e6-372">각 시장 상태를 변경 하는 방법 때문에 이와 같이 잠금 블록 안에 `StockTicker` 클래스를 스레드로부터 안전 해야 합니다.:</span><span class="sxs-lookup"><span data-stu-id="576e6-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="576e6-373">이 코드는 스레드로부터 안전 해야 합니다 `_marketState` 지 원하는 필드를 `MarketState` 지정 된 속성 `volatile`:</span><span class="sxs-lookup"><span data-stu-id="576e6-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="576e6-374">합니다 `BroadcastMarketStateChange` 및 `BroadcastMarketReset` 메서드는 클라이언트에서 정의 된 다른 메서드를 호출 하는 제외에 이미 살펴보았습니다 BroadcastStockPrice 메서드 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="576e6-375">서버를 호출할 수 있는 클라이언트에서 추가 기능</span><span class="sxs-lookup"><span data-stu-id="576e6-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="576e6-376">합니다 `updateStockPrice` 함수는 이제 주식 종목 표시와 테이블을 모두 처리 하 고 사용 하 여 `jQuery.Color` 빨간색 및 녹색 깜빡입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="576e6-377">새 함수 *SignalR.StockTicker.js* 사용 하도록 설정 하 고 시장 상태에 따라 단추를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="576e6-378">이러한도 중지 하거나 시작 합니다 **실시간 주식 시세 표시기** 가로 스크롤.</span><span class="sxs-lookup"><span data-stu-id="576e6-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="576e6-379">다양 한 함수에 추가 되는 때문 `ticker.client`, 앱에서는 합니다 [함수를 확장 하는 jQuery](http://api.jquery.com/jQuery.extend/) 추가할.</span><span class="sxs-lookup"><span data-stu-id="576e6-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="576e6-380">연결을 설정한 후 추가 클라이언트 설정</span><span class="sxs-lookup"><span data-stu-id="576e6-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="576e6-381">클라이언트 연결을 설정, 후 일부 추가 작업을 수행에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="576e6-382">시장 열림 또는 닫힘 적절 한 호출 하는 경우 찾기 `marketOpened` 또는 `marketClosed` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="576e6-383">단추에 대 한 server 메서드 호출을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="576e6-384">서버 메서드 앱 연결을 설정 후까지 단추 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="576e6-385">이므로 제공 되기 전에 코드는 서버 메서드를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="576e6-386">추가 자료</span><span class="sxs-lookup"><span data-stu-id="576e6-386">Additional resources</span></span>

<span data-ttu-id="576e6-387">이 자습서에서는 연결 된 모든 클라이언트에 게 서버에서 메시지를 브로드캐스트하는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="576e6-388">이제 모든 클라이언트에서 알림 응답에서 메시지를 정기적으로 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="576e6-389">다중 스레드 singleton 인스턴스 개념이 멀티 플레이어 온라인 게임 시나리오에서 서버 상태를 유지 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="576e6-390">예를 들어 참조 [SignalR을 기반으로 ShootR 게임](https://github.com/NTaylorMullen/ShootR)합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="576e6-391">피어-투-피어 통신 시나리오를 보여 주는 자습서를 참조 하세요. [Getting Started with SignalR](introduction-to-signalr.md) 하 고 [SignalR을 사용 하 여 실시간 업데이트](tutorial-high-frequency-realtime-with-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="576e6-392">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="576e6-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="576e6-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="576e6-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="576e6-394">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="576e6-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="576e6-395">SignalR GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="576e6-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="576e6-396">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="576e6-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="576e6-397">다음 단계</span><span class="sxs-lookup"><span data-stu-id="576e6-397">Next steps</span></span>

<span data-ttu-id="576e6-398">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="576e6-399">프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-399">Created the project</span></span>
> * <span data-ttu-id="576e6-400">서버 코드 설정</span><span class="sxs-lookup"><span data-stu-id="576e6-400">Set up the server code</span></span>
> * <span data-ttu-id="576e6-401">서버 코드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-401">Examined the server code</span></span>
> * <span data-ttu-id="576e6-402">클라이언트 코드를 설정 하기</span><span class="sxs-lookup"><span data-stu-id="576e6-402">Set up the client code</span></span>
> * <span data-ttu-id="576e6-403">클라이언트 코드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="576e6-403">Examined the client code</span></span>
> * <span data-ttu-id="576e6-404">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="576e6-404">Tested the application</span></span>
> * <span data-ttu-id="576e6-405">활성화 된 로깅</span><span class="sxs-lookup"><span data-stu-id="576e6-405">Enabled logging</span></span>

<span data-ttu-id="576e6-406">ASP.NET SignalR 2를 사용 하 여 실시간 웹 응용 프로그램을 만드는 방법에 알아보려면 다음 문서로 계속 진행 하세요.</span><span class="sxs-lookup"><span data-stu-id="576e6-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="576e6-407">SignalR을 사용 하 여 실시간 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="576e6-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)