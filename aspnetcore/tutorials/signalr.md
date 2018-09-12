---
title: '자습서: ASP.NET Core에서 SignalR 시작'
author: tdykstra
description: 이 자습서에서는 ASP.NET Core용 SignalR을 사용하는 채팅 앱을 만듭니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/31/2018
uid: tutorials/signalr
ms.openlocfilehash: 6d96331a4630f766ca11edb056fd3e13b52b6ae4
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893167"
---
# <a name="tutorial-get-started-with-signalr-on-aspnet-core"></a><span data-ttu-id="edd21-103">자습서: ASP.NET Core에서 SignalR 시작</span><span class="sxs-lookup"><span data-stu-id="edd21-103">Tutorial: Get started with SignalR on ASP.NET Core</span></span>

<span data-ttu-id="edd21-104">이 자습서에서는 SignalR을 사용하여 실시간 앱을 빌드하는 방법에 대한 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-104">This tutorial teaches the basics of building a real-time app using SignalR.</span></span> <span data-ttu-id="edd21-105">여기에서는 다음과 같은 작업을 수행하는 방법에 대해 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="edd21-106">ASP.NET Core에서 SignalR을 사용하는 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-106">Create a web app that uses SignalR on ASP.NET Core.</span></span>
> * <span data-ttu-id="edd21-107">서버에서 SignalR 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-107">Create a SignalR hub on the server.</span></span>
> * <span data-ttu-id="edd21-108">JavaScript 클라이언트에서 SignalR 허브에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-108">Connect to the SignalR hub from JavaScript clients.</span></span>
> * <span data-ttu-id="edd21-109">허브를 사용하여 모든 클라이언트에서 연결된 모든 클라이언트에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-109">Use the hub to send messages from any client to all connected clients.</span></span>

<span data-ttu-id="edd21-110">작동하는 채팅 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-110">At the end, you'll have a working chat app:</span></span>

