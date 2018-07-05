---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 소개 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: 408256d116a7e73e01c34b0a11881e14c5b8401d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385734"
---
<a name="intro-to-aspnet-mvc"></a><span data-ttu-id="55830-104">ASP.NET MVC 소개</span><span class="sxs-lookup"><span data-stu-id="55830-104">Intro to ASP.NET MVC</span></span>
====================
<span data-ttu-id="55830-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="55830-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="55830-106">이 자습서는 사용할 수 있는 경우 업데이트 된 버전 [같습니다](../../getting-started/introduction/getting-started.md) 사용 하 여 [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads).</span></span> <span data-ttu-id="55830-107">새 자습서에는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
> 
> 
> <span data-ttu-id="55830-108">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55830-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="55830-109">읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="55830-110">방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55830-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="55830-111">사용 하 여 첫 ASP.NET MVC 웹 응용 프로그램을 만들어 보겠습니다 [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="55830-112">보겠습니다 만들고 영화를 나열 하는 간단한 영화 목록 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="55830-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="55830-113">만들 내용</span><span class="sxs-lookup"><span data-stu-id="55830-113">What You'll Build</span></span>

<span data-ttu-id="55830-114">다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="55830-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="55830-115">다양 한 열을 사용 하 여 동영상의 간단한 테이블을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="55830-116">[![영화 목록-Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="55830-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="55830-117">및 영화 목록에 추가할 수 있도록 만드는 폼을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="55830-118">[![동영상-Windows Internet Explorer (2) 만들기](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="55830-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="55830-119">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="55830-119">Skills You'll Learn</span></span>

<span data-ttu-id="55830-120">이 자습서는 Visual Studio를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="55830-121">알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="55830-121">You'll learn:</span></span>

- <span data-ttu-id="55830-122">새 ASP.NET MVC 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="55830-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="55830-123">SQL Server를 사용 하 여 새 데이터베이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="55830-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="55830-124">ASP.NET MVC 컨트롤러 및 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="55830-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="55830-125">검색 데이터를 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="55830-125">How to retrieve and display data</span></span>
- <span data-ttu-id="55830-126">데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="55830-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="55830-127">데이터베이스 스키마를 업데이트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="55830-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="55830-128">시작</span><span class="sxs-lookup"><span data-stu-id="55830-128">Get Started</span></span>

<span data-ttu-id="55830-129">시작 화면에서 Visual Web Developer 2010 Express (부르겠습니다 "VWD" 지금부터) 선택한 새 프로젝트를 실행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="55830-130">Visual Web Developer에는 IDE 또는 통합 개발자 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="55830-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="55830-131">Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 IDE를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="55830-132">파일 선택를 사용할 수도 있습니다 메뉴 뿐만 아니라, 사용 가능한 여러 옵션을 보여 주는 위에 도구 모음 | 새 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="55830-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="55830-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="55830-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="55830-134">응용 프로그램 처음 만들기</span><span class="sxs-lookup"><span data-stu-id="55830-134">Creating Your First Application</span></span>

<span data-ttu-id="55830-135">Visual Basic 또는 Visual C#을 사용 하 여 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55830-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="55830-136">이제 선택 Visual C# 왼쪽에서 선택 "ASP.NET MVC 2 웹 응용 프로그램입니다."</span><span class="sxs-lookup"><span data-stu-id="55830-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="55830-137">프로젝트 "Movies" 이름을 지정 하 고 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="55830-138">[![새 프로젝트](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="55830-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="55830-139">오른쪽에 응용 프로그램에서 모든 파일 및 폴더를 보여 주는 솔루션 탐색기.</span><span class="sxs-lookup"><span data-stu-id="55830-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="55830-140">중간에 큰 기간은 코드를 편집 하 고 대부분의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="55830-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="55830-141">있다면 응용 프로그램을 사용 지금은 아무 작업도 수행 하지 않고 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하는 visual Studio!</span><span class="sxs-lookup"><span data-stu-id="55830-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="55830-142">이 간단한 "Hello World!</span><span class="sxs-lookup"><span data-stu-id="55830-142">This is a simple "Hello World!</span></span> <span data-ttu-id="55830-143">프로젝트 되며 응용 프로그램을 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55830-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="55830-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="55830-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="55830-145">도구 모음에 "재생" 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-145">Select the "play" button to the toolbar.</span></span>

![디버깅 시작](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="55830-147">프로그램을 컴파일하고 웹 브라우저에서 응용 프로그램을 시작 하는 오른쪽을 가리키는 녹색 화살표는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55830-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="55830-148">*참고: 있습니다 수 대신 키보드에서 f5 키를 누르거나 디버그-&gt;"디버그" 메뉴에서 디버깅 시작 합니다.*</span><span class="sxs-lookup"><span data-stu-id="55830-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="55830-149">이렇게 하면 Visual Web Developer는 개발 웹 서버를 시작 하 고 (구성 또는이 기능을 사용 하는 데 필요한 수동 단계 없는 함) 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="55830-150">그런 다음 브라우저를 시작 하 고 응용 프로그램의 홈 페이지로 이동 하도록 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="55830-151">아래는 브라우저의 주소 표시줄 코드는 "localhost" example.com 같이 하지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="55830-152">Localhost는 방금 빌드한 응용 프로그램을 실행 하는 경우에 자신의 로컬 컴퓨터-항상 가리키는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="55830-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="55830-153">[![홈 페이지](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="55830-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="55830-154">기본적으로이 기본 템플릿은 있습니다 두 페이지를 방문 하 고 기본 로그인 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="55830-155">보겠습니다이 응용 프로그램의 작동 방식을 변경할 조금 더 자세히 알아보고 ASP.NET MVC 진행에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="55830-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="55830-156">브라우저를 닫고 몇 가지 코드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55830-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="55830-157">다음</span><span class="sxs-lookup"><span data-stu-id="55830-157">Next</span></span>](getting-started-with-mvc-part2.md)
