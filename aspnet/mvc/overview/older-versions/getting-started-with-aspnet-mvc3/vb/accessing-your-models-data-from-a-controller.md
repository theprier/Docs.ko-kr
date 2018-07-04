---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: 컨트롤러 (VB)에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 0c0cdb7214b99908e4d64583e880fb03f69252c2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369304"
---
<a name="accessing-your-models-data-from-a-controller-vb"></a><span data-ttu-id="3ccec-103">컨트롤러 (VB)에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="3ccec-103">Accessing your Model's Data from a Controller (VB)</span></span>
====================
<span data-ttu-id="3ccec-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="3ccec-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="3ccec-105">이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3ccec-106">시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3ccec-107">다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3ccec-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="3ccec-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="3ccec-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="3ccec-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="3ccec-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="3ccec-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="3ccec-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="3ccec-112">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="3ccec-113">VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="3ccec-114">[VB.NET 버전](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="3ccec-115">원하는 경우 C#으로 전환 합니다 [C# 버전](../cs/accessing-your-models-data-from-a-controller.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-115">If you prefer C#, switch to the [C# version](../cs/accessing-your-models-data-from-a-controller.md) of this tutorial.</span></span>


<span data-ttu-id="3ccec-116">이 섹션에서는 새 만듭니다 `MoviesController` 클래스 및 영화 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-116">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="3ccec-117">계속 하기 전에 응용 프로그램을 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-117">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="3ccec-118">마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더를 만들어 새 `MoviesController` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-118">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="3ccec-119">다음 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-119">Select the following options:</span></span>

- <span data-ttu-id="3ccec-120">컨트롤러 이름: **MoviesController**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-120">Controller name: **MoviesController**.</span></span> <span data-ttu-id="3ccec-121">(이것이 기본값입니다.)</span><span class="sxs-lookup"><span data-stu-id="3ccec-121">(This is the default.)</span></span>
- <span data-ttu-id="3ccec-122">템플릿: **Entity Framework를 사용 하 여 읽기/쓰기 작업 및 보기를 사용 하 여 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-122">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="3ccec-123">모델 클래스: **Movie (MvcMovie.Models)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-123">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="3ccec-124">데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie.Models)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-124">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="3ccec-125">보기: **Razor (CSHTML)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-125">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="3ccec-126">(기본값입니다.)</span><span class="sxs-lookup"><span data-stu-id="3ccec-126">(The default.)</span></span>