![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

<span data-ttu-id="edd21-112">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="edd21-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edd21-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="edd21-113">Prerequisites</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="edd21-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edd21-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="edd21-115">[Visual Studio 2017 버전 15.8 이상](https://www.visualstudio.com/downloads/)(**ASP.NET 및 웹 개발** 워크로드 포함)</span><span class="sxs-lookup"><span data-stu-id="edd21-115">[Visual Studio 2017 version 15.8 or later](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload</span></span>
* [<span data-ttu-id="edd21-116">.NET Core SDK 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="edd21-116">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="edd21-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="edd21-117">Visual Studio Code</span></span>](#tab/visual-studio-code)

* [<span data-ttu-id="edd21-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="edd21-118">Visual Studio Code</span></span>](https://code.visualstudio.com/download)
* [<span data-ttu-id="edd21-119">.NET Core SDK 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="edd21-119">.NET Core SDK 2.1 or later</span></span>](https://www.microsoft.com/net/download/all)
* [<span data-ttu-id="edd21-120">Visual Studio Code용 C#</span><span class="sxs-lookup"><span data-stu-id="edd21-120">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="edd21-121">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="edd21-121">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* [<span data-ttu-id="edd21-122">Mac용 Visual Studio 버전 7.5.4 이상</span><span class="sxs-lookup"><span data-stu-id="edd21-122">Visual Studio for Mac version 7.5.4 or later</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="edd21-123">[.NET Core SDK 2.1 이상](https://www.microsoft.com/net/download/all)(Visual Studio 설치에 포함됨)</span><span class="sxs-lookup"><span data-stu-id="edd21-123">[.NET Core SDK 2.1 or later](https://www.microsoft.com/net/download/all) (included in the Visual Studio install)</span></span>

---

## <a name="create-the-project"></a><span data-ttu-id="edd21-124">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-124">Create the project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="edd21-125">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edd21-125">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="edd21-126">메뉴에서 **파일 > 새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-126">From the menu, select **File > New Project**.</span></span>

* <span data-ttu-id="edd21-127">**새 프로젝트** 대화 상자에서 **설치됨 > Visual C# > 웹 > ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-127">In the **New Project** dialog, select **Installed > Visual C# > Web > ASP.NET Core Web Application**.</span></span> <span data-ttu-id="edd21-128">프로젝트의 이름을 *SignalRChat*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-128">Name the project *SignalRChat*.</span></span>

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-dialog.png)

* <span data-ttu-id="edd21-130">Razor Pages를 사용하는 프로젝트를 생성하려면 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-130">Select **Web Application** to create a project that uses Razor Pages.</span></span>

* <span data-ttu-id="edd21-131">**.NET Core**의 대상 프레임워크를 선택하고, **ASP.NET Core 2.1**을 선택하고, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-131">Select a target framework of **.NET Core**, select **ASP.NET Core 2.1**, and click **OK**.</span></span>

  ![Visual Studio의 새 프로젝트 대화 상자](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="edd21-133">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="edd21-133">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="edd21-134">새 프로젝트에 사용할 수 있는 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-134">Open a folder that you can use for a new project.</span></span>

* <span data-ttu-id="edd21-135">**통합 터미널**에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-135">In the **Integrated Terminal**, run the following command:</span></span>

   ```console
   dotnet new webapp -o SignalRChat
   ```

   [!INCLUDE[](~/includes/webapp-alias-notice.md)]

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="edd21-136">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="edd21-136">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="edd21-137">메뉴에서 **파일 > 새 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-137">From the menu, select **File > New Solution**.</span></span>

* <span data-ttu-id="edd21-138">**.NET Core > 앱 > ASP.NET Core 웹앱**(**ASP.NET Core 웹앱(MVC) 선택 안 함**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-138">Select **.NET Core > App > ASP.NET Core Web App** (Don't select **ASP.NET Core Web App (MVC)**).</span></span>

* <span data-ttu-id="edd21-139">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-139">Select **Next**.</span></span>

* <span data-ttu-id="edd21-140">프로젝트 이름을 *SignalRChat*으로 지정한 다음, **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-140">Name the project *SignalRChat*, and then select **Create**.</span></span>

---

## <a name="add-the-signalr-client-library"></a><span data-ttu-id="edd21-141">SignalR 클라이언트 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="edd21-141">Add the SignalR client library</span></span>

<span data-ttu-id="edd21-142">SignalR 서버 라이브러리는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-142">The SignalR server library is included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="edd21-143">JavaScript 클라이언트 라이브러리는 프로젝트에 자동으로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-143">The JavaScript client library isn't automatically included in the project.</span></span> <span data-ttu-id="edd21-144">이 자습서에서는 [라이브러리 관리자(LibMan)](xref:client-side/libman/index)를 사용하여 *unpkg*에서 클라이언트 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-144">For this tutorial, you use [Library Manager (LibMan)](xref:client-side/libman/index) to get the client library from *unpkg*.</span></span> <span data-ttu-id="edd21-145">[unpkg](https://unpkg.com/#/)는 [npm, Node.js 패키지 관리자](https://www.npmjs.com/get-npm)에서 찾은 내용을 전달할 수 있는 [콘텐츠 배달 네트워크](https://wikipedia.org/wiki/Content_delivery_network)입니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-145">[unpkg](https://unpkg.com/#/) is a [content delivery network](https://wikipedia.org/wiki/Content_delivery_network) that can deliver anything found in [npm, the Node.js package manager](https://www.npmjs.com/get-npm).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="edd21-146">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edd21-146">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="edd21-147">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Add** > **Client-Side Library**(클라이언트 쪽 라이브러리 추가)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-147">In **Solution Explorer**, right-click the project, and select **Add** > **Client-Side Library**.</span></span>

* <span data-ttu-id="edd21-148">**Add Client-Side Library**(클라이언트 쪽 라이브러리 추가) 대화 상자에서 **공급자**에 대해 **unpkg**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-148">In the **Add Client-Side Library** dialog, for **Provider** select **unpkg**.</span></span> 

* <span data-ttu-id="edd21-149">**라이브러리**에 대해 _@aspnet/signalr@1_을 입력하고 미리 보기가 아닌 최신 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-149">For **Library**, enter _@aspnet/signalr@1_, and select the latest version that isn't preview.</span></span>

  ![Add Client-Side Library(클라이언트 쪽 라이브러리 추가) 대화 상자 - 라이브러리 선택](signalr/_static/libman1.png)

* <span data-ttu-id="edd21-151">**Choose specific files**(특정 파일 선택)를 선택하고 *dist/browser* 폴더를 확장한 후 *signalr.js* 및 *signalr.min.js*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-151">Select **Choose specific files**, expand the *dist/browser* folder, and select *signalr.js* and *signalr.min.js*.</span></span>

* <span data-ttu-id="edd21-152">**대상 위치**를 *wwwroot/lib/signalr/* 로 설정하고 **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-152">Set **Target Location** to *wwwroot/lib/signalr/*, and select **Install**.</span></span>

  ![Add Client-Side Library(클라이언트 쪽 라이브러리 추가) 대화 상자 - 파일 및 대상 선택](signalr/_static/libman2.png)

  <span data-ttu-id="edd21-154">[LibMan](xref:client-side/libman/index)은 *wwwroot/lib/signalr* 폴더를 생성하고 선택한 파일을 여기에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-154">[LibMan](xref:client-side/libman/index) creates a *wwwroot/lib/signalr* folder and copies the selected files to it.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="edd21-155">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="edd21-155">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="edd21-156">**통합 터미널**에서 다음 명령을 실행하여 LibMan을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-156">In the **Integrated Terminal**, run the following command to install LibMan.</span></span>

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* <span data-ttu-id="edd21-157">프로젝트 폴더로 이동합니다(*SignalRChat.csproj* 파일을 포함하는 폴더).</span><span class="sxs-lookup"><span data-stu-id="edd21-157">Navigate to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

* <span data-ttu-id="edd21-158">다음 명령을 실행하고 LibMan을 사용하여 SignalR 클라이언트 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-158">Run the following command to get the SignalR client library by using LibMan.</span></span> <span data-ttu-id="edd21-159">출력이 표시되기 전에 잠시 기다려야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-159">You might have to wait a few seconds before seeing output.</span></span>

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot\lib\signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  <span data-ttu-id="edd21-160">매개 변수는 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-160">The parameters specify the following options:</span></span>
  * <span data-ttu-id="edd21-161">unpkg 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-161">Use the unpkg provider.</span></span>
  * <span data-ttu-id="edd21-162">파일을 *wwwroot/lib/signalr* 대상으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-162">Copy files to the *wwwroot/lib/signalr* destination.</span></span>
  * <span data-ttu-id="edd21-163">지정된 파일만 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-163">Copy only the specified files.</span></span>

  <span data-ttu-id="edd21-164">출력은 다음 예와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-164">The output looks like the following example:</span></span>

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot\lib\signalr"
  ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="edd21-165">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="edd21-165">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="edd21-166">**터미널**에서 다음 명령을 실행하여 LibMan을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-166">In the **Terminal**, run the following command to install LibMan.</span></span>

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* <span data-ttu-id="edd21-167">프로젝트 폴더로 이동합니다(*SignalRChat.csproj* 파일을 포함하는 폴더).</span><span class="sxs-lookup"><span data-stu-id="edd21-167">Navigate to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

* <span data-ttu-id="edd21-168">다음 명령을 실행하고 LibMan을 사용하여 SignalR 클라이언트 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-168">Run the following command to get the SignalR client library by using LibMan.</span></span>

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot\lib\signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  <span data-ttu-id="edd21-169">매개 변수는 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-169">The parameters specify the following options:</span></span>
  * <span data-ttu-id="edd21-170">unpkg 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-170">Use the unpkg provider.</span></span>
  * <span data-ttu-id="edd21-171">파일을 *wwwroot/lib/signalr* 대상으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-171">Copy files to the *wwwroot/lib/signalr* destination.</span></span>
  * <span data-ttu-id="edd21-172">지정된 파일만 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-172">Copy only the specified files.</span></span>

  <span data-ttu-id="edd21-173">출력은 다음 예와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-173">The output looks like the following example:</span></span>

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot\lib\signalr"
  ```

---

## <a name="create-the-signalr-hub"></a><span data-ttu-id="edd21-174">SignalR 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="edd21-174">Create the SignalR hub</span></span>

<span data-ttu-id="edd21-175">[허브](xref:signalr/hubs)는 클라이언트-서버 통신을 처리하는 높은 수준의 파이프라인으로 제공되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-175">A [hub](xref:signalr/hubs) is a class that serves as a high-level pipeline that handles client-server communication.</span></span>

* <span data-ttu-id="edd21-176">SignalRChat 프로젝트 폴더에서 *Hubs* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-176">In the SignalRChat project folder, create a *Hubs* folder.</span></span>

* <span data-ttu-id="edd21-177">*Hubs* 폴더에 다음 코드를 사용하여 *ChatHub.cs* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-177">In the *Hubs* folder, create a *ChatHub.cs* file with the following code:</span></span>

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  <span data-ttu-id="edd21-178">`ChatHub` 클래스는 SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-178">The `ChatHub` class inherits from the SignalR [Hub](/dotnet/api/microsoft.aspnetcore.signalr.hub) class.</span></span> <span data-ttu-id="edd21-179">`Hub` 클래스는 연결, 그룹 및 메시징을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-179">The `Hub` class manages connections, groups, and messaging.</span></span>

  <span data-ttu-id="edd21-180">연결된 모든 클라이언트에서 `SendMessage` 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-180">The `SendMessage` method can be called by any connected client.</span></span> <span data-ttu-id="edd21-181">모든 클라이언트에 수신된 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-181">It sends the received message to all clients.</span></span> <span data-ttu-id="edd21-182">SignalR 코드는 최대 확장성을 제공하도록 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-182">SignalR code is asynchronous to provide maximum scalability.</span></span>

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="edd21-183">SignalR을 사용하도록 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="edd21-183">Configure the project to use SignalR</span></span>

<span data-ttu-id="edd21-184">SignalR 서버는 SignalR에 SignalR 요청을 전달하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-184">The SignalR server must be configured to pass SignalR requests to SignalR.</span></span>

* <span data-ttu-id="edd21-185">다음 강조 표시된 코드를 *Startup.cs* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-185">Add the following highlighted code to the *Startup.cs* file.</span></span>

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  <span data-ttu-id="edd21-186">이러한 변경 사항은 [종속성 주입](xref:fundamentals/dependency-injection) 시스템 및 [미들웨어](xref:fundamentals/middleware/index) 파이프라인에 SignalR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-186">These changes add SignalR to the [dependency injection](xref:fundamentals/dependency-injection) system and the [middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="edd21-187">SignalR 클라이언트 코드 만들기</span><span class="sxs-lookup"><span data-stu-id="edd21-187">Create the SignalR client code</span></span>

* <span data-ttu-id="edd21-188">*Pages\Index.cshtml*의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-188">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  <span data-ttu-id="edd21-189">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="edd21-189">The preceding code:</span></span>

  * <span data-ttu-id="edd21-190">이름 및 메시지 텍스트에 대한 텍스트 상자 및 전송 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-190">Creates text boxes for name and message text, and a submit button.</span></span>
  * <span data-ttu-id="edd21-191">SignalR 허브에서 받은 메시지를 표시하기 위해 `id="messagesList"`를 사용하여 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-191">Creates a list with `id="messagesList"` for displaying messages that are received from the SignalR hub.</span></span>
  * <span data-ttu-id="edd21-192">SignalR에 대한 스크립트 참조 및 다음 단계에서 만드는 *chat.js* 응용 프로그램 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-192">Includes script references to SignalR and the *chat.js* application code that you create in the next step.</span></span>

* <span data-ttu-id="edd21-193">*wwwroot/js* 폴더에서 다음 코드를 사용하여 *chat.js* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-193">In the *wwwroot/js* folder, create a *chat.js* file with the following code:</span></span>

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  <span data-ttu-id="edd21-194">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="edd21-194">The preceding code:</span></span>

  * <span data-ttu-id="edd21-195">연결을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-195">Creates and starts a connection.</span></span>
  * <span data-ttu-id="edd21-196">허브에 메시지를 전송하는 처리기를 전송 단추에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-196">Adds to the submit button a handler that sends messages to the hub.</span></span>
  * <span data-ttu-id="edd21-197">허브에서 메시지를 수신하고 목록에 추가하는 처리기를 연결 개체에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-197">Adds to the connection object a handler that receives messages from the hub and adds them to the list.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="edd21-198">앱 실행</span><span class="sxs-lookup"><span data-stu-id="edd21-198">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="edd21-199">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edd21-199">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="edd21-200">**CTRL+F5** 키를 눌러 디버깅 없이 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-200">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="edd21-201">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="edd21-201">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="edd21-202">**CTRL+F5** 키를 눌러 디버깅 없이 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-202">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="edd21-203">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="edd21-203">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="edd21-204">메뉴에서 **실행 > 디버깅하지 않고 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-204">From the menu, select **Run > Start Without Debugging**.</span></span>

---

* <span data-ttu-id="edd21-205">주소 표시줄에서 URL을 복사하고, 다른 브라우저 인스턴스 또는 탭을 열고, 주소 표시줄에 URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-205">Copy the URL from the address bar, open another browser instance or tab, and paste the URL in the address bar.</span></span>

* <span data-ttu-id="edd21-206">브라우저 중 하나를 선택하고, 이름 및 메시지를 입력하고, **보내기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-206">Choose either browser, enter a name and message, and select the **Send** button.</span></span>

  <span data-ttu-id="edd21-207">이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-207">The name and message are displayed on both pages instantly.</span></span>

  ![SignalR 샘플 앱](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> <span data-ttu-id="edd21-209">앱이 작동하지 않는 경우 브라우저 개발자 도구(F12)를 열고 콘솔로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-209">If the app doesn't work, open your browser developer tools (F12) and go to the console.</span></span> <span data-ttu-id="edd21-210">HTML 및 JavaScript 코드와 관련된 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-210">You might see errors related to your HTML and JavaScript code.</span></span> <span data-ttu-id="edd21-211">예를 들어 지정되지 않은 다른 폴더에 *signalr.js*를 넣었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-211">For example, suppose you put *signalr.js* in a different folder than directed.</span></span> <span data-ttu-id="edd21-212">이 경우 해당 파일에 대한 참조는 작동하지 않으며 콘솔에 404 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-212">In that case the reference to that file won't work and you'll see a 404 error in the console.</span></span>
> <span data-ttu-id="edd21-213">![signalr.js 찾을 수 없음 오류](signalr/_static/f12-console.png)</span><span class="sxs-lookup"><span data-stu-id="edd21-213">![signalr.js not found error](signalr/_static/f12-console.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="edd21-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="edd21-214">Next steps</span></span>

<span data-ttu-id="edd21-215">클라이언트를 다른 도메인의 SignalR 앱에 연결하려는 경우 CORS(원본 간 리소스 공유)를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd21-215">If you want clients to connect to a SignalR app from different domains, you have to enable Cross-Origin Resource Sharing (CORS).</span></span> <span data-ttu-id="edd21-216">자세한 내용은 [원본 간 리소스 공유](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edd21-216">For more information, see [Cross-origin resource sharing](xref:signalr/security?view=aspnetcore-2.1#cross-origin-resource-sharing).</span></span>

<span data-ttu-id="edd21-217">SignalR, 허브 및 JavaScript 클라이언트에 대해 자세히 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edd21-217">To learn more about SignalR, hubs, and JavaScript clients, see these resources:</span></span>

* [<span data-ttu-id="edd21-218">ASP.NET Core용 SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="edd21-218">Introduction to SignalR for ASP.NET Core</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="edd21-219">ASP.NET Core용 SignalR에서 허브 사용</span><span class="sxs-lookup"><span data-stu-id="edd21-219">Use hubs in SignalR for ASP.NET Core</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="edd21-220">ASP.NET Core SignalR JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="edd21-220">ASP.NET Core SignalR JavaScript client</span></span>](xref:signalr/javascript-client)
