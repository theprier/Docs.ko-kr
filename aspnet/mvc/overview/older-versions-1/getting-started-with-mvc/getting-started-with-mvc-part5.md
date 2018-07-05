---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 읽기 및 쓰기 데이터베이스에서 간단한 웹 응용 프로그램을 만듭니다.
ms.author: aspnetcontent
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 556eed77cbd9e81c0a2a1334bb0a8ee56abafd34
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815008"
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="d32d5-104">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="d32d5-104">Accessing your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="d32d5-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="d32d5-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="d32d5-106">ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="d32d5-107">읽기 및 쓰기 데이터베이스는 간단한 웹 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="d32d5-108">방문 합니다 [ASP.NET MVC 학습 센터](../../../index.md) 자습서 및 샘플 다른 ASP.NET MVC를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>


<span data-ttu-id="d32d5-109">이 섹션에서는 하겠습니다 새 MoviesController 클래스를 만들고 영화 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 다시 표시 하는 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="d32d5-110">컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 MoviesController를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="d32d5-111">[![컨트롤러 추가](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d32d5-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="d32d5-112">이 프로젝트 내에서 우리의 \Controllers 폴더 아래에 있는 새 "MoviesController.cs" 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="d32d5-113">영화 목록에 새로 채워진된 데이터베이스에서 검색할 MovieController 업데이트 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="d32d5-114">우리는 1984 년 여름부터 이후 출시 된 영화만 검색 되도록 LINQ 쿼리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="d32d5-115">보기 템플릿을이 목록을 다시 영화 렌더링, 따라서 메서드에서 마우스 오른쪽 단추로 클릭 하 고 만들려면 추가 보기를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="d32d5-116">뷰 추가 대화 상자 내 나타냅니다 목록을 전달 하는 것&lt;Movies.Models.Movie&gt; 보기 템플릿은 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="d32d5-117">뷰 추가 대화 상자를 사용 하 고 "Empty" 템플릿을 작성 하기로 했습니다. 이전 시간을 달리이 이번에는 나타냅니다 하려고 자동으로 "스 캐 폴딩" 보기 템플릿을 한 일부 기본 콘텐츠를 사용 하 여 Visual Studio 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="d32d5-118">"보기 콘텐츠 드롭다운 메뉴에서"List"항목을 선택 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="d32d5-119">포함을 만든 경우 새 클래스 추가 보기 대화 상자에서 표시 하기 위해 응용 프로그램을 컴파일하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![뷰 추가](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="d32d5-121">클릭 추가 하 고 자동으로 생성 됩니다 코드를 보려면 동영상 목록을 표시 하는 우리 회사에.</span><span class="sxs-lookup"><span data-stu-id="d32d5-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="d32d5-122">이 변경할 수 있는 좋은 기회를 &lt;h2&gt; Hello World 뷰를 사용 하 여 이전에 수행한 것과 같이 "내 Movie List" 같이 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="d32d5-123">[![동영상-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="d32d5-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="d32d5-124">응용 프로그램을 실행 하 고 주소 표시줄에 /Movies를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="d32d5-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="d32d5-125">이제 했습니다 컨트롤러 내에서 기본 쿼리를 사용 하 여 데이터베이스에서 데이터를 검색 하 고 영화에 대 한 알고 있는 뷰로 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="d32d5-126">해당 보기 다음 동영상 목록을 통해 회전 하 고 우리 회사에 데이터 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="d32d5-127">[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="d32d5-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="d32d5-128">에서는 되므로 스 캐 폴드 템플릿을 생성 하는 기본 링크를 필요가 없습니다이 응용 프로그램을 사용 하 여 편집, 세부 정보 및 삭제 기능을 구현 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="d32d5-129">/Movies/Index.aspx 파일을 열고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="d32d5-130">보기 템플릿은 업데이트 된 모양을 만들면 이러한 변경에 대 한 소스 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="d32d5-131">에서는 필요가 있는 링크를 만들 되므로 예를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="d32d5-132">그러나 다음으로 새로 만들기 링크를 유지 됩니다!</span><span class="sxs-lookup"><span data-stu-id="d32d5-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="d32d5-133">해당 열이 제거 포함 된 앱 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="d32d5-134">[![영화 목록-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="d32d5-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="d32d5-135">이제 영화 데이터의 단순 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="d32d5-136">그러나 "새로 만들기" 링크를 클릭는 연결 되지 않았습니다으로 오류가 표시 됩니다 것!</span><span class="sxs-lookup"><span data-stu-id="d32d5-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="d32d5-137">만들기 동작 메서드를 구현 하 고 사용자가 데이터베이스에 새 영화를 입력할 수 있도록 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d32d5-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d32d5-138">[이전](getting-started-with-mvc-part4.md)
> [다음](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="d32d5-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
