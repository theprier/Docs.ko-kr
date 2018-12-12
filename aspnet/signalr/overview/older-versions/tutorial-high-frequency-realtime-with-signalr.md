---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: SignalR 사용 하 여 고주파수 1.x | Microsoft Docs
author: pfletcher
description: 이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR을 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 빈도가 높은 메시징에 중...
ms.author: riande
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: a679a7c66a94fa440a1ead64225eb86f7de90c9e
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287964"
---
<a name="high-frequency-realtime-with-signalr-1x"></a><span data-ttu-id="13f3c-104">SignalR 사용 하 여 고주파수 1.x</span><span class="sxs-lookup"><span data-stu-id="13f3c-104">High-Frequency Realtime with SignalR 1.x</span></span>
====================
<span data-ttu-id="13f3c-105">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="13f3c-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="13f3c-106">이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR을 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="13f3c-107">이 경우 고정 된 요금이; 전송 되는 업데이트를 의미 빈도가 높은 메시징 이 응용 프로그램의 경우 최대 10 개까지 두 번째를 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-107">High-frequency messaging in this case means updates that are sent at a fixed rate; in the case of this application, up to 10 messages a second.</span></span>
> 
> <span data-ttu-id="13f3c-108">이 자습서에서 만드는 응용 프로그램 사용자 끌 수 있는 셰이프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-108">The application you'll create in this tutorial displays a shape that users can drag.</span></span> <span data-ttu-id="13f3c-109">연결 된 다른 모든 브라우저에서 모양의 위치 다음의 업데이트를 사용 하 여 끌어 온 모양의 위치와 일치 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-109">The position of the shape in all other connected browsers will then be updated to match the position of the dragged shape using timed updates.</span></span>
> 
> <span data-ttu-id="13f3c-110">이 자습서에 도입 된 개념 실시간 게임에서 응용 프로그램 및 다른 시뮬레이션 응용 프로그램을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-110">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>
> 
> <span data-ttu-id="13f3c-111">이 자습서에 대 한 의견을 기다리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-111">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="13f3c-112">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>


## <a name="overview"></a><span data-ttu-id="13f3c-113">개요</span><span class="sxs-lookup"><span data-stu-id="13f3c-113">Overview</span></span>

<span data-ttu-id="13f3c-114">이 자습서에는 실시간으로 다른 브라우저를 사용 하 여 개체의 상태를 공유 하는 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-114">This tutorial demonstrates how to create an application that shares the state of an object with other browsers in real time.</span></span> <span data-ttu-id="13f3c-115">응용 프로그램 만들겠습니다 MoveShape 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-115">The application we'll create is called MoveShape.</span></span> <span data-ttu-id="13f3c-116">MoveShape 페이지는 다음을 끌 수 있습니다; HTML Div 요소가 표시 됩니다. Div를 끌 때 새 위치로 연결 된 다른 모든 클라이언트에 맞게 도형의 위치를 업데이트 하려면 다음 알려 서버로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-116">The MoveShape page will display an HTML Div element that the user can drag; when the user drags the Div, its new position will be sent to the server, which will then tell all other connected clients to update the shape's position to match.</span></span>

