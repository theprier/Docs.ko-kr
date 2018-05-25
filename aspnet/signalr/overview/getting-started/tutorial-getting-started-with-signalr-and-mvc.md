---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: '자습서: SignalR 2 및 MVC 5 시작 | Microsoft Docs'
author: pfletcher
description: 이 자습서에는 실시간 채팅 응용 프로그램을 만들려면 ASP.NET SignalR 2를 사용 하는 방법을 보여 줍니다. SignalR MVC 5 응용 프로그램에 추가 하 고 채팅 보기를 만드는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.openlocfilehash: ca0471114da7363c5df9d459308708e7ab4f8b84
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="tutorial-getting-started-with-signalr-2-and-mvc-5"></a><span data-ttu-id="9af61-104">자습서: SignalR 2 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="9af61-104">Tutorial: Getting Started with SignalR 2 and MVC 5</span></span>
====================
<span data-ttu-id="9af61-105">여 [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="9af61-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[<span data-ttu-id="9af61-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

> <span data-ttu-id="9af61-107">이 자습서에는 실시간 채팅 응용 프로그램을 만들려면 ASP.NET SignalR 2를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-107">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="9af61-108">SignalR MVC 5 응용 프로그램에 추가 되며 채팅 보기를 만들어 보내고, 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-108">You will add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span> 
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9af61-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="9af61-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="9af61-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9af61-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="9af61-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="9af61-111">.NET 4.5</span></span>
> - <span data-ttu-id="9af61-112">MVC 5</span><span class="sxs-lookup"><span data-stu-id="9af61-112">MVC 5</span></span>
> - <span data-ttu-id="9af61-113">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="9af61-113">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="9af61-114">이 자습서와 함께 Visual Studio 2012를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9af61-114">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="9af61-115">이 자습서와 함께 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-115">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="9af61-116">업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 를 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-116">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="9af61-117">설치는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-117">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="9af61-118">웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-118">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="9af61-119">SignalR 클래스에 대 한 Visual Studio 템플릿을와 같은 설치 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-119">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="9af61-120">일부 서식 파일 (와 같은 **OWIN 시작 클래스**)은 사용할 수 없습니다; 이러한 경우에 대 한 클래스 파일을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-120">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="9af61-121">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="9af61-121">Tutorial Versions</span></span>
> 
> <span data-ttu-id="9af61-122">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-122">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="9af61-123">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="9af61-123">Questions and comments</span></span>
> 
> <span data-ttu-id="9af61-124">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="9af61-124">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="9af61-125">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-125">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="9af61-126">개요</span><span class="sxs-lookup"><span data-stu-id="9af61-126">Overview</span></span>

<span data-ttu-id="9af61-127">이 자습서는 ASP.NET SignalR 2 및 ASP.NET MVC 5 실시간 웹 응용 프로그램 개발을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-127">This tutorial introduces you to real-time web application development with ASP.NET SignalR 2 and ASP.NET MVC 5.</span></span> <span data-ttu-id="9af61-128">이 자습서에 동일한 채팅 응용 프로그램 코드를 사용 하 여는 [SignalR 시작 자습서](tutorial-getting-started-with-signalr.md), 있지만 MVC 5 응용 프로그램에 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-128">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 5 application.</span></span>

<span data-ttu-id="9af61-129">이 항목의 다음 SignalR 개발 작업에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-129">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="9af61-130">MVC 5 응용 프로그램에 SignalR 라이브러리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-130">Adding the SignalR library to an MVC 5 application.</span></span>
- <span data-ttu-id="9af61-131">허브 및 클라이언트에 콘텐츠를 푸시 하려면 OWIN 시작 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="9af61-131">Creating hub and OWIN startup classes to push content to clients.</span></span>
- <span data-ttu-id="9af61-132">웹 페이지에서 SignalR jQuery 라이브러리를 사용 하 여 메시지를 보내고 허브에서 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-132">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="9af61-133">다음 스크린 샷에서 브라우저에서 실행 되는 완료 된 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-133">The following screen shot shows the completed chat application running in a browser.</span></span>

![채팅 인스턴스](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

<span data-ttu-id="9af61-135">섹션:</span><span class="sxs-lookup"><span data-stu-id="9af61-135">Sections:</span></span>

- [<span data-ttu-id="9af61-136">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="9af61-136">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="9af61-137">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="9af61-137">Run the Sample</span></span>](#run)
- [<span data-ttu-id="9af61-138">코드 검사</span><span class="sxs-lookup"><span data-stu-id="9af61-138">Examine the Code</span></span>](#code)
- [<span data-ttu-id="9af61-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9af61-139">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="9af61-140">프로젝트를 설정</span><span class="sxs-lookup"><span data-stu-id="9af61-140">Set up the Project</span></span>

<span data-ttu-id="9af61-141">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="9af61-141">Prerequisites:</span></span>

- <span data-ttu-id="9af61-142">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="9af61-142">Visual Studio 2013.</span></span> <span data-ttu-id="9af61-143">Visual Studio가 참조 [ASP.NET 다운로드](https://www.asp.net/downloads) 무료 Visual Studio 2013 Express 개발 도구를 얻으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-143">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express Development Tool.</span></span>

<span data-ttu-id="9af61-144">이 섹션에는 ASP.NET MVC 5 응용 프로그램을 만들고 SignalR 라이브러리를 추가, 채팅 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-144">This section shows how to create an ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="9af61-145">Visual Studio에서.NET Framework 4.5를 대상으로 하는 C# ASP.NET 응용 프로그램을 만듭니다 SignalRChat, 라는 이름을 지정 하 고 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-145">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![웹 만들기](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)
2. <span data-ttu-id="9af61-147">에 `New ASP.NET Project` 대화 상자를 닫고 선택 **MVC**를 클릭 하 고 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-147">In the `New ASP.NET Project` dialog, and select **MVC**, and click **Change Authentication**.</span></span>

    ![웹 만들기](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)
3. <span data-ttu-id="9af61-149">선택 **인증 안 함** 에 **인증 변경** 대화 상자를 닫고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-149">Select **No Authentication** in the **Change Authentication** dialog, and click **OK**.</span></span>

    ![인증 안 함 선택](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="9af61-151">응용 프로그램에 대 한 다른 인증 공급자를 선택 하는 경우는 `Startup.cs` 클래스를 생성 됩니다; 직접 만들 필요가 `Startup.cs` 10 아래 단계에는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-151">If you select a different authentication provider for your application, a `Startup.cs` class will be created for you; you will not need to create your own `Startup.cs` class in step 10 below.</span></span>
4. <span data-ttu-id="9af61-152">클릭 **확인** 에 **새 ASP.NET 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="9af61-152">Click **OK** in the **New ASP.NET Project** dialog.</span></span>
5. <span data-ttu-id="9af61-153">열기는 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔** 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-153">Open the **Tools | Library Package Manager | Package Manager Console** and run the following command.</span></span> <span data-ttu-id="9af61-154">이 단계는 SignalR 기능을 사용 하는 어셈블리 참조 및 스크립트 파일 집합이 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-154">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

    `install-package Microsoft.AspNet.SignalR`
6. <span data-ttu-id="9af61-155">**솔루션 탐색기**, 스크립트 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-155">In **Solution Explorer**, expand the Scripts folder.</span></span> <span data-ttu-id="9af61-156">SignalR에 대 한 스크립트 라이브러리를 프로젝트에 추가한 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-156">Note that script libraries for SignalR have been added to the project.</span></span>

    ![스크립트 폴더](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)
7. <span data-ttu-id="9af61-158">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 선택 **추가 | 새 폴더**, 라는 새 폴더를 추가 하 고 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-158">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
8. <span data-ttu-id="9af61-159">마우스 오른쪽 단추로 클릭는 **허브** 폴더를 클릭 하 여 **추가 | 새 항목**, 선택는 **Visual C# | 웹 | SignalR** 에서 노드는 **설치 됨** 창에서 **SignalR 허브 클래스 (v2)** 가운데 창에서 명명 된 새 허브를 만들고 **ChatHub.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-159">Right-click the **Hubs** folder, click **Add | New Item**, select the **Visual C# | Web | SignalR** node in the **Installed** pane, select **SignalR Hub Class (v2)** from the center pane, and create a new hub named **ChatHub.cs**.</span></span> <span data-ttu-id="9af61-160">이 클래스는 모든 클라이언트에 메시지를 보내는 SignalR 서버 허브로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-160">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

    ![새 허브를 만듭니다.](tutorial-getting-started-with-signalr-and-mvc/_static/image6.png)
9. <span data-ttu-id="9af61-162">코드는 **ChatHub** 를 다음 코드로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-162">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]
10. <span data-ttu-id="9af61-163">Startup.cs 라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-163">Create a new class called Startup.cs.</span></span> <span data-ttu-id="9af61-164">다음에 파일의 내용을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-164">Change the contents of the file to the following.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]
11. <span data-ttu-id="9af61-165">편집는 `HomeController` 에서 클래스를 찾을 **Controllers/HomeController.cs** 클래스에 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-165">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="9af61-166">이 메서드는 반환 된 **채팅** 이후 단계에서 만들 보기.</span><span class="sxs-lookup"><span data-stu-id="9af61-166">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]
12. <span data-ttu-id="9af61-167">마우스 오른쪽 단추로 클릭는 **뷰/홈** 폴더를 찾아 선택 **추가... | 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-167">Right-click the **Views/Home** folder, and select **Add... | View**.</span></span>
13. <span data-ttu-id="9af61-168">에 **뷰 추가** 대화 상자에서 새 뷰 이름 **채팅**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-168">In the **Add View** dialog, name the new view **Chat**.</span></span>

    ![보기 추가](tutorial-getting-started-with-signalr-and-mvc/_static/image7.png)
14. <span data-ttu-id="9af61-170">내용을 대체 **Chat.cshtml** 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-170">Replace the contents of **Chat.cshtml** with the following code.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9af61-171">SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자는이 항목에 표시 된 버전 보다 더 최신 SignalR 스크립트 파일의 버전을 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-171">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install a version of the SignalR script file that is more recent than the version shown in this topic.</span></span> <span data-ttu-id="9af61-172">코드에서 스크립트 참조가 프로젝트에 설치 된 스크립트 라이브러리의 버전이 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-172">Make sure that the script reference in your code matches the version of the script library installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]
15. <span data-ttu-id="9af61-173">**모두 저장** 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-173">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="9af61-174">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="9af61-174">Run the Sample</span></span>

1. <span data-ttu-id="9af61-175">F5 키를 눌러 디버그 모드에서 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-175">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="9af61-176">브라우저 주소 표시줄에 추가할 **/home/채팅** 프로젝트에 대 한 기본 페이지의 url입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-176">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="9af61-177">채팅 페이지 사용자 이름에 대 한 프롬프트 및 브라우저 인스턴스를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-177">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![사용자 이름 입력](tutorial-getting-started-with-signalr-and-mvc/_static/image8.png)
3. <span data-ttu-id="9af61-179">사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-179">Enter a user name.</span></span>
4. <span data-ttu-id="9af61-180">브라우저의 주소 표시줄에서 URL을 복사 하 고 두 인스턴스를 열어 자세한 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-180">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="9af61-181">각 브라우저 인스턴스에서 고유한 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-181">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="9af61-182">각 브라우저 인스턴스에서 주석을 추가 하 고 클릭 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-182">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="9af61-183">모든 브라우저 인스턴스에 주석을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-183">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9af61-184">이 간단한 채팅 응용 프로그램 서버에서 토론 컨텍스트를 유지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-184">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="9af61-185">허브 모든 현재 사용자에 게 의견을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-185">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="9af61-186">사용자에 게 채팅을 나중에 조인에 참여할 때부터 추가 된 메시지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-186">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="9af61-187">다음 스크린 샷에서 브라우저에서 실행 중인 채팅 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-187">The following screen shot shows the chat application running in a browser.</span></span>

    ![채팅 브라우저](tutorial-getting-started-with-signalr-and-mvc/_static/image9.png)
7. <span data-ttu-id="9af61-189">**솔루션 탐색기**, 검사는 **스크립트 문서** 실행 중인 응용 프로그램에 대 한 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-189">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="9af61-190">이 노드는 브라우저로 Internet Explorer를 사용 하는 경우 디버그 모드에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-190">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="9af61-191">라는 스크립트 파일이 **허브** SignalR 라이브러리를 런타임에 동적으로 생성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-191">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="9af61-192">이 파일 jQuery 스크립트와 서버 쪽 코드 간의 통신을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-192">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="9af61-193">Internet Explorer 이외의 브라우저를 사용 하면 동적 액세스할 수도 있습니다 **허브** 파일을 찾아 직접 예를 들어 http://mywebsite/signalr/hubs 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-193">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="9af61-194">코드 검사</span><span class="sxs-lookup"><span data-stu-id="9af61-194">Examine the Code</span></span>

<span data-ttu-id="9af61-195">SignalR 채팅 응용 프로그램에서는 두 가지 기본 SignalR 개발 작업: 서버에서 주 조정 개체로 허브를 만들고 SignalR jQuery 라이브러리를 사용 하 여 메시지를 주고받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-195">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="9af61-196">SignalR 허브</span><span class="sxs-lookup"><span data-stu-id="9af61-196">SignalR Hubs</span></span>

<span data-ttu-id="9af61-197">코드 예제에서는 **ChatHub** 클래스에서 파생 되는 **Microsoft.AspNet.SignalR.Hub** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-197">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="9af61-198">파생 되는 **허브** 클래스는 SignalR 응용 프로그램을 작성 하는 유용한 방법은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-198">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="9af61-199">허브 클래스에 공용 메서드를 만들고 그런 다음 웹 페이지의 스크립트에서 호출 하 여 이러한 메서드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-199">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="9af61-200">클라이언트 채팅 코드에서 호출할는 **ChatHub.Send** 메서드 새 메시지를 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-200">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="9af61-201">허브에 메시지를 보냅니다 모든 클라이언트를 호출 하 여 **Clients.All.addNewMessageToPage**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-201">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="9af61-202">**보낼** 메서드 여러 허브 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-202">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="9af61-203">클라이언트에서 호출할 수 있도록 허브에서 공용 메서드를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-203">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="9af61-204">사용 하 여는 **Microsoft.AspNet.SignalR.Hub.Clients** 이 허브에 연결 된 속성을 모든 클라이언트에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-204">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="9af61-205">클라이언트에서 함수를 호출 (예:는 `addNewMessageToPage` 함수) 클라이언트를 업데이트 하려면.</span><span class="sxs-lookup"><span data-stu-id="9af61-205">Call a function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="9af61-206">SignalR 및 jQuery</span><span class="sxs-lookup"><span data-stu-id="9af61-206">SignalR and jQuery</span></span>

<span data-ttu-id="9af61-207">**Chat.cshtml** 코드 샘플에서 파일 보기에는 SignalR 허브와 통신 하는 SignalR jQuery 라이브러리를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-207">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="9af61-208">코드에는 필수 작업 자동 생성 된 프록시에는 허브에 대 한 서버를 클라이언트에 대 한 밀어넣기 콘텐츠를 호출할 수 있는 함수를 선언 하 고 연결을 시작 하는 허브에 메시지를 보낼 대 한 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-208">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="9af61-209">다음 코드는 허브 프록시에 대 한 참조를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-209">The following code declares a reference to a hub proxy.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="9af61-210">JavaScript에서 카멜식 대 /에서 서버 클래스 및 해당 멤버에 대 한 참조는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-210">In JavaScript the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="9af61-211">코드 샘플 참조는 C# **ChatHub** 으로 JavaScript에서 클래스 **chatHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-211">The code sample references the C# **ChatHub** class in JavaScript as **chatHub**.</span></span> <span data-ttu-id="9af61-212">참조 하려는 경우는 `ChatHub` 클래스 규칙에 따른 파스칼와 jQuery에서 ChatHub.cs 클래스 파일을 편집 C#에서 마찬가지로 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-212">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="9af61-213">추가 `using` 문을 참조 하는 `Microsoft.AspNet.SignalR.Hubs` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-213">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="9af61-214">그런 다음 추가 `HubName` 특성을 `ChatHub` 클래스, 예를 들어 `[HubName("ChatHub")]`합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-214">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="9af61-215">jQuery 참조를 마지막으로 업데이트는 `ChatHub` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-215">Finally, update your jQuery reference to the `ChatHub` class.</span></span>


<span data-ttu-id="9af61-216">다음 코드를 스크립트에는 콜백 함수를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-216">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="9af61-217">서버에서 허브 클래스에는 각 클라이언트에 콘텐츠 업데이트 적용 하려면이 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-217">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="9af61-218">에 대 한 선택적 호출은 `htmlEncode` 함수를 HTML로 변환 하는 방법 보여 주는 스크립트 삽입을 방지 하는 방법으로 페이지에 표시 하기 전에 메시지 내용을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-218">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="9af61-219">다음 코드에는 허브에 대 한 연결을 여는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-219">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="9af61-220">연결을 시작 하 고 다음에 클릭 이벤트를 처리 하는 함수 전달 하는 코드는 **보낼** 채팅 페이지의에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-220">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="9af61-221">이 방법을 사용 하면 이벤트 처리기 실행 되기 전에 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-221">This approach ensures that the connection is established before the event handler executes.</span></span>


[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="9af61-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9af61-222">Next Steps</span></span>

<span data-ttu-id="9af61-223">SignalR은 실시간 웹 응용 프로그램을 구축 하기 위한 프레임 워크는 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-223">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="9af61-224">여러 가지 SignalR 개발 작업에 배웠습니다: SignalR ASP.NET 응용 프로그램에 추가 하는 방법, 허브 클래스를 만드는 방법 및 보내고 허브에서 메시지를 수신 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-224">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="9af61-225">샘플 SignalR 응용 프로그램을 Azure에 배포 하는 방법에 대 한 연습을을 참조 하십시오. [Azure 앱 서비스의 웹 앱과 함께 사용 하 여 SignalR](../deployment/using-signalr-with-azure-web-sites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-225">For a walkthrough on how to deploy the sample SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="9af61-226">Visual Studio 웹 프로젝트는 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 앱 서비스에서 ASP.NET 웹 앱을 만들](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9af61-226">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<span data-ttu-id="9af61-227">SignalR 개발 보다 발전된 된 개념을 알아보려면 SignalR 소스 코드 및 리소스에 대 한 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9af61-227">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="9af61-228">SignalR 프로젝트</span><span class="sxs-lookup"><span data-stu-id="9af61-228">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="9af61-229">SignalR Github 및 샘플</span><span class="sxs-lookup"><span data-stu-id="9af61-229">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="9af61-230">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="9af61-230">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
