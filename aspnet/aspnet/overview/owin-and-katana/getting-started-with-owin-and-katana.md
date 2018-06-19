---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN 및 Katana 시작 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/27/2013
ms.topic: article
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: ac0302ef1a786f6b1eef8119b3134a965f01c533
ms.sourcegitcommit: 5ab5c5f4bfdb0150f42ba84c2770eadf540cae48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
ms.locfileid: "30257680"
---
<a name="getting-started-with-owin-and-katana"></a><span data-ttu-id="9f2b1-102">OWIN 및 Katana 시작</span><span class="sxs-lookup"><span data-stu-id="9f2b1-102">Getting Started with OWIN and Katana</span></span>
====================
<span data-ttu-id="9f2b1-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="9f2b1-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="9f2b1-104">[.NET (OWIN)에 대 한 웹 인터페이스를 열고](http://owin.org/) .NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-104">[Open Web Interface for .NET (OWIN)](http://owin.org/) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="9f2b1-105">응용 프로그램에서 웹 서버를 분리 하 여 OWIN 쉽게.NET 웹 개발에 대 한 미들웨어를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-105">By decoupling the web server from the application, OWIN makes it easier to create middleware for .NET web development.</span></span> <span data-ttu-id="9f2b1-106">또한, OWIN 쉽게 다른 호스트에 포트 웹 응용 프로그램에&#8212;예를 들어 Windows 서비스 또는 다른 프로세스에서 자체 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-106">Also, OWIN makes it easier to port web applications to other hosts&#8212;for example, self-hosting in a Windows service or other process.</span></span>

<span data-ttu-id="9f2b1-107">OWIN는 커뮤니티 소유 사양, 구현 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-107">OWIN is a community-owned specification, not an implementation.</span></span> <span data-ttu-id="9f2b1-108">Katana 프로젝트가 Microsoft에서 개발 된 오픈 소스 OWIN 구성 요소 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-108">The Katana project is a set of open-source OWIN components developed by Microsoft.</span></span> <span data-ttu-id="9f2b1-109">OWIN 프로그램과 Katana의 일반적인 개요를 참조 하십시오. [An 프로젝트 Katana 개요](an-overview-of-project-katana.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-109">For a general overview of both OWIN and Katana, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="9f2b1-110">이 문서에서 시작 하는 코드를 바로 됩니다 I.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-110">In this article, I will jump right into code to get started.</span></span>

<span data-ttu-id="9f2b1-111">이 자습서에서는 [Visual Studio 2013 릴리스 후보](https://go.microsoft.com/fwlink/?LinkId=306566), 하지만 Visual Studio 2012를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-111">This tutorial uses [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), but you can also use Visual Studio 2012.</span></span> <span data-ttu-id="9f2b1-112">일부 단계는 아래 언급 있는 Visual Studio 2012 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-112">A few of the steps are different in Visual Studio 2012, which I note below.</span></span>

## <a name="host-owin-in-iis"></a><span data-ttu-id="9f2b1-113">OWIN IIS에서 호스트</span><span class="sxs-lookup"><span data-stu-id="9f2b1-113">Host OWIN in IIS</span></span>

<span data-ttu-id="9f2b1-114">이 섹션에서는 IIS에서 OWIN 호스팅할 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-114">In this section, we'll host OWIN in IIS.</span></span> <span data-ttu-id="9f2b1-115">이 옵션에는 유연성과 함께 IIS의 완성도 높은 기능 집합 OWIN 파이프라인의 작성 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-115">This option gives you the flexibility and composability of an OWIN pipeline together with the mature feature set of IIS.</span></span> <span data-ttu-id="9f2b1-116">OWIN 응용 프로그램이이 옵션을 사용 하는 ASP.NET 요청 파이프라인에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-116">Using this option, the OWIN application runs in the ASP.NET request pipeline.</span></span>

<span data-ttu-id="9f2b1-117">먼저 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-117">First, create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="9f2b1-118">(Visual Studio 2012에서 ASP.NET 빈 웹 응용 프로그램 프로젝트 형식을 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="9f2b1-118">(In Visual Studio 2012, use the ASP.NET Empty Web Application project type.)</span></span>

![](getting-started-with-owin-and-katana/_static/image1.png)

<span data-ttu-id="9f2b1-119">에 **새 ASP.NET 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-119">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span>

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a><span data-ttu-id="9f2b1-120">NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="9f2b1-120">Add NuGet Packages</span></span>

<span data-ttu-id="9f2b1-121">다음으로 데 필요한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-121">Next, add the required NuGet packages.</span></span> <span data-ttu-id="9f2b1-122">**도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-122">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="9f2b1-123">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-123">In the Package Manager Console window, type the following command:</span></span>

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a><span data-ttu-id="9f2b1-124">시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="9f2b1-124">Add a Startup Class</span></span>

<span data-ttu-id="9f2b1-125">OWIN 시작 클래스 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-125">Next, add an OWIN startup class.</span></span> <span data-ttu-id="9f2b1-126">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**을 선택한 후 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-126">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span> <span data-ttu-id="9f2b1-127">에 **새 항목 추가** 대화 상자에서 **Owin 시작 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-127">In the **Add New Item** dialog, select **Owin Startup class**.</span></span> <span data-ttu-id="9f2b1-128">시작 클래스를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [OWIN 시작 클래스 검색](owin-startup-class-detection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-128">For more info on configuring the startup class, see [OWIN Startup Class Detection](owin-startup-class-detection.md).</span></span>

![](getting-started-with-owin-and-katana/_static/image4.png)

<span data-ttu-id="9f2b1-129">`Startup1.Configuration` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-129">Add the following code to the `Startup1.Configuration` method:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

<span data-ttu-id="9f2b1-130">이 코드를 수신 하는 함수로 구현 OWIN 파이프라인에 미들웨어의 간단한 조각 추가 **Microsoft.Owin.IOwinContext** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-130">This code adds a simple piece of middleware to the OWIN pipeline, implemented as a function that receives a **Microsoft.Owin.IOwinContext** instance.</span></span> <span data-ttu-id="9f2b1-131">서버에서 HTTP 요청을 받으면 OWIN 파이프라인 미들웨어를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-131">When the server receives an HTTP request, the OWIN pipeline invokes the middleware.</span></span> <span data-ttu-id="9f2b1-132">미들웨어의 응답에 대 한 콘텐츠 형식을 설정 하 고 응답 본문을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-132">The middleware sets the content type for the response and writes the response body.</span></span>

> [!NOTE]
> <span data-ttu-id="9f2b1-133">OWIN 시작 클래스 템플릿을 Visual Studio 2013에서 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-133">The OWIN Startup class template is available in Visual Studio 2013.</span></span> <span data-ttu-id="9f2b1-134">Visual Studio 2012를 사용 하는 경우 라는 새 빈 클래스 추가 `Startup1`, 다음 코드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-134">If you are using Visual Studio 2012, just add a new empty class named `Startup1`, and paste in the following code:</span></span>


[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a><span data-ttu-id="9f2b1-135">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9f2b1-135">Run the Application</span></span>

<span data-ttu-id="9f2b1-136">F5 키를 눌러 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-136">Press F5 to begin debugging.</span></span> <span data-ttu-id="9f2b1-137">Visual Studio에 대 한 브라우저 창을 열립니다 `http://localhost:*port*/`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-137">Visual Studio will open a browser window to `http://localhost:*port*/`.</span></span> <span data-ttu-id="9f2b1-138">페이지는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-138">The page should look like the following:</span></span>

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a><span data-ttu-id="9f2b1-139">콘솔 응용 프로그램에서 자체 호스트 OWIN</span><span class="sxs-lookup"><span data-stu-id="9f2b1-139">Self-Host OWIN in a Console Application</span></span>

<span data-ttu-id="9f2b1-140">이 응용 프로그램에서 사용자 지정 프로세스의 자체 호스팅에 IIS 호스팅에서 변환 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-140">It's easy to convert this application from IIS hosting to self-hosting in a custom process.</span></span> <span data-ttu-id="9f2b1-141">IIS 호스팅와 IIS와 역할을 수행 HTTP 서버 서비스를 호스팅하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-141">With IIS hosting, IIS acts as both the HTTP server and as the process that hosts the service.</span></span> <span data-ttu-id="9f2b1-142">자체 호스팅을 사용 응용 프로그램 프로세스에서 만들고 사용 하는 **HttpListener** 클래스는 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-142">With self-hosting, your application creates the process and uses the **HttpListener** class as the HTTP server.</span></span>

<span data-ttu-id="9f2b1-143">Visual Studio에서 새 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-143">In Visual Studio, create a new console application.</span></span> <span data-ttu-id="9f2b1-144">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-144">In the Package Manager Console window, type the following command:</span></span>

`Install-Package Microsoft.Owin.SelfHost -Pre`

<span data-ttu-id="9f2b1-145">추가 `Startup1` 이 자습서의 1 단계에서 프로젝트에 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-145">Add a `Startup1` class from part 1 of this tutorial to the project.</span></span> <span data-ttu-id="9f2b1-146">이 클래스를 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-146">You don't need to modify this class.</span></span>

<span data-ttu-id="9f2b1-147">응용 프로그램의 구현 `Main` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-147">Implement the application's `Main` method as follows.</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

<span data-ttu-id="9f2b1-148">서버를 수신 하기 시작 하는 콘솔 응용 프로그램을 실행 하면 `http://localhost:9000`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-148">When you run the console application, the server starts listening to `http://localhost:9000`.</span></span> <span data-ttu-id="9f2b1-149">웹 브라우저에서이 주소로 이동 하는 경우에 "Hello world" 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-149">If you navigate to this address in a web browser, you will see the "Hello world" page.</span></span>

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a><span data-ttu-id="9f2b1-150">OWIN Diagnostics 추가</span><span class="sxs-lookup"><span data-stu-id="9f2b1-150">Add OWIN Diagnostics</span></span>

<span data-ttu-id="9f2b1-151">Microsoft.Owin.Diagnostics 패키지용 처리 되지 않은 예외를 catch 하는 HTML 페이지 오류 세부 정보를 표시 하는 미들웨어를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-151">The Microsoft.Owin.Diagnostics package contains middleware that catches unhandled exceptions and displays an HTML page with error details.</span></span> <span data-ttu-id="9f2b1-152">이 페이지 함수과 거의 동일한이 라고도 하는 ASP.NET 오류 페이지는 "[사망의 노란색 화면](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-152">This page functions much like the ASP.NET error page that is sometimes called the "[yellow screen of death](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD).</span></span> <span data-ttu-id="9f2b1-153">YSOD와 같은 개발 하는 동안 Katana 오류 페이지는 유용 하지만 프로덕션 모드에서 해제 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-153">Like the YSOD, the Katana error page is useful during development, but it's a good practice to disable it in production mode.</span></span>

<span data-ttu-id="9f2b1-154">프로젝트에서 진단 패키지를 설치 하려면 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-154">To install the Diagnostics package in your project, type the following command in the Package Manager Console window:</span></span>

`install-package Microsoft.Owin.Diagnostics –Pre`

<span data-ttu-id="9f2b1-155">코드를 변경 하면 `Startup1.Configuration` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-155">Change the code in your `Startup1.Configuration` method as follows:</span></span>

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

<span data-ttu-id="9f2b1-156">이제 Visual Studio 예외에서 중단 하지 않는다는 되도록 디버깅 하지 않고 응용 프로그램을 실행 하려면 CTRL + f 5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-156">Now use CTRL+F5 to run the application without debugging, so that Visual Studio will not break on the exception.</span></span> <span data-ttu-id="9f2b1-157">응용 프로그램 동일 하 게 작동 이전 처럼로 이동 될 때까지 `http://localhost/fail`, 이때 응용 프로그램에 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-157">The application behaves the same as before, until you navigate to `http://localhost/fail`, at which point the application throws the exception.</span></span> <span data-ttu-id="9f2b1-158">오류 페이지 미들웨어 되는 예외를 catch 하 고 HTML 페이지 오류에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-158">The error page middleware will catch the exception and display an HTML page with information about the error.</span></span> <span data-ttu-id="9f2b1-159">스택, 쿼리 문자열, 쿠키, 요청 헤더 및 OWIN 환경 변수를 참조 하려면 해당 탭을 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-159">You can click the tabs to see the stack, query string, cookies, request header, and OWIN environment variables.</span></span>

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a><span data-ttu-id="9f2b1-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f2b1-160">Next Steps</span></span>

- [<span data-ttu-id="9f2b1-161">OWIN 시작 클래스 검색</span><span class="sxs-lookup"><span data-stu-id="9f2b1-161">OWIN Startup Class Detection</span></span>](owin-startup-class-detection.md)
- [<span data-ttu-id="9f2b1-162">OWIN 자체 호스트 하는 ASP.NET Web API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9f2b1-162">Use OWIN to Self-Host ASP.NET Web API</span></span>](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [<span data-ttu-id="9f2b1-163">OWIN를 사용 하 여 자체 호스트 하는 SignalR</span><span class="sxs-lookup"><span data-stu-id="9f2b1-163">Use OWIN to Self-Host SignalR</span></span>](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
