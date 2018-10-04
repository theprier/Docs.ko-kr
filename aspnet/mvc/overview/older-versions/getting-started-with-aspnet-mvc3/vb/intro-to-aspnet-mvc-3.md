---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 (VB) 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: f596dbfb534a64169767fb77fb15ecc867466c74
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577186"
---
<a name="intro-to-aspnet-mvc-3-vb"></a><span data-ttu-id="818a8-103">ASP.NET MVC 3 (VB) 소개</span><span class="sxs-lookup"><span data-stu-id="818a8-103">Intro to ASP.NET MVC 3 (VB)</span></span>
====================
<span data-ttu-id="818a8-104">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="818a8-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="818a8-105">이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="818a8-106">시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="818a8-107">다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="818a8-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="818a8-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="818a8-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="818a8-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="818a8-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="818a8-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="818a8-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="818a8-112">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="818a8-113">VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="818a8-114">[VB.NET 버전](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="818a8-115">원하는 경우 C#으로 전환 합니다 [C# 버전](../cs/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-115">If you prefer C#, switch to the [C# version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="818a8-116">이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-116">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="818a8-117">시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-117">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="818a8-118">다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-118">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="818a8-119">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-119">Alternatively, you can individually install the prerequisites using the following links:</span></span>

- [<span data-ttu-id="818a8-120">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="818a8-120">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="818a8-121">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="818a8-121">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="818a8-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="818a8-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="818a8-123">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-123">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="818a8-124">VB 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-124">A Visual Web Developer project with VB source code is available to accompany this topic.</span></span> <span data-ttu-id="818a8-125">[VB 버전을 다운로드](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-125">[Download the VB version here](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span></span> <span data-ttu-id="818a8-126">CSharp 원한다 면으로 전환 합니다 [CSharp 버전](../cs/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-126">If you prefer CSharp, switch to the [CSharp version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="818a8-127">만들 내용</span><span class="sxs-lookup"><span data-stu-id="818a8-127">What You'll Build</span></span>

<span data-ttu-id="818a8-128">만들기, 편집 및 나열 하는 데이터베이스에서 동영상을 지 원하는 간단한 영화 목록 응용 프로그램을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-128">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="818a8-129">다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="818a8-130">데이터베이스에서 동영상 목록을 표시 하는 페이지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-130">It includes a page that displays a list of movies from a database:</span></span>

<span data-ttu-id="818a8-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="818a8-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span></span>

<span data-ttu-id="818a8-132">또한 응용 프로그램 추가, 편집 및 개별 문제에 대 한 참조 정보 뿐만 아니라 영화를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-132">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="818a8-133">데이터베이스에 저장 된 데이터가 올바른지 확인 하려면 유효성 검사를 포함 하는 모든 데이터 입력 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-133">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

<span data-ttu-id="818a8-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="818a8-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="818a8-135">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="818a8-135">Skills You'll Learn</span></span>

<span data-ttu-id="818a8-136">학습할 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-136">Here's what you'll learn:</span></span>

- <span data-ttu-id="818a8-137">새 ASP.NET MVC 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="818a8-137">How to create a new ASP.NET MVC project</span></span>
- <span data-ttu-id="818a8-138">Entity Framework 코드 중심을 사용 하 여 새 데이터베이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="818a8-138">How to create a new database using Entity Framework code-first</span></span>
- <span data-ttu-id="818a8-139">컨트롤러 및 보기에는 ASP.NET MVC를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="818a8-139">How to create ASP.NET MVC controllers and views</span></span>
- <span data-ttu-id="818a8-140">검색 데이터를 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="818a8-140">How to retrieve and display data</span></span>
- <span data-ttu-id="818a8-141">데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="818a8-141">How to edit data and enable data validation</span></span>

## <a name="getting-started"></a><span data-ttu-id="818a8-142">시작</span><span class="sxs-lookup"><span data-stu-id="818a8-142">Getting Started</span></span>

<span data-ttu-id="818a8-143">Visual Web Developer 2010 Express (줄여서 "VWD")를 실행 하 여 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-143">Start by running Visual Web Developer 2010 Express ("VWD" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="818a8-144">Visual Web Developer에는 IDE 또는 통합된 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-144">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="818a8-145">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-145">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="818a8-146">Visual Web Developer에서 사용할 수 있는 다양 한 옵션을 보여 주는 맨 위에 있는 도구 모음이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-146">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="818a8-147">IDE에서 작업을 수행 하는 또 다른 방법은 제공 하는 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-147">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="818a8-148">(예를 들어, 선택 하는 대신 **새 프로젝트** 에서 합니다 **시작** 페이지에서 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)</span><span class="sxs-lookup"><span data-stu-id="818a8-148">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="818a8-149">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="818a8-149">Creating Your First Application</span></span>

<span data-ttu-id="818a8-150">사용 하 여 Visual Basic 또는 Visual C# 프로그래밍 언어와 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-150">You can create applications using your choice of either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="818a8-151">이 자습서에서는 Visual Basic 왼쪽에서 선택한 다음 선택 **ASP.NET MVC 3 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-151">For this tutorial, select Visual Basic on the left, then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="818a8-152">"MvcMovie" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-152">Name your project "MvcMovie" and then click **OK**.</span></span>

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="818a8-154">에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-154">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="818a8-155">둡니다 **Razor** 기본 뷰 엔진으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-155">Leave **Razor** as the default view engine.</span></span>

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

<span data-ttu-id="818a8-157">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-157">Click **OK**.</span></span> <span data-ttu-id="818a8-158">있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Web Developer!</span><span class="sxs-lookup"><span data-stu-id="818a8-158">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="818a8-159">이는 간단한 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="818a8-159">This is a simple "Hello World!"</span></span> <span data-ttu-id="818a8-160">프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-160">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="818a8-161">**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-161">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image11.png)

<span data-ttu-id="818a8-162">디버깅을 시작 하려면 바로 가기 키 F5 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-162">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="818a8-163">F5 Visual Web Developer는 개발 웹 서버를 시작 하 고 웹 응용 프로그램을 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-163">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="818a8-164">그런 다음 VWD 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-164">VWD then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="818a8-165">브라우저의 주소 표시줄에 다음과 같은 알림이 `localhost` 등은 표시 되지 않습니다 및 `example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-165">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="818a8-166">있기 때문입니다 `localhost` 는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터는 항상 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-166">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="818a8-167">VWD 웹 프로젝트를 실행 하면 프로젝트에 대 한 임의의 포트가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-167">When VWD runs a web project, a random port is used for the project.</span></span> <span data-ttu-id="818a8-168">아래 이미지에서 임의 포트 번호가 43246입니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-168">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="818a8-169">프로젝트가 다른 포트 번호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-169">Your project will probably use a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image12.png)

<span data-ttu-id="818a8-170">기본적으로이 기본 템플릿은 있습니다 두 페이지를 방문 하 고 기본 로그인 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-170">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="818a8-171">보겠습니다이 응용 프로그램의 작동 방식을 변경할 조금 더 자세히 알아보고 ASP.NET MVC 진행에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-171">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="818a8-172">브라우저를 닫고 몇 가지 코드를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="818a8-172">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="818a8-173">다음</span><span class="sxs-lookup"><span data-stu-id="818a8-173">Next</span></span>](adding-a-controller.md)
