---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN 및 Katana 시작 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 9920861da0e67d9304a944cacfb8ff8685267cd6
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48913179"
---
<a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="7bc68-102">OWIN 및 Katana 시작</span><span class="sxs-lookup"><span data-stu-id="7bc68-102">Getting Started with OWIN and Katana</span></span>
====================
<span data-ttu-id="7bc68-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7bc68-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7bc68-104">[.NET (OWIN)에 대 한 open Web Interface](http://owin.org/) .NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="7bc68-105">응용 프로그램에서 웹 서버를 분리 하 여 OWIN 쉽게.NET 웹 개발에 대 한 미들웨어를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="7bc68-106">또한 OWIN 쉽게 다른 호스트에 포트 웹 응용 프로그램&#8212;예를 들어, Windows 서비스 또는 다른 프로세스에서 자체 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="7bc68-107">OWIN는 커뮤니티 소유 사양을 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="7bc68-108">Katana 프로젝트에는 Microsoft에서 개발한 오픈 소스 OWIN 구성 요소 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="7bc68-109">OWIN 및 Katana를 둘 다의 일반적인 개요를 참조 하세요 [는 프로젝트 Katana 개요](an-overview-of-project-katana.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="7bc68-110">이 문서에서는 시작 코드에 바로 필자입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="7bc68-111">이 자습서에서는 [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566)를 쓰지만 Visual Studio 2012를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="7bc68-112">몇 가지 단계를 아래 언급 하는 Visual Studio 2012에서 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="7bc68-113">IIS에 OWIN 호스트</span><span class="sxs-lookup"><span data-stu-id="7bc68-113">Host OWIN in IIS</span></span>

<span data-ttu-id="7bc68-114">이 섹션에서는 IIS에서 OWIN 호스트할 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="7bc68-115">이 옵션의 유연성과 IIS 완성도 높은 기능 집합과 함께 OWIN 파이프라인을 작성 하는 가능성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="7bc68-116">ASP.NET 요청 파이프라인에서 OWIN 응용 프로그램 실행이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="7bc68-117">먼저 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="7bc68-118">(Visual Studio 2012에서 ASP.NET 빈 웹 응용 프로그램 프로젝트 형식을 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="7bc68-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="7bc68-119">에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="7bc68-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="7bc68-120">NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="7bc68-120">Add NuGet Packages</span></span>

<span data-ttu-id="7bc68-121">다음으로 필요한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="7bc68-122">**도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-122">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7bc68-123">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="7bc68-124">시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="7bc68-124">Add a Startup Class</span></span>

<span data-ttu-id="7bc68-125">다음에 OWIN 시작 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="7bc68-126">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**을 선택한 후 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="7bc68-127">에 **새 항목 추가** 대화 상자에서 **Owin 시작 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="7bc68-128">Startup 클래스를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [OWIN 시작 클래스 검색](owin-startup-class-detection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="7bc68-129">`Startup1.Configuration` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="7bc68-130">OWIN 파이프라인을 수신 하는 함수로 구현에 간단한 부분 미들웨어를 추가 하는이 코드는 **Microsoft.Owin.IOwinContext** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="7bc68-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="7bc68-131">서버는 HTTP 요청을 받으면 OWIN 파이프라인을 미들웨어를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="7bc68-132">미들웨어는 응답의 콘텐츠 형식을 설정 하 고 응답 본문을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="7bc68-133">OWIN 시작 클래스 템플릿을 Visual Studio 2013에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="7bc68-134">라는 비어 있는 새 클래스가 추가 Visual Studio 2012를 사용 하는 경우 `Startup1`, 다음 코드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="7bc68-135">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bc68-135">Run the Application</span></span>

<span data-ttu-id="7bc68-136">F5 키를 눌러 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="7bc68-137">Visual Studio는 브라우저 창이 열립니다 `http://localhost:*port*/`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="7bc68-138">페이지는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="7bc68-139">콘솔 응용 프로그램의 OWIN 자체 호스팅</span><span class="sxs-lookup"><span data-stu-id="7bc68-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="7bc68-140">사용자 지정 프로세스에서 자체 호스팅되는 IIS 호스팅에서이 응용 프로그램을 변환 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="7bc68-141">IIS는 IIS 호스팅을 사용 하 여 HTTP 서버와 서비스를 호스팅하는 프로세스와 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="7bc68-142">자체 호스팅을 사용 하 여 응용 프로그램 프로세스를 만들고 사용 합니다 **HttpListener** 클래스는 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="7bc68-143">Visual Studio에서 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="7bc68-144">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="7bc68-145">추가 된 `Startup1` 프로젝트에이 자습서의 1 부에서 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="7bc68-146">이 클래스를 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-146">You don't need to modify this class.</span></span>

<span data-ttu-id="7bc68-147">응용 프로그램의 구현 `Main` 같이 메서드.</span><span class="sxs-lookup"><span data-stu-id="7bc68-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="7bc68-148">서버 수신 대기 하기 시작 하는 콘솔 응용 프로그램을 실행 하는 경우 `http://localhost:9000`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="7bc68-149">웹 브라우저에서이 주소로 이동 하면 "Hello world" 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="7bc68-150">OWIN에 대 한 진단 유틸리티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="7bc68-151">Microsoft.Owin.Diagnostics 패키지는 처리 되지 않은 예외를 catch 하 고 오류 세부 정보를 사용 하 여 HTML 페이지를 표시 하는 미들웨어를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="7bc68-152">이 페이지 함수 처럼이 라고도 하는 ASP.NET 오류 페이지는 "[노란색 퍼플 스크린이](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span><span class="sxs-lookup"><span data-stu-id="7bc68-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="7bc68-153">YSOD와 같은 개발 하는 동안 Katana 오류 페이지는 유용 하지만 프로덕션 모드에서 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="7bc68-154">프로젝트에서 진단 패키지를 설치 하려면 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="7bc68-155">코드를 변경 하면 `Startup1.Configuration` 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="7bc68-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="7bc68-156">이제 Visual Studio 예외에서 중단 되지 것입니다 있도록 디버깅 하지 않고 응용 프로그램을 실행 하려면 CTRL + F5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="7bc68-157">응용 프로그램 동일 하 게 이전과 마찬가지로 이동할 때까지 `http://localhost/fail`,이 시점에서 응용 프로그램 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="7bc68-158">오류 페이지 미들웨어는 예외를 catch 하 고 오류에 대 한 정보를 사용 하 여 HTML 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="7bc68-159">스택, 쿼리 문자열, 쿠키, 요청 헤더 및 OWIN 환경 변수를 보려면 탭을 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bc68-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="7bc68-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7bc68-160">Next Steps</span></span>

- [<span data-ttu-id="7bc68-161">OWIN 시작 클래스 검색</span><span class="sxs-lookup"><span data-stu-id="7bc68-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="7bc68-162">OWIN을 사용 하 여 자체 호스트 하는 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="7bc68-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="7bc68-163">OWIN을 사용 하 여 SignalR 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="7bc68-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