![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

<span data-ttu-id="13f3c-118">이 자습서에서 만든 응용 프로그램은 Damian edwards의 데모를 기반으로 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-118">The application created in this tutorial is based on a demo by Damian Edwards.</span></span> <span data-ttu-id="13f3c-119">이 데모를 포함 하는 비디오를 볼 수 있습니다 [여기](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-119">A video containing this demo can be seen [here](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR).</span></span>

<span data-ttu-id="13f3c-120">이 자습서는 셰이프를 끌 때 발생 하는 각 이벤트에서 SignalR 메시지를 보내는 방법을 보여 줍니다 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-120">The tutorial will start by demonstrating how to send SignalR messages from each event that fires as the shape is dragged.</span></span> <span data-ttu-id="13f3c-121">연결 된 각 클라이언트가 모양의 로컬 버전의 위치는 메시지가 수신 될 때마다 업데이트 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-121">Each connected client will then update the position of the local version of the shape each time a message is received.</span></span>

<span data-ttu-id="13f3c-122">이 메서드를 사용 하 여 응용 프로그램 작동을 하는 동안 이것이 권장 되는 프로그래밍 모델을 클라이언트와 서버가 메시지를 사용 하 여 과부하가 가져올 수 없습니다 하 고 성능 저하는 보낸 시작 메시지의 수에 제한이 없어집니다 것 이므로 .</span><span class="sxs-lookup"><span data-stu-id="13f3c-122">While the application will function using this method, this is not a recommended programming model, since there would be no upper limit to the number of messages getting sent, so the clients and server could get overwhelmed with messages and performance would degrade.</span></span> <span data-ttu-id="13f3c-123">각 새 위치에 원활 하 게 이동 하는 대신 각 메서드에서 셰이프를 즉시 이동은 연결이 끊긴 클라이언트에 표시 된 애니메이션도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-123">The displayed animation on the client would also be disjointed, as the shape would be moved instantly by each method, rather than moving smoothly to each new location.</span></span> <span data-ttu-id="13f3c-124">자습서의 뒷부분에 나오는 섹션에서는 클라이언트 또는 서버에서 메시지가 전송 되는 최대 속도 제한 하는 타이머 함수를 만드는 방법 및 셰이프를 위치 간에 원활 하 게 이동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-124">Later sections of the tutorial will demonstrate how to create a timer function that restricts the maximum rate at which messages are sent by either the client or server, and how to move the shape smoothly between locations.</span></span> <span data-ttu-id="13f3c-125">이 자습서에서 만든 응용 프로그램의 최종 버전에서 다운로드할 수 있습니다 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-125">The final version of the application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="13f3c-126">이 자습서는 다음 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-126">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="13f3c-127">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="13f3c-127">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="13f3c-128">프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="13f3c-128">Create the project</span></span>](#createtheproject)
- [<span data-ttu-id="13f3c-129">ASP.NET SignalR 및 JQuery.UI NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="13f3c-129">Add the ASP.NET SignalR and JQuery.UI NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="13f3c-130">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="13f3c-130">Create the base application</span></span>](#baseapp)
- [<span data-ttu-id="13f3c-131">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="13f3c-131">Add the client loop</span></span>](#clientloop)
- [<span data-ttu-id="13f3c-132">서버 루프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-132">Add the server loop</span></span>](#serverloop)
- [<span data-ttu-id="13f3c-133">클라이언트에서 부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="13f3c-133">Add smooth animation on the client</span></span>](#animation)
- [<span data-ttu-id="13f3c-134">추가 단계</span><span class="sxs-lookup"><span data-stu-id="13f3c-134">Further Steps</span></span>](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="13f3c-135">전제 조건</span><span class="sxs-lookup"><span data-stu-id="13f3c-135">Prerequisites</span></span>

<span data-ttu-id="13f3c-136">이 자습서는 Visual Studio 2012 또는 Visual Studio 2010에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-136">This tutorial requires Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="13f3c-137">Visual Studio 2010을 사용 하는 경우 프로젝트가.NET Framework 4.5를 사용 하지 않고.NET Framework 4를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-137">If Visual Studio 2010 is used, the project will use .NET Framework 4 rather than .NET Framework 4.5.</span></span>

<span data-ttu-id="13f3c-138">Visual Studio 2012를 사용 하는 것이 좋습니다 설치 하는 [ASP.NET 및 웹 도구 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-138">If you are using Visual Studio 2012, it's recommended that you install the [ASP.NET and Web Tools 2012.2 update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="13f3c-139">이 업데이트에는 게시의 경우 새 기능에 고급 기능과 같은 새 기능이 포함 되어 있습니다. 및 새 템플릿.</span><span class="sxs-lookup"><span data-stu-id="13f3c-139">This update contains new features such as enhancements to publishing, new functionality, and new templates.</span></span>

<span data-ttu-id="13f3c-140">Visual Studio 2010 경우 했는지 [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-140">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createtheproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="13f3c-141">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-141">Create the project</span></span>

<span data-ttu-id="13f3c-142">이 섹션에서는 Visual Studio에서 프로젝트를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-142">In this section, we'll create the project in Visual Studio.</span></span>

1. <span data-ttu-id="13f3c-143">**파일** 메뉴 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-143">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="13f3c-144">에 **새 프로젝트** 대화 상자에서 **C#** 아래에 있는 **템플릿** 선택한 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-144">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="13f3c-145">선택 된 **ASP.NET 빈 웹 응용 프로그램** 서식 파일을 프로젝트의 이름 *MoveShapeDemo*, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-145">Select the **ASP.NET Empty Web Application** template, name the project *MoveShapeDemo*, and click **OK**.</span></span>

    ![새 프로젝트 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a><span data-ttu-id="13f3c-147">SignalR 및 JQuery.UI NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="13f3c-147">Add the SignalR and JQuery.UI NuGet Packages</span></span>

<span data-ttu-id="13f3c-148">프로젝트에 NuGet 패키지를 설치 하 여 SignalR 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-148">You can add SignalR functionality to a project by installing a NuGet package.</span></span> <span data-ttu-id="13f3c-149">이 자습서 도형에 애니메이션을 끌어서 놓을 수 있도록 하는 것에 대 한 JQuery.UI 패키지도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-149">This tutorial will also use the JQuery.UI package for allowing the shape to be dragged and animated.</span></span>

1. <span data-ttu-id="13f3c-150">클릭 **도구 | NuGet 패키지 관리자 | 패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-150">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="13f3c-151">패키지 관리자에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-151">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    <span data-ttu-id="13f3c-152">SignalR 패키지 종속성으로 다양 한 다른 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-152">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="13f3c-153">설치가 완료 되는 경우 모든 ASP.NET 응용 프로그램에서 SignalR을 사용 하는 데 필요한 서버 및 클라이언트 구성 요소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-153">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>
3. <span data-ttu-id="13f3c-154">JQuery 및 JQuery.UI 패키지를 설치 하려면 패키지 관리자 콘솔에 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-154">Enter the following command into the package manager console to install the JQuery and JQuery.UI packages.</span></span>

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a><span data-ttu-id="13f3c-155">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="13f3c-155">Create the base application</span></span>

<span data-ttu-id="13f3c-156">이 섹션에서는 각 마우스 이동 이벤트 동안 모양의 위치 서버로 전송 하는 브라우저 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-156">In this section, we'll create a browser application that sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="13f3c-157">그런 다음 서버를 수신할 때 연결 된 다른 모든 클라이언트에이 정보를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-157">The server then broadcasts this information to all other connected clients as it is received.</span></span> <span data-ttu-id="13f3c-158">이후 섹션에서이 응용 프로그램에서 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-158">We'll expand on this application in later sections.</span></span>

1. <span data-ttu-id="13f3c-159">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**, **클래스...** . 클래스의 이름을 **MoveShapeHub** 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-159">In **Solution Explorer**, right-click on the project and select **Add**, **Class...**. Name the class **MoveShapeHub** and click **Add**.</span></span>
2. <span data-ttu-id="13f3c-160">새 코드를 바꿉니다 **MoveShapeHub** 다음 코드를 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-160">Replace the code in the new **MoveShapeHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="13f3c-161">`MoveShapeHub` 위의 클래스는 SignalR 허브의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-161">The `MoveShapeHub` class above is an implementation of a SignalR hub.</span></span> <span data-ttu-id="13f3c-162">에서처럼 합니다 [SignalR 시작](index.md) 자습서에서는 허브에 클라이언트를 직접 호출 하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-162">As in the [Getting Started with SignalR](index.md) tutorial, the hub has a method that the clients will call directly.</span></span> <span data-ttu-id="13f3c-163">이 경우 클라이언트는 새 포함 된 개체를 보냅니다 서버에 연결 된 다른 모든 클라이언트에 브로드캐스트 가져옵니다 셰이프의 X 및 Y 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-163">In this case, the client will send an object containing the new X and Y coordinates of the shape to the server, which then gets broadcasted to all other connected clients.</span></span> <span data-ttu-id="13f3c-164">SignalR은 JSON을 사용 하 여이 개체를 자동으로 직렬화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-164">SignalR will automatically serialize this object using JSON.</span></span>

    <span data-ttu-id="13f3c-165">클라이언트에 보낼 개체 (`ShapeModel`) 모양의 위치를 저장 하는 멤버가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-165">The object that will be sent to the client (`ShapeModel`) contains members to store the position of the shape.</span></span> <span data-ttu-id="13f3c-166">서버에서 개체의 버전도 멤버를 포함 추적 하는 클라이언트의 데이터가 저장 되 고, 지정된 된 클라이언트는 자체 데이터를 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-166">The version of the object on the server also contains a member to track which client's data is being stored, so that a given client won't be sent their own data.</span></span> <span data-ttu-id="13f3c-167">이 멤버를 사용 하는 `JsonIgnore` 특성에서 직렬화 되 고 클라이언트에 전송 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-167">This member uses the `JsonIgnore` attribute to keep it from being serialized and sent to the client.</span></span>
3. <span data-ttu-id="13f3c-168">다음을 시작 하면 응용 프로그램 허브를 설정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-168">Next, we'll set up the hub when the application starts.</span></span> <span data-ttu-id="13f3c-169">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | 전역 응용 프로그램 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-169">In **Solution Explorer**, right-click the project, then click **Add | Global Application Class**.</span></span> <span data-ttu-id="13f3c-170">기본 이름을 *Global* 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-170">Accept the default name of *Global* and click **OK**.</span></span>

    ![전역 응용 프로그램 클래스를 추가 합니다.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. <span data-ttu-id="13f3c-172">다음을 추가 합니다 `using` 제공 된 뒤의 문으로 **를 사용 하 여** Global.asax.cs 클래스에는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-172">Add the following `using` statement after the provided **using** statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. <span data-ttu-id="13f3c-173">코드의 다음 줄을 추가 합니다 `Application_Start` SignalR에 대 한 기본 경로 등록 하려면 전역 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="13f3c-173">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    <span data-ttu-id="13f3c-174">Global.asax 파일에는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-174">Your global.asax file should look like the following:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. <span data-ttu-id="13f3c-175">다음으로, 클라이언트가 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-175">Next, we'll add the client.</span></span> <span data-ttu-id="13f3c-176">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **추가 | 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-176">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="13f3c-177">에 **새 항목 추가** 대화 상자에서 **Html 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-177">In the **Add New Item** dialog, select **Html Page**.</span></span> <span data-ttu-id="13f3c-178">페이지는 적절 한 이름을 (같은 **Default.html**)를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-178">Give the page an appropriate name (like **Default.html**) and click **Add**.</span></span>
7. <span data-ttu-id="13f3c-179">**솔루션 탐색기**방금 만든 페이지를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-179">In **Solution Explorer**, right-click the page you just created and click **Set as Start Page**.</span></span>
8. <span data-ttu-id="13f3c-180">다음 코드 조각을 사용 하 여 HTML 페이지의 기본 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-180">Replace the default code in the HTML page with the following code snippet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="13f3c-181">스크립트 참조 Scripts 폴더에서 프로젝트에 추가 하는 패키지에 일치 하는 아래를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-181">Verify that the script references below match the packages added to your project in the Scripts folder.</span></span> <span data-ttu-id="13f3c-182">Visual Studio 2010 JQuery 및 SignalR 프로젝트에 추가 버전을 아래 버전 번호는 일치 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-182">In Visual Studio 2010, the version of JQuery and SignalR added to the project may not match the version numbers below.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    <span data-ttu-id="13f3c-183">위의 HTML 및 JavaScript 코드 셰이프라고 빨간색 Div 만듭니다, jQuery 라이브러리를 사용 하 여 셰이프 끌기 동작을 사용 하도록 설정 및 셰이프를 사용 하 여 `drag` 도형의 위치 서버로 보낼 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-183">The above HTML and JavaScript code creates a red Div called Shape, enables the shape's dragging behavior using the jQuery library, and uses the shape's `drag` event to send the shape's position to the server.</span></span>
9. <span data-ttu-id="13f3c-184">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-184">Start the application by pressing F5.</span></span> <span data-ttu-id="13f3c-185">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-185">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="13f3c-186">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-186">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a><span data-ttu-id="13f3c-188">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="13f3c-188">Add the client loop</span></span>

<span data-ttu-id="13f3c-189">위치의 모든 마우스 이동 이벤트의 셰이프를 보내는 만들어집니다는 불필요 한 네트워크 트래픽 양, 클라이언트에서 메시지를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-189">Since sending the location of the shape on every mouse move event will create an unneccesary amount of network traffic, the messages from the client need to be throttled.</span></span> <span data-ttu-id="13f3c-190">Javascript에서는 `setInterval` 고정된 요금으로 서버에 새 위치 정보를 전송 하는 루프를 설정 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-190">We'll use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="13f3c-191">이 루프는 "게임 루프의" 모든 게임 또는 기타 시뮬레이션의 기능을 구동 하는 반복적으로 호출된 된 함수는 매우 기본적인 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-191">This loop is a very basic representation of a "game loop", a repeatedly called function that drives all of the functionality of a game or other simulation.</span></span>

1. <span data-ttu-id="13f3c-192">다음 코드 조각에 맞게 HTML 페이지에서 클라이언트 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-192">Update the client code in the HTML page to match the following code snippet.</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    <span data-ttu-id="13f3c-193">위의 업데이트 추가 `updateServerModel` 고정된 빈도 호출 되는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-193">The above update adds the `updateServerModel` function, which gets called on a fixed frequency.</span></span> <span data-ttu-id="13f3c-194">이 함수는 서버에 위치 데이터를 보냅니다 때마다는 `moved` 플래그 보낼 새 위치 데이터 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-194">This function sends the position data to the server whenever the `moved` flag indicates that there is new position data to send.</span></span>
2. <span data-ttu-id="13f3c-195">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-195">Start the application by pressing F5.</span></span> <span data-ttu-id="13f3c-196">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-196">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="13f3c-197">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-197">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="13f3c-198">서버에 전송 된 메시지 수가 제한 됩니다, 되므로 애니메이션 이전 섹션과 원활 하 게 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-198">Since the number of messages that get sent to the server will be throttled, the animation will not appear as smooth as in the previous section.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a><span data-ttu-id="13f3c-200">서버 루프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-200">Add the server loop</span></span>

<span data-ttu-id="13f3c-201">현재 응용 프로그램에서 클라이언트에 서버에서 보낸 메시지 서 수신 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-201">In the current application, messages sent from the server to the client go out as often as they are received.</span></span> <span data-ttu-id="13f3c-202">클라이언트에 표시 된 대로 비슷한 문제가 필요한 연결 수 닥 결과적으로 보다 더 자주 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-202">This presents a similar problem as was seen on the client; messages can be sent more often than they are needed, and the connection could become flooded as a result.</span></span> <span data-ttu-id="13f3c-203">이 섹션에는 나가는 메시지의 속도 제한 하는 타이머를 구현 하도록 서버를 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-203">This section describes how to update the server to implement a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="13f3c-204">내용을 바꿉니다 `MoveShapeHub.cs` 다음 코드 조각을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-204">Replace the contents of `MoveShapeHub.cs` with the following code snippet.</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="13f3c-205">위의 코드를 추가 하려면 클라이언트를 확장 합니다 `Broadcaster` 나가는 제한 하는 클래스를 사용 하 여 메시지를 `Timer` .NET framework 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-205">The above code expands the client to add the `Broadcaster` class, which throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

    <span data-ttu-id="13f3c-206">자체 허브 일시적인 이므로 (만든 필요할 때마다)는 `Broadcaster` 단일 항목으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-206">Since the hub itself is transitory (it is created every time it is needed), the `Broadcaster` will be created as a singleton.</span></span> <span data-ttu-id="13f3c-207">(.NET 4에 도입 됨) 하는 초기화 지연 타이머가 시작 되기 전에 첫 번째 인스턴스에 완전히 만들지 보장, 필요할 때까지 생성을 지연 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-207">Lazy initialization (introduced in .NET 4) is used to defer its creation until it is needed, ensuring that the first hub instance is completely created before the timer is started.</span></span>

    <span data-ttu-id="13f3c-208">클라이언트에 대 한 호출 `UpdateShape` 함수는 허브의 외부로 이동 후 `UpdateModel` 메서드, 들어오는 메시지를 받을 때마다 즉시에 더 이상 해당 it 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-208">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method, so that it is no longer called immediately whenever incoming messages are received.</span></span> <span data-ttu-id="13f3c-209">초 당 25 호출의 속도로 클라이언트에 메시지를 전송할 대신 관리 하는 `_broadcastLoop` 내에서 타이머를 `Broadcaster` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-209">Instead, the messages to the clients will be sent at a rate of 25 calls per second, managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

    <span data-ttu-id="13f3c-210">허브에서 직접 클라이언트 메서드를 호출 하는 대신에 마지막으로, 합니다 `Broadcaster` 클래스를 현재 운영 허브에 대 한 참조를 입수해 야 합니다. (`_hubContext`)를 사용 하 여는 `GlobalHost`합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-210">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to obtain a reference to the currently operating hub (`_hubContext`) using the `GlobalHost`.</span></span>
2. <span data-ttu-id="13f3c-211">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-211">Start the application by pressing F5.</span></span> <span data-ttu-id="13f3c-212">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-212">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="13f3c-213">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-213">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="13f3c-214">더 이상 없습니다 브라우저의 이전 섹션에서 차이 볼 수 있지만 클라이언트에 전송 된 메시지 수가 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-214">There will not be a visible difference in the browser from the previous section, but the number of messages that get sent to the client will be throttled.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a><span data-ttu-id="13f3c-216">클라이언트에서 부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="13f3c-216">Add smooth animation on the client</span></span>

<span data-ttu-id="13f3c-217">응용 프로그램은 거의 완료 하지만 한 가지 자세한 개선, 클라이언트의 모양 동작 서버 메시지에 대 한 응답으로 이동할 때 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-217">The application is almost complete, but we could make one more improvement, in the motion of the shape on the client as it is moved in response to server messages.</span></span> <span data-ttu-id="13f3c-218">서버에서 지정 된 새 위치로 모양의 위치를 설정 하는 대신 JQuery UI 라이브러리의 사용 `animate` 현재 및 새 위치로 간에 셰이프를 원활 하 게 이동 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-218">Rather than setting the position of the shape to the new location given by the server, we'll use the JQuery UI library's `animate` function to move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="13f3c-219">클라이언트의 업데이트 `updateShape` 검색할 메서드 같은 아래 강조 표시 된 코드:</span><span class="sxs-lookup"><span data-stu-id="13f3c-219">Update the client's `updateShape` method to look like the highlighted code below:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    <span data-ttu-id="13f3c-220">위의 코드를 새 것 (이 예제의 경우 100 밀리초)에 애니메이션 간격에 걸쳐 서버에서 지정 된 이전 위치에서 셰이프를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-220">The above code moves the shape from the old location to the new one given by the server over the course of the animation interval (in this case, 100 milliseconds).</span></span> <span data-ttu-id="13f3c-221">새 애니메이션을 시작 하기 전에 셰이프를 실행 하는 모든 이전 애니메이션이 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-221">Any previous animation running on the shape is cleared before the new animation starts.</span></span>
2. <span data-ttu-id="13f3c-222">F5 키를 눌러 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-222">Start the application by pressing F5.</span></span> <span data-ttu-id="13f3c-223">페이지의 URL을 복사 하 고 두 번째 브라우저 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-223">Copy the page's URL, and paste it into a second browser window.</span></span> <span data-ttu-id="13f3c-224">브라우저 창을; 중 하나에서 셰이프를 끌어 옵니다. 다른 브라우저 창에서 모양을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-224">Drag the shape in one of the browser windows; the shape in the other browser window should move.</span></span> <span data-ttu-id="13f3c-225">다른 창에서 모양 이동 들어오는 메시지당 한 번 설정 하는 것이 아니라 시간 위로 이동을 보간 되는 대로 작은 불규칙적인 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-225">The movement of the shape in the other window should appear less jerky as its movement is interpolated over time rather than being set once per incoming message.</span></span>

    ![응용 프로그램 창](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a><span data-ttu-id="13f3c-227">추가 단계</span><span class="sxs-lookup"><span data-stu-id="13f3c-227">Further Steps</span></span>

<span data-ttu-id="13f3c-228">이 자습서에서는 클라이언트와 서버 간의 빈도가 높은 메시지를 보내는 SignalR 응용 프로그램을 프로그래밍 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-228">In this tutorial, you've learned how to program a SignalR application that sends high-frequency messages between clients and servers.</span></span> <span data-ttu-id="13f3c-229">이 통신 패러다임은 온라인 게임 및 다른 시뮬레이션와 같은 개발 하기 위한 유용한 [SignalR을 사용 하 여 만든 ShootR 게임](http://shootr.signalr.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-229">This communication paradigm is useful for developing online games and other simulations, such as [the ShootR game created with SignalR](http://shootr.signalr.net).</span></span>

<span data-ttu-id="13f3c-230">이 자습서에서 만든 전체 응용 프로그램에서 다운로드할 수 있습니다 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)합니다.</span><span class="sxs-lookup"><span data-stu-id="13f3c-230">The complete application created in this tutorial can be downloaded from [Code Gallery](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6).</span></span>

<span data-ttu-id="13f3c-231">SignalR 개발 개념에 대 한 자세한 내용은 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="13f3c-231">To learn more about SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="13f3c-232">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="13f3c-232">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="13f3c-233">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="13f3c-233">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="13f3c-234">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="13f3c-234">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
