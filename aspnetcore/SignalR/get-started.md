---
title: SignalR에서 ASP.NET Core 시작
author: rachelappel
description: 이 자습서에서는 ASP.NET Core 용 SignalR을 사용 하 여 응용 프로그램을 만듭니다.
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/16/2018
ms.prod: aspnet-core
ms.topic: tutorial
ms.technology: aspnet
uid: signalr/get-started
ms.openlocfilehash: cf120d535c85c7871f5b1f27039018ea2405b9cb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="get-started-with-signalr-on-aspnet-core"></a><span data-ttu-id="7afcd-103">SignalR에서 ASP.NET Core 시작</span><span class="sxs-lookup"><span data-stu-id="7afcd-103">Get started with SignalR on ASP.NET Core</span></span>

<span data-ttu-id="7afcd-104">작성자: [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="7afcd-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

[!INCLUDE [Version notice](../includes/signalr-version-notice.md)]

<span data-ttu-id="7afcd-105">이 자습서의 ASP.NET Core 용 SignalR을 사용 하 여 실시간 앱 빌드 기본 사항에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-105">This tutorial teaches the basics of building a real-time app using SignalR for ASP.NET Core.</span></span>

   ![솔루션](get-started/_static/signalr-get-started-finished.png)

<span data-ttu-id="7afcd-107">이 자습서에서는 다음 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-107">This tutorial demonstrates the following SignalR development tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7afcd-108">ASP.NET Core 웹 앱에는 SignalR을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-108">Create a SignalR on ASP.NET Core web app.</span></span>
> * <span data-ttu-id="7afcd-109">클라이언트에 콘텐츠를 푸시 하려면 SignalR 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-109">Create a SignalR hub to push content to clients.</span></span>
> * <span data-ttu-id="7afcd-110">수정 된 `Startup` 클래스 및 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-110">Modify the `Startup` class and configure the app.</span></span>

<span data-ttu-id="7afcd-111">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="7afcd-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="prerequisites"></a><span data-ttu-id="7afcd-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="7afcd-112">Prerequisites</span></span>

<span data-ttu-id="7afcd-113">다음 소프트웨어를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-113">Install the following software:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7afcd-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7afcd-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="7afcd-115">[.NET core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) 이상 버전</span><span class="sxs-lookup"><span data-stu-id="7afcd-115">[.NET Core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) or later</span></span>
* <span data-ttu-id="7afcd-116">[Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.6 이상 버전에서 **ASP.NET 및 웹 개발** 작업</span><span class="sxs-lookup"><span data-stu-id="7afcd-116">[Visual Studio 2017](https://www.visualstudio.com/downloads/) version 15.6 or later with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="7afcd-117">npm</span><span class="sxs-lookup"><span data-stu-id="7afcd-117">npm</span></span>](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="7afcd-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7afcd-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="7afcd-119">[.NET core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) 이상 버전</span><span class="sxs-lookup"><span data-stu-id="7afcd-119">[.NET Core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) or later</span></span>
* [<span data-ttu-id="7afcd-120">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7afcd-120">Visual Studio Code</span></span>](https://code.visualstudio.com/download) 
* [<span data-ttu-id="7afcd-121">Visual Studio 코드에 대 한 C#</span><span class="sxs-lookup"><span data-stu-id="7afcd-121">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [<span data-ttu-id="7afcd-122">npm</span><span class="sxs-lookup"><span data-stu-id="7afcd-122">npm</span></span>](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a><span data-ttu-id="7afcd-123">SignalR 클라이언트와 서버를 호스팅하는 ASP.NET Core 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7afcd-123">Create an ASP.NET Core project that hosts SignalR client and server</span></span>

#### <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7afcd-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7afcd-124">Visual Studio</span></span>](#tab/visual-studio/)
1. <span data-ttu-id="7afcd-125">사용 하 여는 **파일** > **새 프로젝트** 메뉴 옵션 선택한 **ASP.NET Core 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-125">Use the **File** > **New Project** menu option and choose **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="7afcd-126">프로젝트 이름을 *SignalRChat*합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-126">Name the project *SignalRChat*.</span></span>

   ![Visual Studio에서 새 프로젝트 대화 상자](get-started/_static/signalr-new-project-dialog.png)

2. <span data-ttu-id="7afcd-128">선택 **웹 응용 프로그램** Razor 페이지를 사용 하 여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-128">Select **Web Application** to create a project using Razor Pages.</span></span> <span data-ttu-id="7afcd-129">그런 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-129">Then select **OK**.</span></span> <span data-ttu-id="7afcd-130">수 있도록 **ASP.NET Core 2.1** SignalR 이전 버전의.NET에서 실행 하는 경우 프레임 워크 선택기에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-130">Be sure that **ASP.NET Core 2.1** is selected from the framework selector, though SignalR runs on older versions of .NET.</span></span>

   ![Visual Studio에서 새 프로젝트 대화 상자](get-started/_static/signalr-new-project-choose-type.png)

3. <span data-ttu-id="7afcd-132">프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** > **추가** > **새 항목** > **npm 구성 파일** .</span><span class="sxs-lookup"><span data-stu-id="7afcd-132">Right-click the project in **Solution Explorer** > **Add** > **New Item** > **npm Configuration File**.</span></span> <span data-ttu-id="7afcd-133">파일 이름을 *package.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-133">Name the file *package.json*.</span></span>

4. <span data-ttu-id="7afcd-134">다음 명령을 실행 하는 **패키지 관리자 콘솔** 프로젝트 루트에서 창:</span><span class="sxs-lookup"><span data-stu-id="7afcd-134">Run the following command in the **Package Manager Console** window, from the project root:</span></span>

    ```console
      npm install @aspnet/signalr
    ```
5. <span data-ttu-id="7afcd-135">복사는 <em>signalr.js</em> 에서 파일을 <em>node_modules\\ @aspnet\signalr\dist\browser</em>  에 <em>wwwroot\lib</em> 프로젝트의 폴더에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-135">Copy the <em>signalr.js</em> file from <em>node_modules\\@aspnet\signalr\dist\browser</em> to the <em>wwwroot\lib</em> folder in your project.</span></span>

#### <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="7afcd-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7afcd-136">Visual Studio Code</span></span>](#tab/visual-studio-code/)
1. <span data-ttu-id="7afcd-137">**통합 터미널**, 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-137">From the **Integrated Terminal**, run the following command:</span></span>

    ```console
      dotnet new razor -o SignalRChat
    ```

2. <span data-ttu-id="7afcd-138">사용 하 여 JavaScript 클라이언트 라이브러리를 설치 *npm*합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-138">Install the JavaScript client library using *npm*.</span></span>

    ```
      npm init -y
      npm install @aspnet/signalr
    ```

* * *
## <a name="create-the-signalr-hub"></a><span data-ttu-id="7afcd-139">SignalR 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-139">Create the SignalR Hub</span></span>

<span data-ttu-id="7afcd-140">허브는 클라이언트와 서버에서 다른 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인으로 사용 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-140">A hub is a class that serves as a high-level pipeline that allows the client and server to call methods on each other.</span></span>

#### <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7afcd-141">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7afcd-141">Visual Studio</span></span>](#tab/visual-studio/)
1. <span data-ttu-id="7afcd-142">클래스를 선택 하 여 프로젝트에 추가 **파일** > **새로** > **파일** 선택 하 고 **Visual C# 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-142">Add a class to the project by choosing **File** > **New** > **File** and selecting **Visual C# Class**.</span></span>

2. <span data-ttu-id="7afcd-143">상속 `Microsoft.AspNetCore.SignalR.Hub`합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-143">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="7afcd-144">`Hub` 속성과 송신 및 수신 데이터 뿐 아니라 연결 그룹을 관리 하기 위한 이벤트 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-144">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data.</span></span>

3. <span data-ttu-id="7afcd-145">만들기는 `SendMessage` 모든 연결 된 채팅 클라이언트에 메시지를 보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-145">Create the `SendMessage` method that sends a message to all connected chat clients.</span></span> <span data-ttu-id="7afcd-146">반환 확인는 [작업](https://msdn.microsoft.com/en-us/library/system.threading.tasks.task(v=vs.110).aspx)SignalR 비동기 이기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-146">Notice it returns a [Task](https://msdn.microsoft.com/en-us/library/system.threading.tasks.task(v=vs.110).aspx), because SignalR is asynchronous.</span></span> <span data-ttu-id="7afcd-147">비동기 코드 확장성이 좋아집니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-147">Asynchronous code scales better.</span></span>

   [!code-csharp[Startup](get-started/sample/Hubs/ChatHub.cs?range=7-14)]

#### <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="7afcd-148">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7afcd-148">Visual Studio Code</span></span>](#tab/visual-studio-code/)
1. <span data-ttu-id="7afcd-149">열기는 *SignalRChat* Visual Studio Code에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-149">Open the *SignalRChat* folder in Visual Studio Code.</span></span>

2. <span data-ttu-id="7afcd-150">클래스를 선택 하 여 프로젝트에 추가 **파일** > **새 파일** 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-150">Add a class to the project by selecting **File** > **New File** from the menu.</span></span>

3. <span data-ttu-id="7afcd-151">상속 `Microsoft.AspNetCore.SignalR.Hub`합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-151">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="7afcd-152">`Hub` 속성 및 이벤트 데이터를 클라이언트로 보내는 소켓과 받는 뿐 아니라 연결 그룹을 관리 하기 위한 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-152">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data to clients.</span></span>

4. <span data-ttu-id="7afcd-153">클래스에 `SendMessage` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-153">Add a `SendMessage` method to the class.</span></span> <span data-ttu-id="7afcd-154">`SendMessage` 메서드는 모든 연결 된 채팅 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-154">The `SendMessage` method sends a message to all connected chat clients.</span></span> <span data-ttu-id="7afcd-155">반환 확인는 [작업](/dotnet/api/system.threading.tasks.task)SignalR 비동기 이기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-155">Notice it returns a [Task](/dotnet/api/system.threading.tasks.task), because SignalR is asynchronous.</span></span> <span data-ttu-id="7afcd-156">비동기 코드 확장성이 좋아집니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-156">Asynchronous code scales better.</span></span>

   [!code-csharp[Startup](get-started/sample/Hubs/ChatHub.cs?range=7-14)]

* * *
## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="7afcd-157">SignalR을 사용 하도록 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-157">Configure the project to use SignalR</span></span>

<span data-ttu-id="7afcd-158">SignalR 서버 signalr 요청을 전달 하려면 알 수 있도록 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-158">The SignalR server must be configured so that it knows to pass requests to SignalR.</span></span>

1. <span data-ttu-id="7afcd-159">SignalR 프로젝트를 구성 하려면 프로젝트의 수정 `Startup.ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="7afcd-159">To configure a SignalR project, modify the project's `Startup.ConfigureServices` method.</span></span>

   <span data-ttu-id="7afcd-160">`services.AddSignalR` SignalR의 일부로 추가 [미들웨어](xref:fundamentals/middleware/index) 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="7afcd-160">`services.AddSignalR` adds SignalR as part of the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

2. <span data-ttu-id="7afcd-161">사용 하 여 허브에 대 한 라우팅을 구성 `UseSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-161">Configure routes to your hubs using `UseSignalR`.</span></span>

   [!code-csharp[Startup](get-started/sample/Startup.cs?highlight=22,40-43)]

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="7afcd-162">SignalR 클라이언트 코드 만들기</span><span class="sxs-lookup"><span data-stu-id="7afcd-162">Create the SignalR client code</span></span>

1. <span data-ttu-id="7afcd-163">에서는 교체 *Pages\Index.cshtml* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7afcd-163">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

   [!code-cshtml[Index](get-started/sample/Pages/Index.cshtml)]

   <span data-ttu-id="7afcd-164">위의 HTML 이름 및 메시지 필드 및 전송 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-164">The preceding HTML displays name and message fields, and a submit button.</span></span> <span data-ttu-id="7afcd-165">맨 아래에 스크립트 참조를 확인: SignalR에 대 한 참조 및 *chat.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-165">Notice the script references at the bottom: a reference to SignalR and *chat.js*.</span></span>

2. <span data-ttu-id="7afcd-166">명명 된 JavaScript 파일을 추가 *chat.js*을 *wwwroot\js* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-166">Add a JavaScript file, named *chat.js*, to the *wwwroot\js* folder.</span></span> <span data-ttu-id="7afcd-167">파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-167">Add the following code to it:</span></span>

   [!code-javascript[Index](get-started/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a><span data-ttu-id="7afcd-168">앱 실행</span><span class="sxs-lookup"><span data-stu-id="7afcd-168">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7afcd-169">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7afcd-169">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="7afcd-170">선택 **디버그** > **디버깅 하지 않고 시작** 브라우저를 실행 하 여 로컬 웹 사이트를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-170">Select **Debug** > **Start without debugging** to launch a browser and load the website locally.</span></span> <span data-ttu-id="7afcd-171">주소 표시줄에서 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-171">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="7afcd-172">다른 브라우저 인스턴스 (모든 브라우저)를 열고 주소 표시줄에 URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-172">Open another browser instance (any browser) and paste the URL in the address bar.</span></span>

1. <span data-ttu-id="7afcd-173">브라우저 중 하나를 선택 하 고, 이름 및 메시지를 입력 한 다음 클릭는 **보낼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-173">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="7afcd-174">이름 및 메시지는 두 페이지에 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-174">The name and message are displayed on both pages instantly.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="7afcd-175">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7afcd-175">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="7afcd-176">**디버그**(F5) 키를 눌러 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-176">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="7afcd-177">프로그램을 실행 브라우저 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-177">Running the program opens a browser window.</span></span>

1. <span data-ttu-id="7afcd-178">다른 브라우저 창을 열고에서 로컬로 웹 사이트를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-178">Open another browser window and load the website locally in it.</span></span>

1. <span data-ttu-id="7afcd-179">브라우저 중 하나를 선택 하 고, 이름 및 메시지를 입력 한 다음 클릭는 **보낼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-179">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="7afcd-180">이름 및 메시지는 두 페이지에 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7afcd-180">The name and message are displayed on both pages instantly.</span></span>

-----

  ![솔루션](get-started/_static/signalr-get-started-finished.png)

## <a name="related-resources"></a><span data-ttu-id="7afcd-182">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="7afcd-182">Related resources</span></span>

[<span data-ttu-id="7afcd-183">ASP.NET Core SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="7afcd-183">Introduction to ASP.NET Core SignalR</span></span>](introduction.md)