---
title: '자습서: ASP.NET Core에서 SignalR 시작'
author: tdykstra
description: 이 자습서에서는 ASP.NET Core용 SignalR을 사용하는 채팅 앱을 만듭니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/20/2018
uid: tutorials/signalr
ms.openlocfilehash: a2573e2817a2d8921954264ca17bc3a7e2a010a8
ms.sourcegitcommit: 847cc1de5526ff42a7303491e6336c2dbdb45de4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43055834"
---
# <a name="tutorial-get-started-with-signalr-on-aspnet-core"></a><span data-ttu-id="98d57-103">자습서: ASP.NET Core에서 SignalR 시작</span><span class="sxs-lookup"><span data-stu-id="98d57-103">Tutorial: Get started with SignalR on ASP.NET Core</span></span>

<span data-ttu-id="98d57-104">이 자습서에서는 SignalR을 사용하여 실시간 앱을 빌드하는 방법에 대한 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-104">This tutorial teaches the basics of building a real-time app using SignalR.</span></span> <span data-ttu-id="98d57-105">여기에서는 다음과 같은 작업을 수행하는 방법에 대해 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98d57-106">ASP.NET Core에서 SignalR을 사용하는 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-106">Create a web app that uses SignalR on ASP.NET Core.</span></span>
> * <span data-ttu-id="98d57-107">서버에서 SignalR 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-107">Create a SignalR hub on the server.</span></span>
> * <span data-ttu-id="98d57-108">JavaScript 클라이언트에서 SignalR 허브에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-108">Connect to the SignalR hub from JavaScript clients.</span></span>
> * <span data-ttu-id="98d57-109">허브를 사용하여 모든 클라이언트에서 연결된 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-109">Use the hub to send messages from any client to all connected clients.</span></span>

<span data-ttu-id="98d57-110">작동하는 채팅 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-110">At the end, you'll have a working chat app:</span></span>

