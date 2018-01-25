---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: "컨트롤러 (VB)에서 모델의 데이터에 액세스 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f1a1db907aa1d0a62af9b363fabfc74ac11acc68
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="accessing-your-models-data-from-a-controller-vb"></a><span data-ttu-id="2c776-103">컨트롤러 (VB)에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="2c776-103">Accessing your Model's Data from a Controller (VB)</span></span>
====================
<span data-ttu-id="2c776-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="2c776-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="2c776-105">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="2c776-106">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="2c776-107">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="2c776-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="2c776-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="2c776-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="2c776-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="2c776-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="2c776-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="2c776-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="2c776-112">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="2c776-113">이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="2c776-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="2c776-114">[VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="2c776-115">원하는 경우 C#으로 전환 된 [C# 버전](../cs/accessing-your-models-data-from-a-controller.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-115">If you prefer C#, switch to the [C# version](../cs/accessing-your-models-data-from-a-controller.md) of this tutorial.</span></span>


<span data-ttu-id="2c776-116">이 섹션에서는 새 만들어 `MoviesController` 클래스 및 동영상 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-116">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="2c776-117">계속 하기 전에 응용 프로그램을 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-117">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="2c776-118">마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더를 만들고 새 `MoviesController` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-118">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="2c776-119">다음 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-119">Select the following options:</span></span>

- <span data-ttu-id="2c776-120">컨트롤러 이름: **MoviesController**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-120">Controller name: **MoviesController**.</span></span> <span data-ttu-id="2c776-121">(기본값입니다.)</span><span class="sxs-lookup"><span data-stu-id="2c776-121">(This is the default.)</span></span>
- <span data-ttu-id="2c776-122">서식 파일: **Entity Framework를 사용 하 여 읽기/쓰기 동작 및 뷰를 사용 하 여 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-122">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="2c776-123">모델 클래스: **동영상 (MvcMovie.Models)**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-123">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="2c776-124">데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie.Models)**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-124">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="2c776-125">보기: **Razor (CSHTML)**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-125">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="2c776-126">(기본값입니다.)</span><span class="sxs-lookup"><span data-stu-id="2c776-126">(The default.)</span></span>

