---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: '자습서: SignalR 2 및 MVC 5를 사용 하 여 실시간 채팅 | Microsoft Docs'
author: bradygaster
description: 이 자습서에는 ASP.NET SignalR 2를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다. MVC 5 응용 프로그램에 SignalR을 추가합니다.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 1b02aecc68a93dbd6373ca5304530e76c9d0b6b5
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837003"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="32b61-104">자습서: SignalR 2 및 MVC 5를 사용 하 여 실시간 채팅</span><span class="sxs-lookup"><span data-stu-id="32b61-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="32b61-105">이 자습서에는 ASP.NET SignalR 2를 사용 하 여 실시간 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="32b61-106">SignalR MVC 5 응용 프로그램에 추가 하 고이 정보를 보내고 메시지를 표시 하는 채팅 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="32b61-107">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32b61-108">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="32b61-108">Set up the project</span></span>
> * <span data-ttu-id="32b61-109">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="32b61-109">Run the sample</span></span>
> * <span data-ttu-id="32b61-110">코드 검사</span><span class="sxs-lookup"><span data-stu-id="32b61-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="32b61-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="32b61-111">Prerequisites</span></span>

* <span data-ttu-id="32b61-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 사용 하 여 합니다 **ASP.NET 및 웹 개발** 워크 로드.</span><span class="sxs-lookup"><span data-stu-id="32b61-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="32b61-113">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="32b61-113">Set up the Project</span></span>

<span data-ttu-id="32b61-114">이 섹션에는 Visual Studio 2017 및 SignalR 2 빈 ASP.NET MVC 5 응용 프로그램, SignalR 라이브러리를 추가 및 채팅 응용 프로그램 만들기를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="32b61-115">Visual Studio에서 C# ASP.NET 응용 프로그램을.NET Framework 4.5를 대상으로 하는, SignalRChat, 이름을 만들고 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![웹 만들기](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="32b61-117">**새 ASP.NET 웹 응용 프로그램-SignalRMvcChat**를 선택 **MVC** 선택한 후 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="32b61-118">**인증 변경**를 선택 **인증 안 함** 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![인증 안 함을 선택 합니다.](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="32b61-120">**새 ASP.NET 웹 응용 프로그램-SignalRMvcChat**를 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="32b61-121">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="32b61-122">**새 항목 추가-SignalRChat**를 선택 **설치 됨** > **시각적 C#**   >  **Web**  >  **SignalR** 선택한 후 **SignalR 허브 클래스 (v2)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="32b61-123">클래스의 이름을 *ChatHub* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="32b61-124">이 단계에서는 합니다 *ChatHub.cs* 클래스 파일 및 스크립트 파일 및 프로젝트에 SignalR을 지 원하는 어셈블리 참조의 집합을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="32b61-125">새 코드를 바꿉니다 *ChatHub.cs* 이 코드를 사용 하 여 클래스 파일:</span><span class="sxs-lookup"><span data-stu-id="32b61-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="32b61-126">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 **추가** > **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="32b61-127">새 클래스 이름을 *시작* 하 고 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="32b61-128">코드를 대체 합니다 *Startup.cs* 이 코드를 사용 하 여 클래스 파일:</span><span class="sxs-lookup"><span data-stu-id="32b61-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="32b61-129">**솔루션 탐색기**를 선택 **컨트롤러** > **HomeController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="32b61-130">이 메서드를 추가 합니다 *HomeController.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="32b61-131">이 메서드는 반환 된 **채팅** 이후 단계에서 만든 뷰.</span><span class="sxs-lookup"><span data-stu-id="32b61-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="32b61-132">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **뷰** > **홈**를 선택 하 고 **추가**  >    **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="32b61-133">**뷰 추가**에서 새 뷰의 이름을 **채팅** 선택한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="32b61-134">내용을 바꿉니다 **Chat.cshtml** 이 코드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="32b61-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="32b61-135">**솔루션 탐색기**를 확장 하 고 **스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="32b61-136">JQuery 및 SignalR에 대 한 스크립트 라이브러리 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="32b61-137">패키지 관리자 SignalR 스크립트의 이후 버전이 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="32b61-138">프로젝트에서 스크립트 파일의 버전에 해당 하는 코드 블록에 대 한 스크립트 참조는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="32b61-139">원래 코드 블록에서 스크립트 참조:</span><span class="sxs-lookup"><span data-stu-id="32b61-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="32b61-140">일치 하지 않으면 업데이트 합니다 *.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="32b61-141">메뉴 모음에서 선택 **파일** > **모두 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="32b61-142">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="32b61-142">Run the Sample</span></span>