![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

<span data-ttu-id="98d57-112">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="98d57-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98d57-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="98d57-113">Prerequisites</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="98d57-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98d57-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="98d57-115">[Visual Studio 2017 버전 15.7.3 이상](https://www.visualstudio.com/downloads/)(**ASP.NET 및 웹 개발** 워크로드 포함)</span><span class="sxs-lookup"><span data-stu-id="98d57-115">[Visual Studio 2017 version 15.7.3 or later](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="98d57-116">.NET Core SDK 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="98d57-116">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* <span data-ttu-id="98d57-117">[npm](https://www.npmjs.com/get-npm)(SignalR JavaScript 클라이언트 라이브러리에 사용되는 Node.js용 패키지 관리자)</span><span class="sxs-lookup"><span data-stu-id="98d57-117">[npm](https://www.npmjs.com/get-npm) (Package manager for Node.js, used for the SignalR JavaScript client library.)</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="98d57-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="98d57-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="98d57-119">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="98d57-119">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="98d57-120">.NET Core SDK 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="98d57-120">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="98d57-121">Visual Studio Code용 C#</span><span class="sxs-lookup"><span data-stu-id="98d57-121">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
* <span data-ttu-id="98d57-122">[npm](https://www.npmjs.com/get-npm)(SignalR JavaScript 클라이언트 라이브러리에 사용되는 Node.js용 패키지 관리자)</span><span class="sxs-lookup"><span data-stu-id="98d57-122">[npm](https://www.npmjs.com/get-npm) (Package manager for Node.js, used for the SignalR JavaScript client library.)</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="98d57-123">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="98d57-123">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* [<span data-ttu-id="98d57-124">Mac용 Visual Studio 버전 7.5.4 이상</span><span class="sxs-lookup"><span data-stu-id="98d57-124">Visual Studio for Mac version 7.5.4 or later</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="98d57-125">[.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)(Visual Studio 설치에 포함됨)</span><span class="sxs-lookup"><span data-stu-id="98d57-125">[.NET Core SDK 2.1 or later](https://www.microsoft.com/net/download/all) (included in the Visual Studio install)</span></span>
* <span data-ttu-id="98d57-126">[npm](https://www.npmjs.com/get-npm)(SignalR JavaScript 클라이언트 라이브러리에 사용되는 Node.js용 패키지 관리자)</span><span class="sxs-lookup"><span data-stu-id="98d57-126">[npm](https://www.npmjs.com/get-npm) (Package manager for Node.js, used for the SignalR JavaScript client library.)</span></span>

---

## <a name="create-the-project"></a><span data-ttu-id="98d57-127">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-127">Create the project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="98d57-128">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98d57-128">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="98d57-129">메뉴에서 **파일 > 새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-129">From the menu, select **File > New Project**.</span></span>

* <span data-ttu-id="98d57-130">**새 프로젝트** 대화 상자에서 **설치됨 > Visual C# > 웹 > ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-130">In the **New Project** dialog, select **Installed > Visual C# > Web > ASP.NET Core Web Application**.</span></span> <span data-ttu-id="98d57-131">프로젝트의 이름을 *SignalRChat*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-131">Name the project *SignalRChat*.</span></span>

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-dialog.png)

* <span data-ttu-id="98d57-133">Razor Pages를 사용하는 프로젝트를 생성하려면 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-133">Select **Web Application** to create a project that uses Razor Pages.</span></span>

* <span data-ttu-id="98d57-134">**.NET Core**의 대상 프레임워크를 선택하고, **ASP.NET Core 2.1**을 선택하고, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-134">Select a target framework of **.NET Core**, select **ASP.NET Core 2.1**, and click **OK**.</span></span>

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="98d57-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="98d57-136">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="98d57-137">새 프로젝트에 사용할 수 있는 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-137">Open a folder that you can use for a new project.</span></span>

* <span data-ttu-id="98d57-138">**통합 터미널**에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-138">In the **Integrated Terminal**, run the following command:</span></span>

   ```console
   dotnet new webapp -o SignalRChat
   ```

   [!INCLUDE[](~/includes/webapp-alias-notice.md)]

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="98d57-139">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="98d57-139">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="98d57-140">메뉴에서 **파일 > 새 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-140">From the menu, select **File > New Solution**.</span></span>

* <span data-ttu-id="98d57-141">**.NET Core > 앱 > ASP.NET Core 웹앱**(**ASP.NET Core 웹앱(MVC) 선택 안 함**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-141">Select **.NET Core > App > ASP.NET Core Web App** (Don't select **ASP.NET Core Web App (MVC)**).</span></span>

* <span data-ttu-id="98d57-142">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-142">Select **Next**.</span></span>

* <span data-ttu-id="98d57-143">프로젝트 이름을 *SignalRChat*으로 지정한 다음, **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-143">Name the project *SignalRChat*, and then select **Create**.</span></span>

---

## <a name="add-the-signalr-client-library"></a><span data-ttu-id="98d57-144">SignalR 클라이언트 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="98d57-144">Add the SignalR client library</span></span>

<span data-ttu-id="98d57-145">SignalR 서버 라이브러리는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-145">The SignalR server library is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="98d57-146">하지만 [npm, Node.js 패키지 관리자](https://www.npmjs.com/get-npm)에서 JavaScript 클라이언트 라이브러리를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-146">But you have to get the JavaScript client library from [npm, the Node.js package manager](https://www.npmjs.com/get-npm).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="98d57-147">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98d57-147">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="98d57-148">**패키지 관리자 콘솔**(PMC)에서 프로젝트 폴더로 변경합니다(*SignalRChat.csproj* 파일을 포함하는 폴더).</span><span class="sxs-lookup"><span data-stu-id="98d57-148">In **Package Manager Console** (PMC), change to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

  ```console
  cd SignalRChat
  ```

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="98d57-149">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="98d57-149">Visual Studio Code</span></span>](#tab/visual-studio-code/)

2. <span data-ttu-id="98d57-150">새 프로젝트 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-150">Change to the new project folder.</span></span>

  ```console
  cd SignalRChat
  ``` 

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="98d57-151">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="98d57-151">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="98d57-152">**터미널**에서 프로젝트 폴더로 이동합니다(*SignalRChat.csproj* 파일을 포함하는 폴더).</span><span class="sxs-lookup"><span data-stu-id="98d57-152">In the **Terminal**, navigate to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

---

* <span data-ttu-id="98d57-153">npm 이니셜라이저를 실행하여 *package.json* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-153">Run the npm initializer to create a *package.json* file:</span></span>

  ```console
  npm init -y
  ```

  <span data-ttu-id="98d57-154">명령은 다음 예제와 유사한 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-154">The command creates output similar to the following example:</span></span>

  ```console
  Wrote to C:\tmp\SignalRChat\package.json:
  {
    "name": "SignalRChat",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC"0
  }
  ```

* <span data-ttu-id="98d57-155">클라이언트 라이브러리 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-155">Install the client library package:</span></span>

  ```console
  npm install @aspnet/signalr
  ```

  <span data-ttu-id="98d57-156">명령은 다음 예제와 유사한 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-156">The command creates output similar to the following example:</span></span>

  ```
  npm notice created a lockfile as package-lock.json. You should commit this file.
  npm WARN signalrchat@1.0.0 No description
  npm WARN signalrchat@1.0.0 No repository field.

  + @aspnet/signalr@1.0.2
  added 1 package in 0.98s
  ```

<span data-ttu-id="98d57-157">`npm install` 명령은 *node_modules* 아래의 하위 폴더에 JavaScript 클라이언트 라이브러리를 다운로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-157">The `npm install` command downloaded the JavaScript client library to a subfolder under *node_modules*.</span></span> <span data-ttu-id="98d57-158">여기에서 채팅 앱 웹 페이지에서 참조할 수 있는 *wwwroot* 아래의 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-158">Copy it from there to a folder under *wwwroot* that you can reference from the chat app web page.</span></span>

* <span data-ttu-id="98d57-159">*wwwroot/lib*에 *signalr* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-159">Create a *signalr* folder in *wwwroot/lib*.</span></span>

* <span data-ttu-id="98d57-160">*node_modules/@aspnet/signalr/dist/browser*에서 새 *wwwroot/lib/signalr* 폴더로 *signalr.js* 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-160">Copy the *signalr.js* file from *node_modules/@aspnet/signalr/dist/browser* to the new *wwwroot/lib/signalr* folder.</span></span>

## <a name="create-the-signalr-hub"></a><span data-ttu-id="98d57-161">SignalR 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="98d57-161">Create the SignalR hub</span></span>

<span data-ttu-id="98d57-162">[허브](xref:signalr/hubs)는 클라이언트-서버 통신을 처리하는 높은 수준의 파이프라인으로 제공되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-162">A [hub](xref:signalr/hubs) is a class that serves as a high-level pipeline that handles client-server communication.</span></span>

* <span data-ttu-id="98d57-163">SignalRChat 프로젝트 폴더에서 *Hubs* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-163">In the SignalRChat project folder, create a *Hubs* folder.</span></span>

* <span data-ttu-id="98d57-164">*Hubs* 폴더에 다음 코드를 사용하여 *ChatHub.cs* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-164">In the *Hubs* folder, create a *ChatHub.cs* file with the following code:</span></span>

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  <span data-ttu-id="98d57-165">`ChatHub` 클래스는 SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-165">The `ChatHub` class inherits from the SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) class.</span></span> <span data-ttu-id="98d57-166">`Hub` 클래스는 연결, 그룹 및 메시징을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-166">The `Hub` class manages connections, groups, and messaging.</span></span>

  <span data-ttu-id="98d57-167">연결된 모든 클라이언트에서 `SendMessage` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-167">The `SendMessage` method can be called by any connected client.</span></span> <span data-ttu-id="98d57-168">모든 클라이언트에 수신된 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-168">It sends the received message to all clients.</span></span> <span data-ttu-id="98d57-169">SignalR 코드는 최대 확장성을 제공하도록 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-169">SignalR code is asynchronous to provide maximum scalability.</span></span>

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="98d57-170">SignalR을 사용하도록 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="98d57-170">Configure the project to use SignalR</span></span>

<span data-ttu-id="98d57-171">SignalR 서버는 SignalR에 SignalR 요청을 전달하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-171">The SignalR server must be configured to pass SignalR requests to SignalR.</span></span>

* <span data-ttu-id="98d57-172">다음 강조 표시된 코드를 *Startup.cs* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-172">Add the following highlighted code to the *Startup.cs* file.</span></span>

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  <span data-ttu-id="98d57-173">이러한 변경 사항은 [종속성 주입](xref:fundamentals/dependency-injection) 시스템 및 [미들웨어](xref:fundamentals/middleware/index) 파이프라인에 SignalR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-173">These changes add SignalR to the [dependency injection](xref:fundamentals/dependency-injection) system and the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="98d57-174">SignalR 클라이언트 코드 만들기</span><span class="sxs-lookup"><span data-stu-id="98d57-174">Create the SignalR client code</span></span>

* <span data-ttu-id="98d57-175">*Pages\Index.cshtml*의 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-175">Replace the content in *Pages\Index.cshtml* with the following:</span></span>

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  <span data-ttu-id="98d57-176">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="98d57-176">The preceding code:</span></span>

  * <span data-ttu-id="98d57-177">이름 및 메시지 텍스트에 대한 텍스트 상자 및 전송 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-177">Creates text boxes for name and message text, and a submit button.</span></span>
  * <span data-ttu-id="98d57-178">SignalR 허브에서 받은 메시지를 표시하기 위해 `id="messagesList"`를 사용하여 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-178">Creates a list with `id="messagesList"` for displaying messages that are received from the SignalR hub.</span></span>
  * <span data-ttu-id="98d57-179">SignalR에 대한 스크립트 참조 및 다음 단계에서 만드는 *chat.js* 응용 프로그램 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-179">Includes script references to SignalR and the *chat.js* application code that you create in the next step.</span></span>

* <span data-ttu-id="98d57-180">*wwwroot/js* 폴더에서 다음 코드를 사용하여 *chat.js* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-180">In the *wwwroot/js* folder, create a *chat.js* file with the following code:</span></span>

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  <span data-ttu-id="98d57-181">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="98d57-181">The preceding code:</span></span>

  * <span data-ttu-id="98d57-182">연결을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-182">Creates and starts a connection.</span></span>
  * <span data-ttu-id="98d57-183">허브에 메시지를 전송하는 처리기를 전송 단추에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-183">Adds to the submit button a handler that sends messages to the hub.</span></span>
  * <span data-ttu-id="98d57-184">허브에서 메시지를 수신하고 목록에 추가하는 처리기를 연결 개체에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-184">Adds to the connection object a handler that receives messages from the hub and adds them to the list.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="98d57-185">앱 실행</span><span class="sxs-lookup"><span data-stu-id="98d57-185">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="98d57-186">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98d57-186">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="98d57-187">**CTRL+F5** 키를 눌러 디버깅 없이 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-187">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="98d57-188">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="98d57-188">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="98d57-189">**CTRL+F5** 키를 눌러 디버깅 없이 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-189">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="98d57-190">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="98d57-190">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="98d57-191">메뉴에서 **실행 > 디버깅하지 않고 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-191">From the menu, select **Run > Start Without Debugging**.</span></span>

---

* <span data-ttu-id="98d57-192">주소 표시줄에서 URL을 복사하고, 다른 브라우저 인스턴스 또는 탭을 열고, 주소 표시줄에 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-192">Copy the URL from the address bar, open another browser instance or tab, and paste the URL in the address bar.</span></span>

* <span data-ttu-id="98d57-193">브라우저 중 하나를 선택하고, 이름 및 메시지를 입력하고, **보내기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-193">Choose either browser, enter a name and message, and select the **Send** button.</span></span>

  <span data-ttu-id="98d57-194">이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-194">The name and message are displayed on both pages instantly.</span></span>

  ![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> <span data-ttu-id="98d57-196">앱이 작동하지 않는 경우 브라우저 개발자 도구(F12)를 열고 콘솔로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-196">If the app doesn't work, open your browser developer tools (F12) and go to the console.</span></span> <span data-ttu-id="98d57-197">HTML 및 JavaScript 코드와 관련된 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-197">You might see errors related to your HTML and JavaScript code.</span></span> <span data-ttu-id="98d57-198">예를 들어 지정되지 않은 다른 폴더에 *signalr.js*를 넣었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-198">For example, suppose you put *signalr.js* in a different folder than directed.</span></span> <span data-ttu-id="98d57-199">이 경우 해당 파일에 대한 참조는 작동하지 않으며 콘솔에 404 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-199">In that case the reference to that file won't work and you'll see a 404 error in the console.</span></span>
> <span data-ttu-id="98d57-200">![signalr.js 찾을 수 없음 오류](signalr/_static/f12-console.png)</span><span class="sxs-lookup"><span data-stu-id="98d57-200">![signalr.js not found error](signalr/_static/f12-console.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="98d57-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98d57-201">Next steps</span></span>

<span data-ttu-id="98d57-202">클라이언트를 다른 도메인의 SignalR 앱에 연결하려는 경우 CORS(원본 간 리소스 공유)를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98d57-202">If you want clients to connect to a SignalR app from different domains, you have to enable Cross-Origin Resource Sharing (CORS).</span></span> <span data-ttu-id="98d57-203">자세한 내용은 [원본 간 리소스 공유](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98d57-203">For more information, see [Cross-origin resource sharing](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing).</span></span>

<span data-ttu-id="98d57-204">SignalR, 허브 및 JavaScript 클라이언트에 대해 자세히 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98d57-204">To learn more about SignalR, hubs, and JavaScript clients, see these resources:</span></span>

* [<span data-ttu-id="98d57-205">ASP.NET Core용 SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="98d57-205">Introduction to SignalR for ASP.NET Core</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="98d57-206">ASP.NET Core용 SignalR에서 허브 사용</span><span class="sxs-lookup"><span data-stu-id="98d57-206">Use hubs in SignalR for ASP.NET Core</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="98d57-207">ASP.NET Core SignalR JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="98d57-207">ASP.NET Core SignalR JavaScript client</span></span>](xref:signalr/javascript-client)
