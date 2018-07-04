---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (C#) 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: d4cda748638a6396750fe2ef7713dd0b2a4555d6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379865"
---
<a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="9b0c9-103">ASP.NET MVC 3 (C#) 소개</span><span class="sxs-lookup"><span data-stu-id="9b0c9-103">Intro to ASP.NET MVC 3 (C#)</span></span>
====================
<span data-ttu-id="9b0c9-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="9b0c9-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="9b0c9-105">이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="9b0c9-106">보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="9b0c9-107">이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="9b0c9-108">시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="9b0c9-109">다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="9b0c9-110">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="9b0c9-111">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9b0c9-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="9b0c9-112">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="9b0c9-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="9b0c9-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="9b0c9-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="9b0c9-114">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="9b0c9-115">C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="9b0c9-116">[C# 버전 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="9b0c9-117">Visual Basic을 원한다 면으로 전환 합니다 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="9b0c9-118">만들 내용</span><span class="sxs-lookup"><span data-stu-id="9b0c9-118">What You'll Build</span></span>

<span data-ttu-id="9b0c9-119">만들기, 편집 및 나열 하는 데이터베이스에서 동영상을 지 원하는 간단한 영화 목록 응용 프로그램을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="9b0c9-120">다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="9b0c9-121">데이터베이스에서 동영상 목록을 표시 하는 페이지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="9b0c9-123">또한 응용 프로그램 추가, 편집 및 개별 문제에 대 한 참조 정보 뿐만 아니라 영화를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="9b0c9-124">데이터베이스에 저장 된 데이터가 올바른지 확인 하려면 유효성 검사를 포함 하는 모든 데이터 입력 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="9b0c9-125">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="9b0c9-125">Skills You'll Learn</span></span>

<span data-ttu-id="9b0c9-126">학습할 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="9b0c9-127">새 ASP.NET MVC 프로젝트를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="9b0c9-128">컨트롤러 및 보기에는 ASP.NET MVC를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="9b0c9-129">Entity Framework Code First 패러다임을 사용 하 여 새 데이터베이스를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="9b0c9-130">검색 데이터를 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="9b0c9-131">데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9b0c9-132">시작</span><span class="sxs-lookup"><span data-stu-id="9b0c9-132">Getting Started</span></span>

<span data-ttu-id="9b0c9-133">Visual Web Developer 2010 Express ("Visual Web Developer" 줄여서)를 실행 하 여 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="9b0c9-134">Visual Web Developer에는 IDE 또는 통합된 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="9b0c9-135">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="9b0c9-136">Visual Web Developer에서 사용할 수 있는 다양 한 옵션을 보여 주는 맨 위에 있는 도구 모음이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="9b0c9-137">IDE에서 작업을 수행 하는 또 다른 방법은 제공 하는 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="9b0c9-138">(예를 들어, 선택 하는 대신 **새 프로젝트** 에서 합니다 **시작** 페이지에서 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)</span><span class="sxs-lookup"><span data-stu-id="9b0c9-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="9b0c9-139">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="9b0c9-139">Creating Your First Application</span></span>

<span data-ttu-id="9b0c9-140">Visual Basic 또는 Visual C# 프로그래밍 언어로 사용 하 여 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="9b0c9-141">왼쪽의 Visual C#을 선택 하 고 선택한 **ASP.NET MVC 3 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="9b0c9-142">"MvcMovie" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="9b0c9-143">(Visual Basic을 원한다 면으로 전환 합니다 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의.)</span><span class="sxs-lookup"><span data-stu-id="9b0c9-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="9b0c9-144">에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="9b0c9-145">확인할 **태그를 사용 하 여 HTML5** 두고 **Razor** 기본 뷰 엔진으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="9b0c9-146">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-146">Click **OK**.</span></span> <span data-ttu-id="9b0c9-147">있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Web Developer!</span><span class="sxs-lookup"><span data-stu-id="9b0c9-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="9b0c9-148">이는 간단한 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="9b0c9-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="9b0c9-149">프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="9b0c9-150">**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="9b0c9-151">디버깅을 시작 하려면 바로 가기 키 F5 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="9b0c9-152">F5 Visual Web Developer는 개발 웹 서버를 시작 하 고 웹 응용 프로그램을 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="9b0c9-153">그런 다음 visual Web Developer는 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="9b0c9-154">브라우저의 주소 표시줄에 다음과 같은 알림이 `localhost` 등은 표시 되지 않습니다 및 `example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="9b0c9-155">있기 때문입니다 `localhost` 는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터는 항상 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="9b0c9-156">Visual Web Developer에서 웹 프로젝트를 실행 하면 임의 포트를 웹 서버에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="9b0c9-157">아래 이미지에서 임의 포트 번호가 43246입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="9b0c9-158">응용 프로그램을 실행 하는 경우 아마도 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="9b0c9-159">즉시이 기본 템플릿을 사용 하면 두 페이지를 방문 하 고 기본 로그인 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="9b0c9-160">다음 단계는이 응용 프로그램의 작동 방식을 변경할 좀 더 자세히 알아보고 ASP.NET MVC 진행에서 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="9b0c9-161">브라우저를 닫고 몇 가지 코드를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0c9-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9b0c9-162">다음</span><span class="sxs-lookup"><span data-stu-id="9b0c9-162">Next</span></span>](adding-a-controller.md)