<span data-ttu-id="3ccec-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="3ccec-128">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-128">Click **Add**.</span></span> <span data-ttu-id="3ccec-129">Visual Web Developer는 다음 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-129">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="3ccec-130">*MoviesController.vb* 프로젝트의 파일 *컨트롤러* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-130">*A MoviesController.vb* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="3ccec-131">A *영화* 프로젝트의 폴더 *뷰* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-131">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="3ccec-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, 및 *Index.vbhtml* 새 *Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, and *Index.vbhtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="3ccec-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="3ccec-134">ASP.NET MVC 3 스 캐 폴딩 메커니즘을 자동으로 생성 됩니다는 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰를 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-134">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="3ccec-135">이제 모든 기능을 갖춘 웹 응용 프로그램을 만들기, 나열, 편집 및 동영상 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-135">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="3ccec-136">응용 프로그램을 실행 하 고 이동 합니다 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에서 URL로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-136">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="3ccec-137">응용 프로그램은 기본 라우팅을 의존 하기 때문에 (에 정의 된 합니다 *Global.asax* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값으로 라우팅됩니다 `Index` 의 동작 메서드는 `Movies` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-137">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="3ccec-138">브라우저 요청 말해 `http://localhost:xxxxx/Movies` 같습니다 효과적으로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-138">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="3ccec-139">결과 빈 목록을 영화, 이므로 아직 추가 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-139">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a><span data-ttu-id="3ccec-140">영화를 만들기</span><span class="sxs-lookup"><span data-stu-id="3ccec-140">Creating a Movie</span></span>

<span data-ttu-id="3ccec-141">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-141">Select the **Create New** link.</span></span> <span data-ttu-id="3ccec-142">영화에 대 한 일부 정보를 입력 한 다음 클릭 합니다 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-142">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="3ccec-143">클릭 하는 **만들기** 단추 하면 폼이 데이터베이스에서 동영상 정보가 저장 된 서버에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-143">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="3ccec-144">다음으로 리디렉션됩니다 합니다 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-144">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="3ccec-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="3ccec-146">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-146">Create a couple more movie entries.</span></span> <span data-ttu-id="3ccec-147">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-147">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="3ccec-148">생성된 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="3ccec-148">Examining the Generated Code</span></span>

<span data-ttu-id="3ccec-149">엽니다는 *Controllers\MoviesController.vb* 파일을 생성 된 검사 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ccec-149">Open the *Controllers\MoviesController.vb* file and examine the generated `Index` method.</span></span> <span data-ttu-id="3ccec-150">영화 컨트롤러와의 일부를 `Index` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-150">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

<span data-ttu-id="3ccec-151">다음 줄을 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-151">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="3ccec-152">쿼리, 편집 및 삭제 영화에 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-152">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

<span data-ttu-id="3ccec-153">요청을를 `Movies` 컨트롤러의 모든 항목을 반환 합니다 `Movies` 영화 데이터베이스의 테이블 다음 결과 전달는 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="3ccec-153">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="3ccec-154">강력한 형식의 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="3ccec-154">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="3ccec-155">이 자습서의 앞부분에서 컨트롤러를 전달 하는 방법 데이터 또는 개체를 사용 하 여 뷰 템플릿 본는 `ViewBag` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-155">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="3ccec-156">`ViewBag` 뷰 정보를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-156">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="3ccec-157">ASP.NET MVC는 또한 형식화 된 데이터 또는 개체를 뷰 템플릿으로 강력 하 게 전달 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-157">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="3ccec-158">이 접근 방식을 사용 하면 컴파일 시간을 개선할 Visual Web Developer 편집기에서 더 다양 한 IntelliSense 및 코드 검사를 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-158">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="3ccec-159">이 방법을 사용 합니다 `MoviesController` 클래스 및 *Index.vbhtml* 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="3ccec-159">We're using this approach with the `MoviesController` class and *Index.vbhtml* view template.</span></span>

<span data-ttu-id="3ccec-160">코드를 만드는 방법을 확인할 수 있습니다는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출할 때 개체를 `View` 의 도우미 메서드에 `Index` 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="3ccec-160">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="3ccec-161">그런 다음이 `Movies` 컨트롤러에서 보기로 목록:</span><span class="sxs-lookup"><span data-stu-id="3ccec-161">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

<span data-ttu-id="3ccec-162">포함 하 여를 `@ModelType` 보기 템플릿 파일의 맨 위에 있는 문을 뷰에서 필요로 하는 개체의 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-162">By including a `@ModelType` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="3ccec-163">다음에 Visual Web Developer 영화 컨트롤러를 만들 때 자동으로 포함 `@model` 맨 위에 있는 문을 합니다 *Index.vbhtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="3ccec-163">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.vbhtml* file:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

<span data-ttu-id="3ccec-164">이렇게 `@ModelType` 지시문을 사용 하면 사용 하 여 컨트롤러에서 보기로 전달 하는 영화 목록에 액세스할 수 있습니다는 `Model` 개체는 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-164">This `@ModelType` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="3ccec-165">예를 들어 합니다 *Index.vbhtml* 수행 하 여 영화를 통해 템플릿 코드를 루프를 `foreach` 는 강력한 형식의 문을 `Model` 개체:</span><span class="sxs-lookup"><span data-stu-id="3ccec-165">For example, in the *Index.vbhtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

<span data-ttu-id="3ccec-166">때문에 `Model` 개체는 강력한 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에 있는 개체 형식의 `Movie`합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-166">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="3ccec-167">다른 이점과 함께이 의미는 코드의 컴파일 타임 검사을 얻고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-167">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="3ccec-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="3ccec-169">SQL Server Compact를 사용 하 여 작업</span><span class="sxs-lookup"><span data-stu-id="3ccec-169">Working with SQL Server Compact</span></span>

<span data-ttu-id="3ccec-170">제공 된 데이터베이스 연결 문자열을 가리키는 entity Framework Code First 검색을 `Movies` Code First 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-170">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="3ccec-171">확인 하 여 생성 된 것을 확인할 수 있습니다 합니다 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-171">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="3ccec-172">표시 되지 않는 경우는 *Movies.sdf* 파일을 클릭 합니다 **모든 파일 표시** 단추를 **솔루션 탐색기** 도구 모음에서 클릭는 **새로 고침** 단추를 클릭 한 다음를 확장 합니다 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-172">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="3ccec-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="3ccec-174">두 번 클릭 *Movies.sdf* 열려는 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-174">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="3ccec-175">다음를 확장 합니다 **테이블** 데이터베이스에서 생성 된 테이블을 표시 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-175">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="3ccec-176">두 번 클릭 하면 오류가 발생 하는 경우 *Movies.sdf*를 설치한 다음 했는지 **SQL Server Compact 4.0 용 Visual Studio 2010 SP1 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-176">If you get an error when you double-click *Movies.sdf*, make sure you've installed **Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**.</span></span> <span data-ttu-id="3ccec-177">(소프트웨어에 대 한 링크,이 자습서 시리즈의 1 부에서는 필수 조건 목록 참조). 릴리스를 설치한 경우 해야 닫았다가 다시 Visual Web Developer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-177">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>


<span data-ttu-id="3ccec-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="3ccec-179">에 대해 하나씩, 두 테이블이 합니다 `Movie` 엔터티 집합 및는 `EdmMetadata` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-179">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="3ccec-180">`EdmMetadata` 테이블 엔터티 프레임 워크에서 모델 및 데이터베이스 동기화 되지 않은 경우 확인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-180">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="3ccec-181">마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-181">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="3ccec-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="3ccec-183">마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 스키마 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-183">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="3ccec-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

<span data-ttu-id="3ccec-186">알림 방법의 스키마를 `Movies` 테이블에 매핑됩니다는 `Movie` 앞에서 만든 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-186">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="3ccec-187">Entity Framework Code First 자동으로 생성이 스키마에 따라 프로그램 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-187">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="3ccec-188">이 과정을 완료 하는 경우 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-188">When you're finished, close the connection.</span></span> <span data-ttu-id="3ccec-189">(연결을 닫으려면 없는 경우 하면 오류가 발생할 수 다음에 프로젝트를 실행할 때).</span><span class="sxs-lookup"><span data-stu-id="3ccec-189">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="3ccec-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="3ccec-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span></span>

<span data-ttu-id="3ccec-191">이제 있고 데이터베이스는 단순 목록 페이지에서 콘텐츠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-191">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="3ccec-192">다음 자습서에서에서는 스 캐 폴드 된 코드의 나머지 부분을 검사 하 고 추가 된 `SearchIndex` 메서드 및 `SearchIndex` 영화가이 데이터베이스에 대 한 검색할 수 있는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="3ccec-192">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3ccec-193">[이전](adding-a-model.md)
> [다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="3ccec-193">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
