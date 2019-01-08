---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: '자습서: SignalR 2를 사용 하 여 자주 실시간 앱 만들기 | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR을 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/02/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 85503db0b41be6f87136627667d6dd71f0d4f609
ms.sourcegitcommit: 97d7a00bd39c83a8f6bccb9daa44130a509f75ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54098592"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a><span data-ttu-id="afa82-103">자습서: SignalR 2를 사용 하 여 자주 실시간 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="afa82-103">Tutorial: Create high-frequency real-time app with SignalR 2</span></span>

<span data-ttu-id="afa82-104">이 자습서에는 빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR 2를 사용 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span> <span data-ttu-id="afa82-105">이 경우 "빈도가 높은 메시징" 의미 서버는 고정된 요금으로 업데이트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-105">In this case, "high-frequency messaging" means the server sends updates at a fixed rate.</span></span> <span data-ttu-id="afa82-106">초당 최대 10 개의 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-106">You send up to 10 messages a second.</span></span>

<span data-ttu-id="afa82-107">만든 응용 프로그램에 사용자를 끌 수 있는 셰이프를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-107">The application you create displays a shape that users can drag.</span></span> <span data-ttu-id="afa82-108">서버는 업데이트를 사용 하 여 끌어 온 모양의 위치와 일치 하도록 모든 연결 된 브라우저에서 모양의 위치를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-108">The server updates the position of the shape in all connected browsers to match the position of the dragged shape using timed updates.</span></span>

<span data-ttu-id="afa82-109">이 자습서에 도입 된 개념 실시간 게임에서 응용 프로그램 및 다른 시뮬레이션 응용 프로그램을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-109">Concepts introduced in this tutorial have applications in real-time gaming and other simulation applications.</span></span>

<span data-ttu-id="afa82-110">이 자습서에서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="afa82-111">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="afa82-111">Set up the project</span></span>
> * <span data-ttu-id="afa82-112">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="afa82-112">Create the base application</span></span>
> * <span data-ttu-id="afa82-113">앱 시작 시 허브에 매핑</span><span class="sxs-lookup"><span data-stu-id="afa82-113">Map to the hub when app starts</span></span>
> * <span data-ttu-id="afa82-114">클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-114">Add the client</span></span>
> * <span data-ttu-id="afa82-115">앱 실행</span><span class="sxs-lookup"><span data-stu-id="afa82-115">Run the app</span></span>
> * <span data-ttu-id="afa82-116">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-116">Add the client loop</span></span>
> * <span data-ttu-id="afa82-117">서버 루프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-117">Add the server loop</span></span>
> * <span data-ttu-id="afa82-118">부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-118">Add smooth animation</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="afa82-119">전제 조건</span><span class="sxs-lookup"><span data-stu-id="afa82-119">Prerequisites</span></span>

* <span data-ttu-id="afa82-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 사용 하 여 합니다 **ASP.NET 및 웹 개발** 워크 로드.</span><span class="sxs-lookup"><span data-stu-id="afa82-120">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="afa82-121">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="afa82-121">Set up the project</span></span>

<span data-ttu-id="afa82-122">이 섹션에서는 Visual Studio 2017에서 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-122">In this section, you create the project in Visual Studio 2017.</span></span>

<span data-ttu-id="afa82-123">이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만들고 SignalR 및 jQuery.UI 라이브러리를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-123">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application and add the SignalR and jQuery.UI libraries.</span></span>

