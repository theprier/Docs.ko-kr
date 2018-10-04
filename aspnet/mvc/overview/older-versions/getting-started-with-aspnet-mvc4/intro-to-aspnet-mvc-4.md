---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 여기 Visual Studio 2013을 사용 하 여 사용할 경우 업데이트 된 버전입니다. 새 자습서 t를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 하는 중...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 62f67d0d0dfe7a3c9d04eacfbcac56f7fd03ef07
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577368"
---
<a name="intro-to-aspnet-mvc-4"></a><span data-ttu-id="5fea6-104">ASP.NET MVC 4 소개</span><span class="sxs-lookup"><span data-stu-id="5fea6-104">Intro to ASP.NET MVC 4</span></span>
====================
<span data-ttu-id="5fea6-105">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="5fea6-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="5fea6-106">이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="5fea6-107">새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
> 
> <span data-ttu-id="5fea6-108">이 자습서는 Microsoft를 사용 하 여 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 기본 사항 설명 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual Web Developer 2010 Express 서비스 팩 1입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-108">This tutorial will teach you the basics of building an ASP.NET MVC 4 Web application using Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1.</span></span> <span data-ttu-id="5fea6-109">자습서를 완료 하려면 어떤 항목도 설치 하지 않아도 됩니다. visual Studio 2012 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-109">Visual Studio 2012 is recommended, you won't need to install anything to complete the tutorial.</span></span> <span data-ttu-id="5fea6-110">Visual Studio 2010을 사용 하는 경우 아래 구성 요소를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-110">If you are using Visual Studio 2010 you must install the components below.</span></span> <span data-ttu-id="5fea6-111">다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-111">You can install all of them by clicking the following links:</span></span>
> 
> - [<span data-ttu-id="5fea6-112">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5fea6-112">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="5fea6-113">ASP.NET MVC 4 용 WPI 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="5fea6-113">WPI installer for ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [<span data-ttu-id="5fea6-114">LocalDB</span><span class="sxs-lookup"><span data-stu-id="5fea6-114">LocalDB</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [<span data-ttu-id="5fea6-115">SSDT</span><span class="sxs-lookup"><span data-stu-id="5fea6-115">SSDT</span></span>](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
> 
> <span data-ttu-id="5fea6-116">Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 설치 합니다 [ASP.NET MVC 4에 대 한 설치 관리자 WPI](https://go.microsoft.com/fwlink/?LinkId=243392) 및: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span><span class="sxs-lookup"><span data-stu-id="5fea6-116">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the [WPI installer for ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392) and the: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span></span>
> 
> <span data-ttu-id="5fea6-117">C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-117">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="5fea6-118">[C# 버전 다운로드](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-118">[Download the C# version](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip).</span></span>
> 
> <span data-ttu-id="5fea6-119">이 자습서에서 Visual Studio에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-119">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="5fea6-120">또한 가능 응용 프로그램 사용 가능한 인터넷을 통해 호스팅 공급자에 배포 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-120">You can also make the application available over the Internet by deploying it to a hosting provider.</span></span> <span data-ttu-id="5fea6-121">Microsoft에서 제공 하는 무료 웹 호스팅에 최대 10 개의 웹 사이트를 [Windows Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-121">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="5fea6-122">Visual Studio 웹 프로젝트를 Windows Azure 웹 사이트를 배포 하는 방법에 대 한 정보를 참조 하세요 [만들기 및 ASP.NET 웹 사이트 및 Visual Studio를 사용 하 여 SQL Database를 배포](https://docs.microsoft.com/dotnet/azure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-122">For information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create and deploy an ASP.NET web site and SQL Database with Visual Studio](https://docs.microsoft.com/dotnet/azure/).</span></span> <span data-ttu-id="5fea6-123">이 자습서에는 Windows Azure SQL Database (이전의 SQL Azure)에 SQL Server 데이터베이스를 배포 하려면 Entity Framework Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-123">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Windows Azure SQL Database (formerly SQL Azure).</span></span>
> 
> <span data-ttu-id="5fea6-124">Rick anderson이 자습서가 작성 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="5fea6-124">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="5fea6-125">만들 내용</span><span class="sxs-lookup"><span data-stu-id="5fea6-125">What You'll Build</span></span>

> [!NOTE]
> <span data-ttu-id="5fea6-126">이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-126">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="5fea6-127">새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-127">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>


<span data-ttu-id="5fea6-128">만들기, 편집, 검색 및 나열 하는 데이터베이스에서 동영상을 지 원하는 간단한 영화 목록 응용 프로그램을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-128">You'll implement a simple movie-listing application that supports creating, editing, searching and listing movies from a database.</span></span> <span data-ttu-id="5fea6-129">다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="5fea6-130">데이터베이스에서 동영상 목록을 표시 하는 페이지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-130">It includes a page that displays a list of movies from a database:</span></span>

![](intro-to-aspnet-mvc-4/_static/image1.png)

<span data-ttu-id="5fea6-131">또한 응용 프로그램 추가, 편집 및 개별 문제에 대 한 참조 정보 뿐만 아니라 영화를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-131">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="5fea6-132">데이터베이스에 저장 된 데이터가 올바른지 확인 하려면 유효성 검사를 포함 하는 모든 데이터 입력 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-132">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a><span data-ttu-id="5fea6-133">시작</span><span class="sxs-lookup"><span data-stu-id="5fea6-133">Getting Started</span></span>

<span data-ttu-id="5fea6-134">Visual Studio Express 2012 또는 Visual Web Developer 2010 Express를 실행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-134">Start by running Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="5fea6-135">이 시리즈에서는 Visual Studio Express 2012, 에서만 스크린 샷 대부분 Visual Studio 2010 SP1, Visual Studio 2012, Visual Studio Express 2012 또는 Visual Web Developer 2010 Express를 사용 하 여이 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-135">Most of the screen shots in this series use Visual Studio Express 2012, but you can complete this tutorial with Visual Studio 2010/SP1, Visual Studio 2012, Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="5fea6-136">선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-136">Select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="5fea6-137">Visual Studio IDE 또는 통합된 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-137">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="5fea6-138">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-138">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="5fea6-139">Visual Studio에서 사용할 수 있는 다양 한 옵션을 보여 주는 맨 위에 있는 도구 모음이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-139">In Visual Studio there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="5fea6-140">IDE에서 작업을 수행 하는 또 다른 방법은 제공 하는 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-140">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="5fea6-141">(예를 들어, 선택 하는 대신 **새 프로젝트** 에서 합니다 **시작** 페이지에서 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)</span><span class="sxs-lookup"><span data-stu-id="5fea6-141">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="5fea6-142">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="5fea6-142">Creating Your First Application</span></span>

<span data-ttu-id="5fea6-143">Visual Basic 또는 Visual C# 프로그래밍 언어로 사용 하 여 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-143">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="5fea6-144">왼쪽의 Visual C#을 선택 하 고 선택한 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-144">Select Visual C# on the left and then select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="5fea6-145">프로젝트 이름을 &quot;MvcMovie&quot; 을 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-145">Name your project &quot;MvcMovie&quot; and then click **OK**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image4.png)

<span data-ttu-id="5fea6-146">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-146">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="5fea6-147">둡니다 **Razor** 기본 뷰 엔진으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-147">Leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-4/_static/image5.png)

<span data-ttu-id="5fea6-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-148">Click **OK**.</span></span> <span data-ttu-id="5fea6-149">있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Studio!</span><span class="sxs-lookup"><span data-stu-id="5fea6-149">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="5fea6-150">이 간단한 &quot;Hello World!&quot; 프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-150">This is a simple &quot;Hello World!&quot; project, and it's a good place to start your application.</span></span>

![](intro-to-aspnet-mvc-4/_static/image6.png)

<span data-ttu-id="5fea6-151">**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-151">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image7.png)

<span data-ttu-id="5fea6-152">디버깅을 시작 하려면 바로 가기 키 F5 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-152">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="5fea6-153">F5 Visual Studio IIS Express를 시작 하 고 웹 응용 프로그램을 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-153">F5 causes Visual Studio to start IIS Express and run your web application.</span></span> <span data-ttu-id="5fea6-154">그런 다음 visual Studio가 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-154">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="5fea6-155">브라우저의 주소 표시줄에 다음과 같은 알림이 `localhost` 등은 표시 되지 않습니다 및 `example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-155">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="5fea6-156">있기 때문입니다 `localhost` 는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터는 항상 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-156">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="5fea6-157">Visual Studio 웹 프로젝트를 실행할 때 임의 포트를 웹 서버에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-157">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="5fea6-158">아래 이미지에서 포트 번호가 41788입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-158">In the image below, the port number is 41788.</span></span> <span data-ttu-id="5fea6-159">응용 프로그램을 실행 하는 경우 아마도 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-159">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-4/_static/image8.png)

<span data-ttu-id="5fea6-160">즉시이 기본 템플릿을 사용 하면 집, 연락처 및에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-160">Right out of the box this default template gives you Home, Contact and About pages.</span></span> <span data-ttu-id="5fea6-161">또한 등록 및 로그인에 대 한 지원을 제공 하 고 Facebook 및 Twitter에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-161">It also provides support to register and log in, and links to Facebook and Twitter.</span></span> <span data-ttu-id="5fea6-162">다음 단계는이 응용 프로그램의 작동 방식을 변경할 좀 더 자세히 알아보고 ASP.NET MVC 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-162">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="5fea6-163">브라우저를 닫고 몇 가지 코드를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5fea6-163">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5fea6-164">다음</span><span class="sxs-lookup"><span data-stu-id="5fea6-164">Next</span></span>](adding-a-controller.md)
