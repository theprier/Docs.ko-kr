---
title: ASP.NET Core에서 SignalR 시작
author: rachelappel
description: 이 자습서에서는 ASP.NET Core용 SignalR을 사용하여 앱을 만듭니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/22/2018
uid: tutorials/signalr
ms.openlocfilehash: ca9145d9e16c23e34bbc1d84ff01ce02709187ce
ms.sourcegitcommit: 08f1a9baa97060da5168840b332c9c0805b5f901
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37144874"
---
# <a name="get-started-with-signalr-on-aspnet-core"></a><span data-ttu-id="5027f-103">ASP.NET Core에서 SignalR 시작</span><span class="sxs-lookup"><span data-stu-id="5027f-103">Get started with SignalR on ASP.NET Core</span></span>

<span data-ttu-id="5027f-104">작성자: [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="5027f-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="5027f-105">이 자습서에서는 ASP.NET Core용 SignalR을 사용하여 실시간 앱을 빌드하는 방법에 대한 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-105">This tutorial teaches the basics of building a real-time app using SignalR for ASP.NET Core.</span></span>

   ![솔루션](signalr/_static/signalr-get-started-finished.png)

<span data-ttu-id="5027f-107">이 자습서에서는 다음과 같은 SignalR 개발 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-107">This tutorial demonstrates the following SignalR development tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5027f-108">ASP.NET Core 웹앱에서 SignalR을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-108">Create a SignalR on ASP.NET Core web app.</span></span>
> * <span data-ttu-id="5027f-109">클라이언트에 콘텐츠를 푸시하는 SignalR Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-109">Create a SignalR hub to push content to clients.</span></span>
> * <span data-ttu-id="5027f-110">`Startup` 클래스를 수정하고 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-110">Modify the `Startup` class and configure the app.</span></span>

<span data-ttu-id="5027f-111">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="5027f-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5027f-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="5027f-112">Prerequisites</span></span>

<span data-ttu-id="5027f-113">다음 소프트웨어를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-113">Install the following software:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5027f-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5027f-114">Visual Studio</span></span>](#tab/visual-studio)

* [<span data-ttu-id="5027f-115">.NET Core SDK 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="5027f-115">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* <span data-ttu-id="5027f-116">[Visual Studio 2017](https://www.visualstudio.com/downloads/) 버전 15.7 이상(**ASP.NET 및 웹 개발** 워크로드 포함)</span><span class="sxs-lookup"><span data-stu-id="5027f-116">[Visual Studio 2017](https://www.visualstudio.com/downloads/) version 15.7 or later with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="5027f-117">npm</span><span class="sxs-lookup"><span data-stu-id="5027f-117">npm</span></span>](https://www.npmjs.com/get-npm)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5027f-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5027f-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="5027f-119">.NET Core SDK 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="5027f-119">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="5027f-120">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5027f-120">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="5027f-121">Visual Studio Code용 C#</span><span class="sxs-lookup"><span data-stu-id="5027f-121">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* [<span data-ttu-id="5027f-122">npm</span><span class="sxs-lookup"><span data-stu-id="5027f-122">npm</span></span>](https://www.npmjs.com/get-npm)

-----

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a><span data-ttu-id="5027f-123">SignalR 클라이언트와 서버를 호스팅하는 ASP.NET Core 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5027f-123">Create an ASP.NET Core project that hosts SignalR client and server</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5027f-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5027f-124">Visual Studio</span></span>](#tab/visual-studio/)

1. <span data-ttu-id="5027f-125">**파일** > **새 프로젝트** 메뉴 옵션을 사용하고 **ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-125">Use the **File** > **New Project** menu option and choose **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="5027f-126">프로젝트의 이름을 *SignalRChat*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-126">Name the project *SignalRChat*.</span></span>

   ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-dialog.png)

2. <span data-ttu-id="5027f-128">Razor Pages를 사용하여 프로젝트를 생성하려면 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-128">Select **Web Application** to create a project using Razor Pages.</span></span> <span data-ttu-id="5027f-129">그런 다음, **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-129">Then select **OK**.</span></span> <span data-ttu-id="5027f-130">SignalR이 이전 버전의 .NET에서 실행되는 경우에도 프레임워크 선택기에서 **ASP.NET Core 2.1**을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-130">Be sure that **ASP.NET Core 2.1** is selected from the framework selector, though SignalR runs on older versions of .NET.</span></span>

   ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-choose-type.png)

<span data-ttu-id="5027f-132">Visual Studio에는 **ASP.NET Core 웹 응용 프로그램** 템플릿의 일부로 서버 라이브러리가 포함된 `Microsoft.AspNetCore.SignalR` 패키지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-132">Visual Studio includes the `Microsoft.AspNetCore.SignalR` package containing its server libraries as part of its **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="5027f-133">그러나 SignalR용 JavaScript 클라이언트 라이브러리는 *npm*을 사용하여 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-133">However, the JavaScript client library for SignalR must be installed using *npm*.</span></span>

3. <span data-ttu-id="5027f-134">**패키지 관리자 콘솔** 창의 프로젝트 루트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-134">Run the following commands in the **Package Manager Console** window, from the project root:</span></span>

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

4. <span data-ttu-id="5027f-135">프로젝트의 *lib* 폴더 안에 "signalr"라는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-135">Create a new folder named "signalr" inside the  *lib* folder in your project.</span></span> <span data-ttu-id="5027f-136">*signalr.js* 파일을 *node_modules\\@aspnet\signalr\dist\browser*에서 이 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-136">Copy the *signalr.js* file from *node_modules\\@aspnet\signalr\dist\browser* to this folder.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5027f-137">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5027f-137">Visual Studio Code</span></span>](#tab/visual-studio-code/)

1. <span data-ttu-id="5027f-138">**통합 터미널**에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-138">From the **Integrated Terminal**, run the following command:</span></span>

    ```console
    dotnet new webapp -o SignalRChat
    ```

    [!INCLUDE[](~/includes/webapp-alias-notice.md)]

2. <span data-ttu-id="5027f-139">*npm*을 사용하여 JavaScript 클라이언트 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-139">Install the JavaScript client library using *npm*.</span></span>

    ```console
    npm init -y
    npm install @aspnet/signalr
    ```

3. <span data-ttu-id="5027f-140">프로젝트의 *lib* 폴더 안에 "signalr"라는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-140">Create a new folder named "signalr" inside the  *lib* folder in your project.</span></span> <span data-ttu-id="5027f-141">*signalr.js* 파일을 *node_modules\\@aspnet\signalr\dist\browser*에서 이 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-141">Copy the *signalr.js* file from *node_modules\\@aspnet\signalr\dist\browser* to this folder.</span></span>

---

## <a name="create-the-signalr-hub"></a><span data-ttu-id="5027f-142">SignalR Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="5027f-142">Create the SignalR Hub</span></span>

<span data-ttu-id="5027f-143">허브는 클라이언트와 서버가 서로 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인 역할을 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-143">A hub is a class that serves as a high-level pipeline that allows the client and server to call methods on each other.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5027f-144">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5027f-144">Visual Studio</span></span>](#tab/visual-studio/)

1. <span data-ttu-id="5027f-145">**파일** > **새로 만들기** > **파일**을 선택하고 **Visual C# 클래스**를 선택하여 클래스를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-145">Add a class to the project by choosing **File** > **New** > **File** and selecting **Visual C# Class**.</span></span> <span data-ttu-id="5027f-146">`ChatHub` 클래스 및 *ChatHub.cs* 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-146">Name the class `ChatHub` and the file *ChatHub.cs*.</span></span>

2. <span data-ttu-id="5027f-147">`Microsoft.AspNetCore.SignalR.Hub`에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-147">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="5027f-148">`Hub` 클래스는 데이터 전송 및 수신뿐만 아니라, 연결 및 그룹 관리를 위한 속성 및 이벤트도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-148">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data.</span></span>

3. <span data-ttu-id="5027f-149">연결된 모든 채팅 클라이언트에 메시지를 보내는 `SendMessage` 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-149">Create the `SendMessage` method that sends a message to all connected chat clients.</span></span> <span data-ttu-id="5027f-150">SignalR은 비동기이기 때문에 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-150">Notice it returns a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task(v=vs.110).aspx), because SignalR is asynchronous.</span></span> <span data-ttu-id="5027f-151">비동기 코드는 더 잘 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-151">Asynchronous code scales better.</span></span>

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5027f-152">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5027f-152">Visual Studio Code</span></span>](#tab/visual-studio-code/)

1. <span data-ttu-id="5027f-153">Visual Studio Code에서 *SignalRChat* 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-153">Open the *SignalRChat* folder in Visual Studio Code.</span></span>

2. <span data-ttu-id="5027f-154">메뉴에서 **파일** > **새 파일**을 선택하여 프로젝트에 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-154">Add a class to the project by selecting **File** > **New File** from the menu.</span></span> <span data-ttu-id="5027f-155">`ChatHub` 클래스 및 *ChatHub.cs* 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-155">Name the class `ChatHub` and the file *ChatHub.cs*.</span></span>

3. <span data-ttu-id="5027f-156">`Microsoft.AspNetCore.SignalR.Hub`에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-156">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="5027f-157">`Hub` 클래스는 클라이언트에 대한 데이터 전송 및 수신뿐만 아니라, 연결 및 그룹 관리를 위한 속성 및 이벤트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-157">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data to clients.</span></span>

4. <span data-ttu-id="5027f-158">클래스에 `SendMessage` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-158">Add a `SendMessage` method to the class.</span></span> <span data-ttu-id="5027f-159">`SendMessage` 메서드는 연결된 모든 채팅 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-159">The `SendMessage` method sends a message to all connected chat clients.</span></span> <span data-ttu-id="5027f-160">SignalR은 비동기이기 때문에 [작업](/dotnet/api/system.threading.tasks.task)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-160">Notice it returns a [Task](/dotnet/api/system.threading.tasks.task), because SignalR is asynchronous.</span></span> <span data-ttu-id="5027f-161">비동기 코드는 더 잘 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-161">Asynchronous code scales better.</span></span>

   [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

-----

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="5027f-162">SignalR을 사용하도록 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="5027f-162">Configure the project to use SignalR</span></span>

<span data-ttu-id="5027f-163">SignalR 서버는 SignalR에 요청을 전달할 수 있도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-163">The SignalR server must be configured so that it knows to pass requests to SignalR.</span></span>

1. <span data-ttu-id="5027f-164">SignalR 프로젝트를 구성하려면 프로젝트의 `Startup.ConfigureServices` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-164">To configure a SignalR project, modify the project's `Startup.ConfigureServices` method.</span></span>

   <span data-ttu-id="5027f-165">`services.AddSignalR`을 통해 [종속성 주입](xref:fundamentals/dependency-injection) 시스템에 SignalR 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-165">`services.AddSignalR` makes the SignalR services available to the [dependency injection](xref:fundamentals/dependency-injection) system.</span></span>

1. <span data-ttu-id="5027f-166">`Configure` 메서드에서 `UseSignalR`을 사용하여 허브에 대한 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-166">Configure routes to your hubs with `UseSignalR` in the `Configure` method.</span></span> <span data-ttu-id="5027f-167">`app.UseSignalR`은 [미들웨어](xref:fundamentals/middleware/index) 파이프라인에 SignalR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-167">`app.UseSignalR` adds SignalR to the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

   [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=37,57-60)]

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="5027f-168">SignalR 클라이언트 코드 만들기</span><span class="sxs-lookup"><span data-stu-id="5027f-168">Create the SignalR client code</span></span>

1. <span data-ttu-id="5027f-169">*chat.js*라는 JavaScript 파일을 *wwwroot\js* 폴더에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-169">Add a JavaScript file, named *chat.js*, to the *wwwroot\js* folder.</span></span> <span data-ttu-id="5027f-170">파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-170">Add the following code to it:</span></span>

   [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

2. <span data-ttu-id="5027f-171">*Pages\Index.cshtml*의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-171">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

   [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

   <span data-ttu-id="5027f-172">앞의 HTML에는 이름과 메시지 필드 및 제출 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-172">The preceding HTML displays name and message fields, and a submit button.</span></span> <span data-ttu-id="5027f-173">맨 아래에 있는 스크립트 참조(SignalR 및 *chat.js*에 대한 참조)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-173">Notice the script references at the bottom: a reference to SignalR and *chat.js*.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="5027f-174">앱 실행</span><span class="sxs-lookup"><span data-stu-id="5027f-174">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="5027f-175">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5027f-175">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="5027f-176">**디버그** > **디버깅 없이 시작**을 선택하여 브라우저를 실행하고 웹 사이트를 로컬로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-176">Select **Debug** > **Start without debugging** to launch a browser and load the website locally.</span></span> <span data-ttu-id="5027f-177">주소 표시줄에서 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-177">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="5027f-178">다른 브라우저 인스턴스(모든 브라우저)를 열고 주소 표시줄에 URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-178">Open another browser instance (any browser) and paste the URL in the address bar.</span></span>

1. <span data-ttu-id="5027f-179">브라우저 중 하나를 선택하고 이름과 메시지를 입력한 후, **보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-179">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="5027f-180">이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-180">The name and message are displayed on both pages instantly.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="5027f-181">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5027f-181">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="5027f-182">**디버그**(F5) 키를 눌러 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-182">Press **Debug** (F5) to build and run the program.</span></span> <span data-ttu-id="5027f-183">프로그램을 실행하면 브라우저 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-183">Running the program opens a browser window.</span></span>

1. <span data-ttu-id="5027f-184">다른 브라우저 창을 열고 웹 사이트를 로컬로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-184">Open another browser window and load the website locally in it.</span></span>

1. <span data-ttu-id="5027f-185">브라우저 중 하나를 선택하고 이름과 메시지를 입력한 후, **보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-185">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="5027f-186">이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5027f-186">The name and message are displayed on both pages instantly.</span></span>

---

  ![솔루션](signalr/_static/signalr-get-started-finished.png)

## <a name="related-resources"></a><span data-ttu-id="5027f-188">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="5027f-188">Related resources</span></span>

[<span data-ttu-id="5027f-189">ASP.NET Core SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="5027f-189">Introduction to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)