1. <span data-ttu-id="afa82-124">Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-124">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![웹 만들기](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. <span data-ttu-id="afa82-126">에 **새 ASP.NET 웹 응용 프로그램-MoveShapeDemo** 창에서 유지 **빈** 선택 하 고 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-126">In the **New ASP.NET Web Application - MoveShapeDemo** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="afa82-127">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-127">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="afa82-128">**새 항목 추가-MoveShapeDemo**를 선택 **설치 됨** > **시각적 C#**   >  **Web**  >  **SignalR** 선택한 후 **SignalR 허브 클래스 (v2)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-128">In **Add New Item - MoveShapeDemo**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="afa82-129">클래스의 이름을 *MoveShapeHub* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-129">Name the class *MoveShapeHub* and add it to the project.</span></span>

    <span data-ttu-id="afa82-130">이 단계에서는 합니다 *MoveShapeHub.cs* 클래스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-130">This step creates the *MoveShapeHub.cs* class file.</span></span> <span data-ttu-id="afa82-131">동시에 스크립트 파일 및 프로젝트에 SignalR을 지 원하는 어셈블리 참조의 집합을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-131">Simultaneously, it adds  a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="afa82-132">선택 **도구가** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-132">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="afa82-133">**패키지 관리자 콘솔**,이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-133">In **Package Manager Console**, run this command:</span></span>

    ```console
    Install-Package jQuery.UI.Combined
    ```

    <span data-ttu-id="afa82-134">이 명령은 jQuery UI 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-134">The command installs the jQuery UI library.</span></span> <span data-ttu-id="afa82-135">도형에 애니메이션 효과를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-135">You use it to animate the shape.</span></span>

