---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: '자습서: SignalR 시작 1.x 및 MVC 4 | Microsoft Docs'
author: pfletcher
description: ASP.NET SignalR 및 ASP.NET MVC 4를 사용 하 여 실시간 채팅 응용 프로그램을 빌드합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/29/2013
ms.topic: article
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 1ae330be5caf00c3cac7451f326398c0958538af
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873721"
---
<a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="c485f-103">자습서: SignalR 시작 1.x 및 MVC 4</span><span class="sxs-lookup"><span data-stu-id="c485f-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>
====================
<span data-ttu-id="c485f-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="c485f-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

> <span data-ttu-id="c485f-105">이 자습서에는 실시간 채팅 응용 프로그램을 만들려면 ASP.NET SignalR을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="c485f-106">SignalR MVC 4 응용 프로그램에 추가 되며 채팅 보기를 만들어 보내고, 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>


## <a name="overview"></a><span data-ttu-id="c485f-107">개요</span><span class="sxs-lookup"><span data-stu-id="c485f-107">Overview</span></span>

<span data-ttu-id="c485f-108">이 자습서에서는 실시간 웹 응용 프로그램 개발 ASP.NET SignalR 및 ASP.NET MVC 4 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="c485f-109">이 자습서에 동일한 채팅 응용 프로그램 코드를 사용 하 여는 [SignalR 시작 자습서](tutorial-getting-started-with-signalr.md), 있지만 인터넷 템플릿을 기반으로 하는 MVC 4 응용 프로그램에 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="c485f-110">이 항목의 다음 SignalR 개발 작업에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="c485f-111">MVC 4 응용 프로그램에 SignalR 라이브러리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="c485f-112">클라이언트에 콘텐츠를 푸시 하려면 허브 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="c485f-113">웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="c485f-114">다음 스크린 샷에서 브라우저에서 실행 되는 완료 된 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![채팅 인스턴스](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="c485f-116">섹션:</span><span class="sxs-lookup"><span data-stu-id="c485f-116">Sections:</span></span>

- [<span data-ttu-id="c485f-117">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="c485f-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="c485f-118">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="c485f-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="c485f-119">코드 검사</span><span class="sxs-lookup"><span data-stu-id="c485f-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="c485f-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c485f-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="c485f-121">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="c485f-121">Set up the Project</span></span>

<span data-ttu-id="c485f-122">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="c485f-122">Prerequisites:</span></span>

- <span data-ttu-id="c485f-123">Visual Studio 2010 SP1, Visual Studio 2012 또는 Visual Studio 2012 Express를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="c485f-124">Visual Studio가 참조 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2012 Express 개발 도구를 얻으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="c485f-125">Visual Studio 2010 설치 [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="c485f-126">이 섹션에는 ASP.NET MVC 4 응용 프로그램을 만들 SignalR 라이브러리를 추가 하 고 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="c485f-127">Visual Studio에서 ASP.NET MVC 4 응용 프로그램, 만들고 SignalRChat, 이름 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="c485f-128">VS 2010에서 선택 **.NET Framework 4** Framework 버전 드롭다운 컨트롤에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="c485f-129">SignalR 코드는.NET Framework 버전 4 및 4.5에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![Mvc 웹 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="c485f-131">인터넷 응용 프로그램 템플릿을 선택, 옵션을 선택 취소 **단위 테스트 프로젝트 만들기**, 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![Mvc 인터넷 사이트 만들기](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="c485f-133">열기는 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔** 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-133">Open the **Tools | Library Package Manager | Package Manager Console** and run the following command.</span></span> <span data-ttu-id="c485f-134">이 단계는 SignalR 기능을 사용 하는 어셈블리 참조 및 스크립트 파일 집합이 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="c485f-135">**솔루션 탐색기** 스크립트 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="c485f-136">SignalR에 대 한 스크립트 라이브러리를 프로젝트에 추가한 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![라이브러리 참조](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="c485f-138">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 선택 **추가 | 새 폴더**, 라는 새 폴더를 추가 하 고 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="c485f-139">마우스 오른쪽 단추로 클릭는 **허브** 폴더를 클릭 하 여 **추가 | 클래스**, C# 라는 새 클래스를 만들고 **ChatHub.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="c485f-140">이 클래스는 모든 클라이언트에 메시지를 보내는 SignalR 서버 허브로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="c485f-141">설치한 후 Visual Studio 2012를 사용 하는 경우는 [ASP.NET 및 웹 도구 2012.2 업데이트](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), 허브 클래스를 만드는 새 SignalR 항목 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="c485f-142">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **허브** 폴더를 클릭 하 여 **추가 | 새 항목**선택, **SignalR 허브 클래스 (v1)**, 클래스 이름을 지정 하 고 **ChatHub.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>


1. <span data-ttu-id="c485f-143">코드는 **ChatHub** 를 다음 코드로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="c485f-144">열기는 **Global.asax** 메서드 호출을 추가 하 고 프로젝트에 대 한 파일 `RouteTable.Routes.MapHubs();` 에 코드의 첫 번째 줄으로는 `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c485f-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="c485f-145">이 코드는 SignalR 허브에 대 한 기본 경로 등록 하 고 다른 경로 등록 하기 전에 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="c485f-146">전체 `Application_Start` 메서드는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="c485f-147">편집는 `HomeController` 에서 클래스를 찾을 **Controllers/HomeController.cs** 클래스에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="c485f-148">이 메서드는 반환 된 **채팅** 이후 단계에서 만들 보기.</span><span class="sxs-lookup"><span data-stu-id="c485f-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="c485f-149">내에서 마우스 오른쪽 단추로 클릭는 `Chat` 메서드 고 사용자가 방금 만든 클릭 **뷰 추가** 새 뷰 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="c485f-150">에 **뷰 추가** 대화 상자에서 하는 확인란을 선택 해야 **레이아웃 또는 마스터 페이지를 사용 하 여** (다른 확인란의 선택을 취소)를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![보기 추가](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="c485f-152">명명 된 새 보기 파일 편집 **Chat.cshtml**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="c485f-153">이후에 &lt;h2&gt; 태그, ¿© ³ ö &lt;div&gt; 섹션 및 `@section scripts` 페이지에 코드 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="c485f-154">이 스크립트는 채팅 메시지를 보내고 서버에서 메시지를 표시 하려면 페이지를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="c485f-155">채팅 보기에 대 한 전체 코드는 다음 코드 블록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c485f-156">Visual Studio 프로젝트에 SignalR 및 기타 스크립트 라이브러리를 추가 하면 패키지 관리자는이 항목에 표시 된 버전 보다 최신인 버전은 스크립트의 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="c485f-157">스크립트 참조를 코드에서 프로젝트에 설치 된 스크립트 라이브러리의 버전 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="c485f-158">**모두 저장** 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="c485f-159">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="c485f-159">Run the Sample</span></span>

1. <span data-ttu-id="c485f-160">F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="c485f-161">브라우저 주소 표시줄에 추가할 **/home/채팅** 프로젝트에 대 한 기본 페이지의 url입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="c485f-162">채팅 페이지 사용자 이름에 대 한 프롬프트 및 브라우저 인스턴스를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="c485f-164">사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-164">Enter a user name.</span></span>
4. <span data-ttu-id="c485f-165">브라우저의 주소 표시줄에서 URL을 복사 하 고 두 인스턴스를 열어 자세한 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="c485f-166">각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="c485f-167">각 브라우저 인스턴스에서 주석을 추가 하 고 클릭 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="c485f-168">모든 브라우저 인스턴스에 주석을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c485f-169">이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="c485f-170">허브 모든 현재 사용자에 게 의견을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="c485f-171">사용자에 게 채팅을 나중에 조인에 참여할 때부터 추가 된 메시지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="c485f-172">다음 스크린 샷에서 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![채팅 브라우저](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="c485f-174">**솔루션 탐색기**, 검사는 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="c485f-175">이 노드는 브라우저로 Internet Explorer를 사용 하는 경우 디버그 모드에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="c485f-176">라는 스크립트 파일이 **허브** SignalR 라이브러리를 런타임에 동적으로 생성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="c485f-177">이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="c485f-178">Internet Explorer 이외의 브라우저를 사용 하면 동적 액세스할 수도 있습니다 **허브** 파일을 찾아 직접 예를 들어 http://mywebsite/signalr/hubs합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![생성 된 허브 스크립트](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="c485f-180">코드 검사</span><span class="sxs-lookup"><span data-stu-id="c485f-180">Examine the Code</span></span>

<span data-ttu-id="c485f-181">SignalR 채팅 응용 프로그램에서는 두 가지 기본 SignalR 개발 작업: 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 주고받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="c485f-182">SignalR 허브</span><span class="sxs-lookup"><span data-stu-id="c485f-182">SignalR Hubs</span></span>

<span data-ttu-id="c485f-183">코드 예제에서는 **ChatHub** 클래스에서 파생 되는 **Microsoft.AspNet.SignalR.Hub** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="c485f-184">파생 되는 **허브** 클래스는 SignalR 응용 프로그램을 작성 하는 유용한 방법은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="c485f-185">허브 클래스에 공용 메서드를 만들고 그런 다음 웹 페이지의 jQuery 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="c485f-186">클라이언트 채팅 코드에서 호출할는 **ChatHub.Send** 메서드 새 메시지를 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="c485f-187">허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 **Clients.All.addNewMessageToPage**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="c485f-188">**보낼** 메서드 여러 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="c485f-189">클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="c485f-190">사용 하 여는 **Microsoft.AspNet.SignalR.Hub.Clients** 이 허브에 연결 된 속성을 모든 클라이언트에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="c485f-191">클라이언트에서 jQuery 함수 호출 (예:는 `addNewMessageToPage` 함수) 클라이언트를 업데이트 하려면.</span><span class="sxs-lookup"><span data-stu-id="c485f-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="c485f-192">SignalR 및 jQuery</span><span class="sxs-lookup"><span data-stu-id="c485f-192">SignalR and jQuery</span></span>

<span data-ttu-id="c485f-193">**Chat.cshtml** 코드 샘플에서 파일 보기에는 SignalR 허브와 통신 하는 SignalR jQuery 라이브러리를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="c485f-194">코드에는 필수 작업 자동 생성 된 프록시에는 허브에 대 한 서버를 클라이언트에 대 한 밀어넣기 콘텐츠를 호출할 수 있는 함수를 선언 하 고 연결을 시작 하는 허브에 메시지를 보낼 대 한 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="c485f-195">다음 코드를 허브에 대 한 프록시를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="c485f-196">JQuery 서버 클래스 및 해당 멤버에 대 한 참조에서 카멜식 대/소문자는입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="c485f-197">코드 샘플 참조는 C# **ChatHub** 으로 jQuery 클래스 **chatHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="c485f-198">참조 하려는 경우는 `ChatHub` 클래스 규칙에 따른 파스칼와 jQuery에서 ChatHub.cs 클래스 파일을 편집 C#에서 마찬가지로 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="c485f-199">추가 `using` 문을 참조 하는 `Microsoft.AspNet.SignalR.Hubs` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="c485f-200">그런 다음 추가 `HubName` 특성을 `ChatHub` 클래스, 예를 들어 `[HubName("ChatHub")]`합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="c485f-201">jQuery 참조를 마지막으로 업데이트는 `ChatHub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>


<span data-ttu-id="c485f-202">다음 코드를 스크립트에는 콜백 함수를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="c485f-203">서버에서 허브 클래스에는 각 클라이언트에 콘텐츠 업데이트 적용 하려면이 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="c485f-204">에 대 한 선택적 호출은 `htmlEncode` 함수를 HTML로 변환 하는 방법 보여 주는 스크립트 삽입을 방지 하는 방법으로 페이지에 표시 하기 전에 메시지 내용을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="c485f-205">다음 코드에는 허브에 대 한 연결을 여는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="c485f-206">연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 하는 코드는 **보낼** 채팅 페이지의에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="c485f-207">이 방법을 사용 하면 이벤트 처리기 실행 되기 전에 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-207">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="c485f-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c485f-208">Next Steps</span></span>

<span data-ttu-id="c485f-209">SignalR은 실시간 웹 응용 프로그램을 구축 하기 위한 프레임 워크는 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="c485f-210">여러 가지 SignalR 개발 작업에 배웠습니다: SignalR ASP.NET 응용 프로그램에 추가 하는 방법, 허브 클래스를 만드는 방법 및 보내고 허브에서 메시지를 수신 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c485f-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="c485f-211">SignalR 개발 보다 발전된 된 개념을 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c485f-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="c485f-212">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c485f-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="c485f-213">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="c485f-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="c485f-214">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="c485f-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
