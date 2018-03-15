---
title: "SignalR에서 ASP.NET Core 시작"
author: rachelappel
description: "ASP.NET Core 용 SignalR을 사용 하 여 실시간 앱 빌드 기본 사항에 알아봅니다."
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/06/2018
ms.prod: aspnet-core
ms.technology: dotnet-signalr
ms.topic: tutorial
uid: signalr/get-started-signalr-core
ms.openlocfilehash: 79af59fc8c2ada71d764ada95a431e10f4f00f27
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="tutorial-get-started-with-signalr-for-aspnet-core"></a><span data-ttu-id="22c09-103">ASP.NET Core 용 SignalR 시작 자습서:</span><span class="sxs-lookup"><span data-stu-id="22c09-103">Tutorial: Get started with SignalR for ASP.NET Core</span></span>

<span data-ttu-id="22c09-104">작성자: [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="22c09-104">By [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="22c09-105">이 자습서의 ASP.NET Core 용 SignalR을 사용 하 여 실시간 앱 빌드 기본 사항에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-105">This tutorial teaches the basics of building a real-time app using SignalR for ASP.NET Core.</span></span>

   ![솔루션](get-started-signalr-core/_static/signalr-get-started-finished.png)

<span data-ttu-id="22c09-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="22c09-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/get-started-signalr-core/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="22c09-108">이 자습서에서는 다음 SignalR 개발 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-108">This tutorial demonstrates the following SignalR development tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="22c09-109">ASP.NET Core 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-109">Create an ASP.NET Core web app.</span></span>
> * <span data-ttu-id="22c09-110">클라이언트에 콘텐츠를 푸시 하려면 SignalR 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-110">Create a SignalR hub to push content to clients.</span></span>
> * <span data-ttu-id="22c09-111">SignalR JavaScript 라이브러리를 사용 하 여 메시지를 보내고을 허브에서 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-111">Use the SignalR JavaScript library to send messages and display updates from the hub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22c09-112">전제 조건</span><span class="sxs-lookup"><span data-stu-id="22c09-112">Prerequisites</span></span>

<span data-ttu-id="22c09-113">다음 소프트웨어를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-113">Install the following software:</span></span>

* <span data-ttu-id="22c09-114">[.NET core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) 이상 버전</span><span class="sxs-lookup"><span data-stu-id="22c09-114">[.NET Core 2.1.0 Preview 1 SDK](https://www.microsoft.com/net/download/dotnet-core/sdk-2.1.300-preview1) or later</span></span>
* <span data-ttu-id="22c09-115">[Visual Studio 2017](https://www.visualstudio.com/downloads/) 15.6 ASP.NET 및 웹 개발 작업의 이후 버전</span><span class="sxs-lookup"><span data-stu-id="22c09-115">[Visual Studio 2017](https://www.visualstudio.com/downloads/) version 15.6 or later with the ASP.NET and web development workload</span></span>
* [<span data-ttu-id="22c09-116">npm</span><span class="sxs-lookup"><span data-stu-id="22c09-116">npm</span></span>](https://www.npmjs.com/get-npm)

## <a name="create-an-aspnet-core-project-that-hosts-signalr-client-and-server"></a><span data-ttu-id="22c09-117">SignalR 클라이언트와 서버를 호스팅하는 ASP.NET Core 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="22c09-117">Create an ASP.NET Core project that hosts SignalR client and server</span></span>

1. <span data-ttu-id="22c09-118">사용 하 여는 **파일** > **새 프로젝트** 메뉴 옵션 선택한 **ASP.NET Core 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-118">Use the **File** > **New Project** menu option and choose **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="22c09-119">프로젝트 이름을 `SignalRChat`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-119">Name the project `SignalRChat`.</span></span>

  ![Visual Studio에서 새 프로젝트 대화 상자](get-started-signalr-core/_static/signalr-new-project-dialog.png)

2. <span data-ttu-id="22c09-121">선택 **웹 응용 프로그램** Razor 페이지를 사용 하 여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-121">Select **Web Application** to create a project using Razor Pages.</span></span> <span data-ttu-id="22c09-122">그런 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-122">Then select **Ok**.</span></span> <span data-ttu-id="22c09-123">수 있도록 **ASP.NET Core 2.1** SignalR 이전 버전의.NET에서 실행 하는 경우 프레임 워크 선택기에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-123">Be sure that **ASP.NET Core 2.1** is selected from the framework selector, though SignalR runs on older versions of .NET.</span></span>

  ![Visual Studio에서 새 프로젝트 대화 상자](get-started-signalr-core/_static/signalr-new-project-choose-type.png)

  <span data-ttu-id="22c09-125">SignalR의 서버 쪽 코드를 호스트 하는 라이브러리 프로젝트 템플릿에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-125">The libraries that host SignalR server-side code are included in the project template.</span></span> <span data-ttu-id="22c09-126">설치와 별도로 클라이언트 쪽 JavaScript [npm](https://www.npmjs.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-126">Install the client-side JavaScript separately with [npm](https://www.npmjs.com/).</span></span>

  ```console
   npm install @aspnet/signalr
  ```

3. <span data-ttu-id="22c09-127">복사는 *signalr.js* 에서 *node_modules\\ @aspnet\signalr\dist\browser*  에 *wwwroot\lib* 프로젝트의 폴더에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-127">Copy the *signalr.js* from *node_modules\\@aspnet\signalr\dist\browser* to the *wwwroot\lib* folder in your project.</span></span>

## <a name="create-the-signalr-hub"></a><span data-ttu-id="22c09-128">SignalR 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-128">Create the SignalR Hub</span></span>

<span data-ttu-id="22c09-129">허브는 클라이언트와 서버에서 다른 메서드를 호출할 수 있도록 하는 높은 수준의 파이프라인으로 사용 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-129">A hub is a class that serves as a high-level pipeline that allows the client and server to call methods on each other.</span></span>

1. <span data-ttu-id="22c09-130">클래스를 선택 하 여 프로젝트에 추가 **파일** > **새로** > **파일** 선택 하 고 **Visual C# 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-130">Add a class to the project by choosing **File** > **New** > **File** and selecting **Visual C# Class**.</span></span> 

1. <span data-ttu-id="22c09-131">상속 `Microsoft.AspNetCore.SignalR.Hub`합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-131">Inherit from `Microsoft.AspNetCore.SignalR.Hub`.</span></span> <span data-ttu-id="22c09-132">`Hub` 속성과 송신 및 수신 데이터 뿐 아니라 연결 그룹을 관리 하기 위한 이벤트 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-132">The `Hub` class contains properties and events for managing connections and groups, as well as sending and receiving data.</span></span>

1. <span data-ttu-id="22c09-133">만들기는 `Send` 모든 연결 된 채팅 클라이언트에 메시지를 보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-133">Create the `Send` method that sends a message to all connected chat clients.</span></span> <span data-ttu-id="22c09-134">반환 확인는 `Task`SignalR 비동기 이기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-134">Notice it returns a `Task`, because SignalR is asynchronous.</span></span> <span data-ttu-id="22c09-135">비동기 코드 확장성이 좋아집니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-135">Asynchronous code scales better.</span></span>

  [!code-csharp[Startup](get-started-signalr-core/sample/Hubs/ChatHub.cs?range=7-14)]

## <a name="configure-the-project-to-use-signalr"></a><span data-ttu-id="22c09-136">SignalR을 사용 하도록 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-136">Configure the project to use SignalR</span></span>

<span data-ttu-id="22c09-137">SignalR 서버 signalr 요청을 전달 하려면 알 수 있도록 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-137">The SignalR server must be configured so that it knows to pass requests to SignalR.</span></span>

1. <span data-ttu-id="22c09-138">SignalR 프로젝트를 구성 하려면 수정 된 `ConfigureServices` 메서드는 응용 프로그램의 `Startup` 클래스에 대 한 호출을 삽입 하 여 `services.AddSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-138">To configure a SignalR project, modify the `ConfigureServices` method of the application's `Startup` class by inserting a call to `services.AddSignalR`.</span></span>

  <span data-ttu-id="22c09-139">`services.AddSignalR` SignalR의 일부로 추가 [ASP.NET Core 미들웨어](xref:fundamentals/middleware/index) 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="22c09-139">`services.AddSignalR` adds SignalR as part of the [ASP.NET Core middleware](xref:fundamentals/middleware/index) pipeline.</span></span>

1. <span data-ttu-id="22c09-140">사용 하 여 허브에 대 한 라우팅을 구성 `UseSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-140">Configure routes to your hubs using `UseSignalR`.</span></span>

  [!code-csharp[Startup](get-started-signalr-core/sample/Startup.cs?highlight=22,40-43)]

## <a name="create-the-signalr-client-code"></a><span data-ttu-id="22c09-141">SignalR 클라이언트 코드 만들기</span><span class="sxs-lookup"><span data-stu-id="22c09-141">Create the SignalR client code</span></span>

1. <span data-ttu-id="22c09-142">에서는 교체 *Pages\Index.cshtml* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="22c09-142">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

  [!code-cshtml[Index](get-started-signalr-core/sample/Pages/Index.cshtml)]

  <span data-ttu-id="22c09-143">위의 HTML 이름 및 메시지 필드 및 전송 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-143">The preceding HTML displays name and message fields, and a submit button.</span></span> <span data-ttu-id="22c09-144">맨 아래에 스크립트 참조를 확인: SignalR에 대 한 참조 및 *chat.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-144">Notice the script references at the bottom: a reference to SignalR and *chat.js*.</span></span>

1. <span data-ttu-id="22c09-145">에 JavaScript 파일을 추가 *wwwroot\js* 라는 폴더 *chat.js* 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-145">Add a JavaScript file to the *wwwroot\js* folder named *chat.js* and add the following code to it:</span></span>

  [!code-javascript[Index](get-started-signalr-core/sample/wwwroot/js/chat.js)]

## <a name="run-the-app"></a><span data-ttu-id="22c09-146">앱 실행</span><span class="sxs-lookup"><span data-stu-id="22c09-146">Run the app</span></span>

1. <span data-ttu-id="22c09-147">선택 **디버그** > **디버깅 하지 않고 시작** 브라우저를 실행 하 여 로컬 웹 사이트를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-147">Select **Debug** > **Start without debugging** to launch a browser and load the website locally.</span></span> <span data-ttu-id="22c09-148">주소 표시줄에서 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-148">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="22c09-149">다른 브라우저 인스턴스 (모든 브라우저)를 열고 주소 표시줄에 URL을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-149">Open another browser instance (any browser) and paste the URL in the address bar.</span></span>

1. <span data-ttu-id="22c09-150">브라우저 중 하나를 선택 하 고, 이름 및 메시지를 입력 한 다음 클릭는 **보낼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-150">Choose either browser, enter a name and message, and click the **Send** button.</span></span> <span data-ttu-id="22c09-151">이름 및 메시지는 두 페이지에 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c09-151">The name and message are displayed on both pages instantly.</span></span>

  ![솔루션](get-started-signalr-core/_static/signalr-get-started-finished.png)