1. <span data-ttu-id="afa82-136">**솔루션 탐색기**, 스크립트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-136">In **Solution Explorer**, expand the Scripts node.</span></span>

    ![스크립트 라이브러리 참조](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    <span data-ttu-id="afa82-138">JQuery, jQueryUI, 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-138">Script libraries for jQuery, jQueryUI, and SignalR are visible in the project.</span></span>

## <a name="create-the-base-application"></a><span data-ttu-id="afa82-139">기본 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="afa82-139">Create the base application</span></span>

<span data-ttu-id="afa82-140">이 섹션에서는 브라우저 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-140">In this section, you create a browser application.</span></span> <span data-ttu-id="afa82-141">앱 서버에 각 마우스 이동 이벤트 동안 모양의 위치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-141">The app sends the location of the shape to the server during each mouse move event.</span></span> <span data-ttu-id="afa82-142">서버에는이 정보를 실시간으로 연결 된 다른 모든 클라이언트를 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-142">The server broadcasts this information to all other connected clients in real time.</span></span> <span data-ttu-id="afa82-143">이후 섹션에서이 응용 프로그램에 대 한 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-143">You learn more about this application in later sections.</span></span>

1. <span data-ttu-id="afa82-144">엽니다는 *MoveShapeHub.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-144">Open the *MoveShapeHub.cs* file.</span></span>

1. <span data-ttu-id="afa82-145">코드를 대체 합니다 *MoveShapeHub.cs* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="afa82-145">Replace the code in the *MoveShapeHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="afa82-146">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-146">Save the file.</span></span>

<span data-ttu-id="afa82-147">`MoveShapeHub` 클래스는 SignalR 허브의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-147">The `MoveShapeHub` class is an implementation of a SignalR hub.</span></span> <span data-ttu-id="afa82-148">에서처럼 합니다 [SignalR을 사용 하 여 시작](tutorial-getting-started-with-signalr.md) 자습서에서는 허브에 클라이언트를 직접 호출 하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-148">As in the [Getting Started with SignalR](tutorial-getting-started-with-signalr.md) tutorial, the hub has a method that the clients call directly.</span></span> <span data-ttu-id="afa82-149">이 경우 새 X 및 Y를 사용 하 여 개체를 서버로 셰이프 조정 하는 클라이언트 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-149">In this case, the client sends an object with the new X and Y coordinates of the shape to the server.</span></span> <span data-ttu-id="afa82-150">이러한 좌표는 연결 된 다른 모든 클라이언트에 브로드캐스트 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-150">Those coordinates get broadcasted to all other connected clients.</span></span> <span data-ttu-id="afa82-151">SignalR은 자동으로 JSON을 사용 하 여이 개체를 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-151">SignalR automatically serializes this object using JSON.</span></span>

<span data-ttu-id="afa82-152">앱 보내기는 `ShapeModel` 클라이언트 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-152">The app sends the `ShapeModel` object to the client.</span></span> <span data-ttu-id="afa82-153">모양의 위치를 저장 하는 멤버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-153">It has members to store the position of the shape.</span></span> <span data-ttu-id="afa82-154">또한 서버에서 개체의 버전이 저장 되는 클라이언트의 데이터 추적에 멤버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-154">The version of the object on the server also has a member to track which client's data is being stored.</span></span> <span data-ttu-id="afa82-155">이 개체는 서버 자체를 다시 클라이언트의 데이터를 보내지 못하도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-155">This object prevents the server from sending a client's data back to itself.</span></span> <span data-ttu-id="afa82-156">이 멤버를 사용 하는 `JsonIgnore` 에서 데이터를 직렬화 및 다시 클라이언트로 보내는 응용 프로그램을 유지 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-156">This member uses the `JsonIgnore` attribute to keep the application from serializing the data and sending it back to the client.</span></span>

## <a name="map-to-the-hub-when-app-starts"></a><span data-ttu-id="afa82-157">앱 시작 시 허브에 매핑</span><span class="sxs-lookup"><span data-stu-id="afa82-157">Map to the hub when app starts</span></span>

<span data-ttu-id="afa82-158">다음으로 허브에 대 한 매핑 때 설정한 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-158">Next, you set up mapping to the hub when the application starts.</span></span> <span data-ttu-id="afa82-159">SignalR 2에 OWIN 시작 클래스 추가 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-159">In SignalR 2, adding an OWIN startup class creates the mapping.</span></span>

1. <span data-ttu-id="afa82-160">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-160">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="afa82-161">**새 항목 추가-MoveShapeDemo** 선택 **설치 됨** > **시각적 C#**   >  **Web** 차례로 선택 **OWIN Startup 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-161">In **Add New Item - MoveShapeDemo** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="afa82-162">클래스의 이름을 *시동* 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-162">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="afa82-163">기본 코드를 대체 합니다 *Startup.cs* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="afa82-163">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

<span data-ttu-id="afa82-164">OWIN 시작 클래스 호출 `MapSignalR` 앱을 실행 하는 경우는 `Configuration` 메서드.</span><span class="sxs-lookup"><span data-stu-id="afa82-164">The OWIN startup class calls `MapSignalR` when the app executes the `Configuration` method.</span></span> <span data-ttu-id="afa82-165">OWIN의 시작 클래스 처리를 사용 하 여 앱 추가 `OwinStartup` 어셈블리 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-165">The app adds the class to OWIN's startup process using the `OwinStartup` assembly attribute.</span></span>

## <a name="add-the-client"></a><span data-ttu-id="afa82-166">클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-166">Add the client</span></span>

<span data-ttu-id="afa82-167">클라이언트에 대 한 HTML 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-167">Add the HTML page for the client.</span></span>

1. <span data-ttu-id="afa82-168">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **HTML 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-168">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="afa82-169">페이지의 이름을 **기본** 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-169">Name the page **Default** and select **OK**.</span></span>

1. <span data-ttu-id="afa82-170">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *Default.html* 선택한 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-170">In **Solution Explorer**, right-click *Default.html* and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="afa82-171">기본 코드를 대체 합니다 *Default.html* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="afa82-171">Replace the default code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. <span data-ttu-id="afa82-172">**솔루션 탐색기**를 확장 하 고 **스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-172">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="afa82-173">JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-173">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="afa82-174">패키지 관리자 SignalR 스크립트의 이후 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-174">The package manager installs a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="afa82-175">프로젝트에서 스크립트 파일의 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-175">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

<span data-ttu-id="afa82-176">이 HTML 및 JavaScript 코드에서는 빨간색 `div` 호출 `shape`합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-176">This HTML and JavaScript code creates a red `div` called `shape`.</span></span> <span data-ttu-id="afa82-177">JQuery 라이브러리를 사용 하 여 셰이프 끌기 동작을 사용 하도록 설정 하 고 사용 하 여 `drag` 도형의 위치 서버로 보낼 이벤트.</span><span class="sxs-lookup"><span data-stu-id="afa82-177">It enables the shape's dragging behavior using the jQuery library and uses the `drag` event to send the shape's position to the server.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="afa82-178">앱 실행</span><span class="sxs-lookup"><span data-stu-id="afa82-178">Run the app</span></span>

<span data-ttu-id="afa82-179">앱을 실행할 수 있습니다 se'e에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-179">You can run the app to se\`e it work.</span></span> <span data-ttu-id="afa82-180">브라우저 창 주위 셰이프를 끌어 놓으면 다른 브라우저에서 셰이프 너무 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-180">When you drag the shape around a browser window, the shape moves in the other browsers too.</span></span>

1. <span data-ttu-id="afa82-181">도구 모음에서 설정 **스크립트 디버깅** 다음 디버그 모드에서 응용 프로그램을 실행 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-181">In the toolbar, turn on **Script Debugging** and then select the play button to run the application in Debug mode.</span></span>

    ![디버깅 모드 켜기 재생을 선택 하는 사용자의 스크린샷.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    <span data-ttu-id="afa82-183">오른쪽 위 모퉁이에 있는 빨간색 셰이프를 사용 하 여 브라우저 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-183">A browser window opens with the red shape in the upper-right corner.</span></span>

1. <span data-ttu-id="afa82-184">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-184">Copy the page's URL.</span></span>

1. <span data-ttu-id="afa82-185">다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-185">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="afa82-186">브라우저 창 중 하나에서 셰이프를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-186">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="afa82-187">다른 브라우저 창에서 셰이프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-187">The shape in the other browser window follows.</span></span>

<span data-ttu-id="afa82-188">응용 프로그램을 하는 동안이 메서드를 사용 하 여 함수를 하지 권장 되는 프로그래밍 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-188">While the application functions using this method, it's not a recommended programming model.</span></span> <span data-ttu-id="afa82-189">보낸 시작 메시지의 수는 상한 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-189">There's no upper limit to the number of messages getting sent.</span></span> <span data-ttu-id="afa82-190">결과적으로, 클라이언트와 서버가 가져올 메시지로 인해 과부하가 걸리면 및 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-190">As a result, the clients and server get overwhelmed with messages and performance degrades.</span></span> <span data-ttu-id="afa82-191">또한 앱 클라이언트에서 연결 되지 않은 애니메이션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-191">Also, the app displays a disjointed animation on the client.</span></span> <span data-ttu-id="afa82-192">이 불규칙적인 애니메이션 셰이프 각 메서드에 의해 즉시 이동 하기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-192">This jerky animation happens because the shape moves instantly by each method.</span></span> <span data-ttu-id="afa82-193">셰이프 원활 하 게 각 새 위치로 이동 하는 경우에 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-193">It's better if the shape moves smoothly to each new location.</span></span> <span data-ttu-id="afa82-194">다음으로, 해당 문제를 해결 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-194">Next, you learn how to fix those issues.</span></span>

## <a name="add-the-client-loop"></a><span data-ttu-id="afa82-195">클라이언트 루프 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-195">Add the client loop</span></span>

<span data-ttu-id="afa82-196">모든 마우스 이동 이벤트의 셰이프를 위치의 보내기는 불필요 한 네트워크 트래픽 양에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-196">Sending the location of the shape on every mouse move event creates an unnecessary amount of network traffic.</span></span> <span data-ttu-id="afa82-197">앱은 클라이언트에서 메시지를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-197">The app needs to throttle the messages from the client.</span></span>

<span data-ttu-id="afa82-198">Javascript를 사용 하 여 `setInterval` 고정된 요금으로 서버에 새 위치 정보를 전송 하는 루프를 설정 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-198">Use the javascript `setInterval` function to set up a loop that sends new position information to the server at a fixed rate.</span></span> <span data-ttu-id="afa82-199">이 루프는 "게임 루프입니다."의 기본 표현</span><span class="sxs-lookup"><span data-stu-id="afa82-199">This loop is a basic representation of a "game loop."</span></span> <span data-ttu-id="afa82-200">반복적으로 호출된 된 함수는 게임의 모든 기능을 구동 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-200">It's a repeatedly called function that drives all the functionality of a game.</span></span>

1. <span data-ttu-id="afa82-201">클라이언트 코드를 대체 합니다 *Default.html* 이 코드를 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="afa82-201">Replace the client code in the *Default.html* file with this code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > <span data-ttu-id="afa82-202">스크립트 파일에 대 한 참조를 다시 대체 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-202">You have to replace the script references again.</span></span> <span data-ttu-id="afa82-203">프로젝트의 스크립트 버전이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-203">They must match the versions of the scripts in the project.</span></span>

    <span data-ttu-id="afa82-204">이 새 코드를 추가 합니다 `updateServerModel` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-204">This new code adds the `updateServerModel` function.</span></span> <span data-ttu-id="afa82-205">고정 된 빈도에 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-205">It gets called on a fixed frequency.</span></span> <span data-ttu-id="afa82-206">함수는 서버에 위치 데이터를 보냅니다 때마다는 `moved` 플래그 보낼 새 위치 데이터 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-206">The function sends the position data to the server whenever the `moved` flag indicates that there's new position data to send.</span></span>

1. <span data-ttu-id="afa82-207">응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-207">Select the play button to start the application</span></span>

1. <span data-ttu-id="afa82-208">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-208">Copy the page's URL.</span></span>

1. <span data-ttu-id="afa82-209">다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-209">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="afa82-210">브라우저 창 중 하나에서 셰이프를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-210">Drag the shape in one of the browser windows.</span></span> <span data-ttu-id="afa82-211">다른 브라우저 창에서 셰이프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-211">The shape in the other browser window follows.</span></span>

<span data-ttu-id="afa82-212">앱에 전송 된 서버를 애니메이션으로 부드러운 나타나지 메시지 수가 제한 되므로 처음 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-212">Since the app throttles the number of messages that get sent to the server, the animation won't appear as smooth did at first.</span></span>

## <a name="add-the-server-loop"></a><span data-ttu-id="afa82-213">서버 루프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-213">Add the server loop</span></span>

<span data-ttu-id="afa82-214">현재 응용 프로그램에서 서버에서 클라이언트로 전송 된 메시지 서 수신 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-214">In the current application, messages sent from the server to the client go out as often as they're received.</span></span> <span data-ttu-id="afa82-215">이 네트워크 트래픽을 클라이언트에서 볼 수 있듯이 유사한 문제를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-215">This network traffic presents a similar problem as we see on the client.</span></span>

<span data-ttu-id="afa82-216">필요한 것 보다 더 자주 앱 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-216">The app can send messages more often than they're needed.</span></span> <span data-ttu-id="afa82-217">결과적으로 연결이 플 러 딩 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-217">The connection can become flooded as a result.</span></span> <span data-ttu-id="afa82-218">이 섹션에는 나가는 메시지의 속도 제한 하는 타이머를 추가 하려면 서버를 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-218">This section describes how to update the server to add a timer that throttles the rate of the outgoing messages.</span></span>

1. <span data-ttu-id="afa82-219">내용을 바꿉니다 `MoveShapeHub.cs` 이 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="afa82-219">Replace the contents of `MoveShapeHub.cs` with this code:</span></span>

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. <span data-ttu-id="afa82-220">응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-220">Select the play button to start the application.</span></span>

1. <span data-ttu-id="afa82-221">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-221">Copy the page's URL.</span></span>

1. <span data-ttu-id="afa82-222">다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-222">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="afa82-223">브라우저 창 중 하나에서 셰이프를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-223">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="afa82-224">이 코드를 추가 하는 클라이언트를 확장 합니다 `Broadcaster` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-224">This code expands the client to add the `Broadcaster` class.</span></span> <span data-ttu-id="afa82-225">새 클래스를 사용 하 여 나가는 메시지를 제한 합니다 `Timer` .NET framework 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-225">The new class throttles the outgoing messages using the `Timer` class from the .NET framework.</span></span>

<span data-ttu-id="afa82-226">자체 허브 일시적인을 학습 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-226">It's good to learn that the hub itself is transitory.</span></span> <span data-ttu-id="afa82-227">필요할 때마다 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-227">It's created every time it's needed.</span></span> <span data-ttu-id="afa82-228">앱은 하므로 `Broadcaster` 단일 항목으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-228">So the app creates the `Broadcaster` as a singleton.</span></span> <span data-ttu-id="afa82-229">초기화 지연을 사용 하 여 지연 된 `Broadcaster`의 필요할 때까지 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-229">It uses lazy initialization to defer the `Broadcaster`'s creation until it's needed.</span></span> <span data-ttu-id="afa82-230">앱은 첫 번째 인스턴스에 완전히 타이머를 시작 하기 전에 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-230">That guarantees that the app creates the first hub instance completely before starting the timer.</span></span>

<span data-ttu-id="afa82-231">클라이언트에 대 한 호출 `UpdateShape` 함수는 허브의 외부로 이동 후 `UpdateModel` 메서드.</span><span class="sxs-lookup"><span data-stu-id="afa82-231">The call to the clients' `UpdateShape` function is then moved out of the hub's `UpdateModel` method.</span></span> <span data-ttu-id="afa82-232">더 이상 앱 들어오는 메시지를 수신 될 때마다 즉시 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-232">It's no longer called immediately whenever the app receives incoming messages.</span></span> <span data-ttu-id="afa82-233">대신 앱 초 당 25 호출의 속도로 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-233">Instead, the app sends the messages to the clients at a rate of 25 calls per second.</span></span> <span data-ttu-id="afa82-234">프로세스에서 관리 되는 `_broadcastLoop` 내에서 타이머를 `Broadcaster` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-234">The process is  managed by the `_broadcastLoop` timer from within the `Broadcaster` class.</span></span>

<span data-ttu-id="afa82-235">허브에서 직접 클라이언트 메서드를 호출 하는 대신에 마지막으로, 합니다 `Broadcaster` 클래스는 현재 운영 체제에 대 한 참조를 가져올 해야 `_hubContext` 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-235">Lastly, instead of calling the client method from the hub directly, the `Broadcaster` class needs to get a reference to the currently operating `_hubContext` hub.</span></span> <span data-ttu-id="afa82-236">사용 하 여 참조를 가져옵니다는 `GlobalHost`합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-236">It gets the reference with the `GlobalHost`.</span></span>

## <a name="add-smooth-animation"></a><span data-ttu-id="afa82-237">부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-237">Add smooth animation</span></span>

<span data-ttu-id="afa82-238">거의 완료 되 면 응용 프로그램 이지만 하나 더 개선 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-238">The application is almost finished, but we could make one more improvement.</span></span> <span data-ttu-id="afa82-239">앱 서버 메시지에 따라에서 클라이언트에서 셰이프를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-239">The app moves the shape on the client in response to server messages.</span></span> <span data-ttu-id="afa82-240">서버에서 지정 된 새 위치로 모양의 위치를 설정 하는 대신 JQuery UI 라이브러리를 사용 하 여 `animate` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-240">Instead of setting the position of the shape to the new location given by the server, use the JQuery UI library's `animate` function.</span></span> <span data-ttu-id="afa82-241">셰이프 현재 및 새 위치로 간에 원활 하 게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-241">It can move the shape smoothly between its current and new position.</span></span>

1. <span data-ttu-id="afa82-242">클라이언트의 업데이트 `updateShape` 의 메서드를 *Default.html* 파일을 강조 표시 된 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-242">Update the client's `updateShape` method in the *Default.html* file to look like the highlighted code:</span></span>

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. <span data-ttu-id="afa82-243">응용 프로그램을 시작 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-243">Select the play button to start the application.</span></span>

1. <span data-ttu-id="afa82-244">페이지의 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-244">Copy the page's URL.</span></span>

1. <span data-ttu-id="afa82-245">다른 브라우저를 열고 주소 표시줄에 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-245">Open another browser and paste the URL into the address bar.</span></span>

1. <span data-ttu-id="afa82-246">브라우저 창 중 하나에서 셰이프를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-246">Drag the shape in one of the browser windows.</span></span>

<span data-ttu-id="afa82-247">다른 창에서 모양 이동 덜 불규칙적인 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-247">The movement of the shape in the other window appears less jerky.</span></span> <span data-ttu-id="afa82-248">앱을 통해 들어오는 메시지당 한 번 설정 하는 것이 아니라 시간 이동을 보간합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-248">The app interpolates its movement over time rather than being set once per incoming message.</span></span>

<span data-ttu-id="afa82-249">이 코드의 이전 위치에서 새 셰이프를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-249">This code moves the shape from the old location to the new one.</span></span> <span data-ttu-id="afa82-250">애니메이션 간격에 걸쳐 모양의 위치를 제공 하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-250">The server gives the position of the shape over the course of the animation interval.</span></span> <span data-ttu-id="afa82-251">이 경우에은 100 밀리초입니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-251">In this case, that's 100 milliseconds.</span></span> <span data-ttu-id="afa82-252">앱을 새 애니메이션을 시작 하기 전에 셰이프를 실행 하는 모든 이전 애니메이션을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-252">The app clears any previous animation running on the shape before the new animation starts.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="afa82-253">추가 자료</span><span class="sxs-lookup"><span data-stu-id="afa82-253">Additional resources</span></span>

<span data-ttu-id="afa82-254">방금 알아본 통신 패러다임은 온라인 게임 및 다른 시뮬레이션 같은 개발 하기 위한 유용한 [SignalR을 사용 하 여 만든 ShootR 게임](https://shootr.azurewebsites.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-254">The communication paradigm you just learned about is useful for developing online games and other simulations, like [the ShootR game created with SignalR](https://shootr.azurewebsites.net/).</span></span>

<span data-ttu-id="afa82-255">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="afa82-255">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="afa82-256">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="afa82-256">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="afa82-257">SignalR GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="afa82-257">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="afa82-258">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="afa82-258">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="afa82-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="afa82-259">Next steps</span></span>

<span data-ttu-id="afa82-260">이 자습서에서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-260">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="afa82-261">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="afa82-261">Set up the project</span></span>
> * <span data-ttu-id="afa82-262">기본 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-262">Created the base application</span></span>
> * <span data-ttu-id="afa82-263">앱 시작 시 허브에 매핑</span><span class="sxs-lookup"><span data-stu-id="afa82-263">Mapped to the hub when app starts</span></span>
> * <span data-ttu-id="afa82-264">클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-264">Added the client</span></span>
> * <span data-ttu-id="afa82-265">앱 실행</span><span class="sxs-lookup"><span data-stu-id="afa82-265">Ran the app</span></span>
> * <span data-ttu-id="afa82-266">클라이언트 루프를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-266">Added the client loop</span></span>
> * <span data-ttu-id="afa82-267">서버 루프를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="afa82-267">Added the server loop</span></span>
> * <span data-ttu-id="afa82-268">부드러운 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="afa82-268">Added smooth animation</span></span>

<span data-ttu-id="afa82-269">ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법에 알아보려면 다음 문서로 계속 진행 하세요.</span><span class="sxs-lookup"><span data-stu-id="afa82-269">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="afa82-270">SignalR 2 및 서버 브로드캐스트</span><span class="sxs-lookup"><span data-stu-id="afa82-270">SignalR 2 and server broadcasting</span></span>](tutorial-server-broadcast-with-signalr.md)