<span data-ttu-id="2c776-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="2c776-128">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-128">Click **Add**.</span></span> <span data-ttu-id="2c776-129">Visual Web Developer는 다음과 같은 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-129">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="2c776-130">*MoviesController.vb* 프로젝트의 파일 *컨트롤러* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-130">*A MoviesController.vb* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="2c776-131">A *동영상* 프로젝트의 폴더 *뷰* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-131">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="2c776-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, 및 *Index.vbhtml* 새 *Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, and *Index.vbhtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="2c776-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="2c776-134">ASP.NET MVC 3 스 캐 폴딩 메커니즘 자동으로 생성 됩니다는 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드 및 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-134">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="2c776-135">만들기, 목록, 편집 및 동영상 항목을 삭제할 수 있는 완벽 하 게 작동 하는 웹 응용 프로그램을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-135">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="2c776-136">응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에 URL을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-136">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="2c776-137">응용 프로그램은 기본 라우팅에 의존 하므로 때문에 (에 정의 된는 *Global.asax* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값에 라우팅 된다고 `Index` 의 동작 메서드는 `Movies` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-137">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="2c776-138">즉, 브라우저 요청 `http://localhost:xxxxx/Movies` 브라우저 요청 동일은 사실상 `http://localhost:xxxxx/Movies/Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-138">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="2c776-139">결과 아직 추가 하지 때문에 빈 목록 영화,입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-139">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a><span data-ttu-id="2c776-140">동영상 만들기</span><span class="sxs-lookup"><span data-stu-id="2c776-140">Creating a Movie</span></span>

<span data-ttu-id="2c776-141">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-141">Select the **Create New** link.</span></span> <span data-ttu-id="2c776-142">동영상에 대 한 일부 세부 정보를 입력 한 다음 클릭는 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-142">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="2c776-143">클릭 하 고 **만들기** 단추를 클릭 하면 데이터베이스에 동영상 정보 저장 되는 서버에 게시 될 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-143">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="2c776-144">다음 리디렉션됩니다 하는 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-144">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="2c776-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="2c776-146">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-146">Create a couple more movie entries.</span></span> <span data-ttu-id="2c776-147">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-147">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="2c776-148">생성된 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="2c776-148">Examining the Generated Code</span></span>

<span data-ttu-id="2c776-149">열기는 *Controllers\MoviesController.vb* 파일을 생성 된 검사 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2c776-149">Open the *Controllers\MoviesController.vb* file and examine the generated `Index` method.</span></span> <span data-ttu-id="2c776-150">영화 컨트롤러와의 일부는 `Index` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-150">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

<span data-ttu-id="2c776-151">다음 줄은 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-151">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="2c776-152">쿼리, 편집 및 삭제 영화를 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-152">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

<span data-ttu-id="2c776-153">요청을는 `Movies` 컨트롤러의 모든 항목이 반환는 `Movies` 영화 데이터베이스 테이블의 다음 결과를 전달는 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="2c776-153">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="2c776-154">강력한 형식 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="2c776-154">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="2c776-155">이 자습서의 앞부분에서 언급 했 듯이 어떻게 컨트롤러를 전달할 수 데이터 나 개체를 사용 하 여 뷰 서식 파일은 `ViewBag` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-155">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="2c776-156">`ViewBag` 정보 보기를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-156">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="2c776-157">또한 ASP.NET MVC는 강력 하 게 전달 하는 기능 입력 한 데이터 또는 개체 템플릿 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-157">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="2c776-158">이 접근 방식을 사용 하면 더 나은 컴파일 타임 검사 코드 및 Visual Web Developer 편집기에서 다양 한 IntelliSense의 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-158">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="2c776-159">이 방법을 사용 하 여는 `MoviesController` 클래스 및 *Index.vbhtml* 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="2c776-159">We're using this approach with the `MoviesController` class and *Index.vbhtml* view template.</span></span>

<span data-ttu-id="2c776-160">코드 만드는 방법을 확인할 수는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출 되 면 개체는 `View` 의 도우미 메서드는 `Index` 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="2c776-160">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="2c776-161">그런 다음이 `Movies` 보기에는 컨트롤러에서 목록:</span><span class="sxs-lookup"><span data-stu-id="2c776-161">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

<span data-ttu-id="2c776-162">포함 하 여 한 `@ModelType` 문을 보기 템플릿 파일 맨 위에 있는 보기를 필요로 하는 개체의 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-162">By including a `@ModelType` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="2c776-163">다음에 Visual Web Developer 영화 컨트롤러를 만들 때 자동으로 포함 `@model` 맨 위에 있는 문에 *Index.vbhtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="2c776-163">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.vbhtml* file:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

<span data-ttu-id="2c776-164">이 `@ModelType` 지시문을 사용 하면 컨트롤러 사용 하 여 보기에 전달 되는 동영상 목록을 액세스할 수 있습니다는 `Model` 강력한 형식 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-164">This `@ModelType` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="2c776-165">예를 들어는 *Index.vbhtml* 서식 파일을 코드 반복 동영상 수행 하 여 한 `foreach` 문을 통해 강력한 형식의 `Model` 개체:</span><span class="sxs-lookup"><span data-stu-id="2c776-165">For example, in the *Index.vbhtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

<span data-ttu-id="2c776-166">때문에 `Model` 개체는 강력한 형식 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에서 개체도 입력 된 `Movie`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-166">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="2c776-167">여러 가지 이점을 얻을이 의미 가져오기 코드의 컴파일 타임 검사 하 고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-167">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="2c776-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="2c776-169">SQL Server Compact 작업</span><span class="sxs-lookup"><span data-stu-id="2c776-169">Working with SQL Server Compact</span></span>

<span data-ttu-id="2c776-170">제공 된 데이터베이스 연결 문자열이 가리키는 entity Framework Code First 감지는 `Movies` 데이터베이스 코드 첫 번째 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-170">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="2c776-171">검색 하 여 생성 되어 있는지 확인할 수 있습니다는 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-171">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="2c776-172">표시 되지 않으면는 *Movies.sdf* 파일을 클릭는 **모든 파일 표시** 단추는 **솔루션 탐색기** 도구 모음에서 클릭 된 **새로 고침** 단추를 선택한 다음 확장은 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-172">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="2c776-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="2c776-174">두 번 클릭 *Movies.sdf* 열려는 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-174">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="2c776-175">다음 확장은 **테이블** 데이터베이스에서 생성 된 테이블을 표시 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-175">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="2c776-176">두 번 클릭 하면 오류가 발생 하는 경우 *Movies.sdf*, 이전에 설치한 해야 **SQL Server Compact 4.0 용 Visual Studio 2010 SP1 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-176">If you get an error when you double-click *Movies.sdf*, make sure you've installed **Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**.</span></span> <span data-ttu-id="2c776-177">(소프트웨어에 대 한 링크,이 자습서 시리즈의 일부 1에서에서 필수 구성 요소 목록 참조). 릴리스를 설치한 경우 해야 닫고 Visual Web Developer를 다시 여세요.</span><span class="sxs-lookup"><span data-stu-id="2c776-177">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>


<span data-ttu-id="2c776-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="2c776-179">에 대해 하나씩, 두 개의 테이블이 `Movie` 엔터티 집합 다음의 `EdmMetadata` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-179">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="2c776-180">`EdmMetadata` 테이블 모델과 데이터베이스는 동기화 시기를 결정 하는 Entity Framework에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-180">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="2c776-181">마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-181">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="2c776-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="2c776-183">마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 스키마 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-183">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="2c776-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

<span data-ttu-id="2c776-186">알림 방법을의 스키마는 `Movies` 테이블에 매핑되는 `Movie` 앞에서 만든 클래스.</span><span class="sxs-lookup"><span data-stu-id="2c776-186">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="2c776-187">Entity Framework Code First 자동으로이 스키마에 대해 만들어진에 따라 프로그램 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-187">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="2c776-188">완료 된 경우 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-188">When you're finished, close the connection.</span></span> <span data-ttu-id="2c776-189">(연결을 닫은 하지 않는 경우 오류가 발생할 수 있습니다는 다음에 프로젝트를 실행할 때).</span><span class="sxs-lookup"><span data-stu-id="2c776-189">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="2c776-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="2c776-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span></span>

<span data-ttu-id="2c776-191">이제는 데이터베이스와 여기에서 콘텐츠를 표시 하는 간단한 목록 페이지 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-191">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="2c776-192">다음 자습서에서는 합니다 스 캐 폴드 코드의 나머지 부분을 검사 하 고 추가 `SearchIndex` 메서드 및 `SearchIndex` 보기를이 데이터베이스에서 영화를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c776-192">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="2c776-193">[이전](adding-a-model.md)
[다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="2c776-193">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