1. <span data-ttu-id="32b61-143">도구 모음에서 설정 **스크립트 디버깅** 다음 디버그 모드에서 샘플을 실행 하려면 재생 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="32b61-145">브라우저가 열리면 채팅 id에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="32b61-146">브라우저에서 URL을 복사 하 고 다른 두 브라우저를 열고 주소 표시줄에 Url을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="32b61-147">각 브라우저에서 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="32b61-148">이제 선택한 주석 추가 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="32b61-149">다른 브라우저에는 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="32b61-150">설명이는 실시간으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="32b61-151">이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="32b61-152">허브는 모든 현재 사용자에 게 의견을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="32b61-153">채팅을 나중에 조인 하는 사용자에 가입할 때부터 추가 된 메시지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="32b61-154">세 가지 다른 브라우저에서 채팅 응용 프로그램을 실행 하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="32b61-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="32b61-155">Tom, Anand, 및 Susan 메시지를 보낼 때, 모든 브라우저 실시간으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![모든 세 가지 브라우저 동일한 채팅 기록 표시](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="32b61-157">**솔루션 탐색기**를 검사 합니다 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드.</span><span class="sxs-lookup"><span data-stu-id="32b61-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="32b61-158">명명 된 스크립트 파일이 *hubs* SignalR 라이브러리는 런타임에 생성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="32b61-159">이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![스크립트 문서 노드의 hubs 스크립트 자동 생성](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="32b61-161">코드 검사</span><span class="sxs-lookup"><span data-stu-id="32b61-161">Examine the Code</span></span>

<span data-ttu-id="32b61-162">SignalR 채팅 응용 프로그램에서는 두 가지 기본 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="32b61-163">허브를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-163">It shows you how to create a hub.</span></span> <span data-ttu-id="32b61-164">서버는 주 조정 개체와 해당 허브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="32b61-165">허브는 SignalR jQuery 라이브러리를 사용 하 여 메시지 보내기 및 받기.</span><span class="sxs-lookup"><span data-stu-id="32b61-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="32b61-166">SignalR 허브를 ChatHub.cs에서</span><span class="sxs-lookup"><span data-stu-id="32b61-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="32b61-167">코드 샘플에서는 합니다 `ChatHub` 클래스에서 파생 되는 `Microsoft.AspNet.SignalR.Hub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="32b61-168">파생 된 `Hub` 클래스는 SignalR 응용 프로그램을 빌드하는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="32b61-169">허브 클래스에서 공용 메서드를 만들 수 있으며 그런 다음 웹 페이지의 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="32b61-170">채팅 코드에서 클라이언트 호출을 `ChatHub.Send` 새 메시지를 전송 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="32b61-171">허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 `Clients.All.addNewMessageToPage`입니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="32b61-172">`Send` 메서드 여러 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="32b61-173">클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="32b61-174">사용 된 `Microsoft.AspNet.SignalR.Hub.Clients` 이 허브에 연결 된 모든 클라이언트와 통신 하는 동적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="32b61-175">클라이언트에서 함수를 호출 (같은 `addNewMessageToPage` 함수) 클라이언트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="32b61-176">SignalR 및 jQuery Chat.cshtml</span><span class="sxs-lookup"><span data-stu-id="32b61-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="32b61-177">합니다 *Chat.cshtml* 코드 샘플에서 파일 보기 SignalR jQuery 라이브러리를 사용 하 여 SignalR 허브와 통신 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="32b61-178">코드는 여러 중요 한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-178">The code carries out many important tasks.</span></span> <span data-ttu-id="32b61-179">이 허브에 대 한 자동 생성 된 프록시에 대 한 참조를 만들고, 서버 클라이언트에 콘텐츠를 푸시 하려면 호출할 수 있으며 허브에 메시지를 보내기 위해 연결을 시작 하는 함수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="32b61-180">JavaScript 서버 클래스 및 해당 멤버에 대 한 참조는 camelCase 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="32b61-181">코드 샘플 참조는 C# `ChatHub` 으로 JavaScript에서 클래스 `chatHub`합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="32b61-182">이 코드 블록을 스크립트에 콜백 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="32b61-183">서버의 허브 클래스는 각 클라이언트에 콘텐츠 업데이트를 푸시 하려면이 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="32b61-184">에 대 한 선택적인 호출을 `htmlEncode` 함수 표시 방법은 HTML 페이지에 표시 하기 전에 메시지 콘텐츠를 인코딩.</span><span class="sxs-lookup"><span data-stu-id="32b61-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="32b61-185">스크립트 삽입을 방지 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="32b61-186">이 코드는 허브를 사용 하 여 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="32b61-187">이 방법을 사용 하면 이벤트 처리기 실행 되기 전에 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="32b61-188">코드는 연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 합니다 **보낼** 채팅 페이지에서 단추.</span><span class="sxs-lookup"><span data-stu-id="32b61-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="32b61-189">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="32b61-189">Get the code</span></span>

[<span data-ttu-id="32b61-190">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="32b61-190">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="32b61-191">추가 자료</span><span class="sxs-lookup"><span data-stu-id="32b61-191">Additional resources</span></span>

<span data-ttu-id="32b61-192">SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="32b61-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="32b61-193">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="32b61-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="32b61-194">SignalR GitHub 및 샘플</span><span class="sxs-lookup"><span data-stu-id="32b61-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="32b61-195">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="32b61-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="32b61-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32b61-196">Next steps</span></span>

<span data-ttu-id="32b61-197">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32b61-198">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="32b61-198">Set up the project</span></span>
> * <span data-ttu-id="32b61-199">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="32b61-199">Ran the sample</span></span>
> * <span data-ttu-id="32b61-200">코드 검사</span><span class="sxs-lookup"><span data-stu-id="32b61-200">Examined the code</span></span>

<span data-ttu-id="32b61-201">빈도가 높은 메시징 기능을 제공 하는 데 ASP.NET SignalR 2를 사용 하는 웹 응용 프로그램을 만드는 방법을 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b61-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="32b61-202">고주파 메시징을 사용 하 여 웹 앱</span><span class="sxs-lookup"><span data-stu-id="32b61-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)