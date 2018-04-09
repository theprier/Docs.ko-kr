---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 2ba1b73f40a920e27e4a03d9f703e62054d3f25c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="5d60f-104">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="5d60f-104">Accessing your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="5d60f-105">으로 [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="5d60f-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="5d60f-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="5d60f-107">읽기 및 쓰기는 데이터베이스에서 단순 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="5d60f-108">방문는 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 예제에는 다른 ASP.NET MVC를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="5d60f-109">이 섹션에서는 하겠습니다를 새 MoviesController 클래스를 만들고 동영상 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 다시 표시 하는 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="5d60f-110">Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 MoviesController를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="5d60f-111">[![컨트롤러 추가](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5d60f-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="5d60f-112">이 프로젝트 내에서 우리의 \Controllers 폴더 아래 새 "MoviesController.cs" 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="5d60f-113">새로 지정된 된 데이터베이스에서 영화 목록을 검색 하려면 MovieController 보겠습니다 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="5d60f-114">우리는 영화 1984 년 여름에 해제만 검색 되도록 LINQ 쿼리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="5d60f-115">이 목록을 영화 다시 렌더링, 하므로 메서드를 마우스 오른쪽 단추로 클릭 하 고 만들 추가 보기를 선택 하는 보기 템플릿이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="5d60f-116">뷰 추가 대화 상자에서는 합니다 나타낼 목록을 전달 하는 것&lt;Movies.Models.Movie&gt; 우리의 보기 서식 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="5d60f-117">달리 뷰 추가 대화 상자를 사용 하 고 "Empty"는 서식 파일을 만들도록 선택한 이전 시간을 나타낼 수이 이번 주시기 바랍니다 Visual Studio를 자동으로 "스 캐 폴드" 템플릿 보기 위해 몇 가지 기본 콘텐츠로.</span><span class="sxs-lookup"><span data-stu-id="5d60f-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="5d60f-118">"보기 콘텐츠 드롭다운 메뉴 내에서"List"항목을 선택 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="5d60f-119">포함을 만든 새 클래스 추가 보기 대화 상자 표시 하기 위해 응용 프로그램을 컴파일하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![뷰 추가](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="5d60f-121">추가 클릭 시스템은 자동으로 코드를 생성 보기에 대 한 동영상 목록을 표시 하는 데에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="5d60f-122">이 값은 좋은 변경 하는 &lt;h2&gt; Hello World 보기와 이전에 수행한 것 처럼 "My 영화 목록"와 같은 값으로 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="5d60f-123">[![동영상-Microsoft Visual Developer 2010 Express를 웹](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5d60f-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="5d60f-124">ְ ְ ¿כ 주소 표시줄에 /Movies를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="5d60f-125">이제 고 했으므로 이러한 내용을 컨트롤러 내에 기본 쿼리를 사용 하 여 데이터베이스에서 데이터를 검색 동영상에서 인식 하는 보기에 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="5d60f-126">해당 보기 다음 동영상 목록을 통해 회전 하 고 us에 대 한 데이터 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="5d60f-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="5d60f-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="5d60f-128">म 않습니다 수 구현-이 응용 프로그램으로 편집, 세부 정보 및 삭제 기능을 수행해 줍니다 스 캐 폴드 템플릿이 생성 하는 기본 링크 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="5d60f-129">/Movies/Index.aspx 파일을 열고 해당 구성 요소 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="5d60f-130">이 업데이트 된 보기 템플릿 어 떠 해야 이러한 변경을 수행 되 면에 대 한 소스 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="5d60f-131">필요 하지 않습니다, 링크 만드는 되므로이 예에 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="5d60f-132">하지만 다음 그대로 우리의 새로 만들기 링크를 유지할 됩니다 있습니다!</span><span class="sxs-lookup"><span data-stu-id="5d60f-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="5d60f-133">해당 열이 제거 포함 앱 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="5d60f-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="5d60f-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="5d60f-135">동영상 데이터의 간단한 목록을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="5d60f-136">그러나 "새로 만들기" 링크를 클릭 하면 살펴보겠습니다 오류가 대로 연결 되지 않았습니다!</span><span class="sxs-lookup"><span data-stu-id="5d60f-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="5d60f-137">만들기 동작 메서드를 구현 하 고 사용자가 데이터베이스에 새 동영상을 입력할 수 있도록 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d60f-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5d60f-138">[이전](getting-started-with-mvc-part4.md)
> [다음](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="5d60f-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
