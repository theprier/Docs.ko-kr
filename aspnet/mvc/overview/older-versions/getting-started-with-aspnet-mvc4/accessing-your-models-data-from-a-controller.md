---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: cf896a6a9ce6cb8cd4adb13c3d87c4e7c3095fa6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="1787c-104">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="1787c-104">Accessing Your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="1787c-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="1787c-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="1787c-106">이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="1787c-107">더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="1787c-108">이 섹션에서는 새 만들어 `MoviesController` 클래스 및 동영상 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="1787c-109">**응용 프로그램을 빌드합니다** 다음 단계를 진행 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="1787c-110">마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더를 만들고 새 `MoviesController` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="1787c-111">아래 옵션은 응용 프로그램을 빌드할 때까지 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="1787c-112">다음 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-112">Select the following options:</span></span>

- <span data-ttu-id="1787c-113">컨트롤러 이름: **MoviesController**합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="1787c-114">(기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-114">(This is the default.</span></span> <span data-ttu-id="1787c-115">)</span><span class="sxs-lookup"><span data-stu-id="1787c-115">)</span></span>
- <span data-ttu-id="1787c-116">서식 파일: **Entity Framework를 사용 하 여 읽기/쓰기 동작 및 뷰가, 포함 된 MVC 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="1787c-117">모델 클래스: **동영상 (MvcMovie.Models)**합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="1787c-118">데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie.Models)**합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="1787c-119">보기: **Razor (CSHTML)**합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="1787c-120">(기본값입니다.)</span><span class="sxs-lookup"><span data-stu-id="1787c-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="1787c-122">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-122">Click **Add**.</span></span> <span data-ttu-id="1787c-123">Visual Studio Express 다음 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="1787c-124">*MoviesController.cs* 프로젝트의 파일 *컨트롤러* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="1787c-125">A *동영상* 프로젝트의 폴더 *뷰* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="1787c-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, 및 *Index.cshtml* 새 *Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="1787c-127">ASP.NET MVC 4 자동으로 생성 됩니다는 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드 및 (CRUD 작업 메서드 및 보기의 자동 만들기가 스 캐 폴딩은) 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="1787c-128">만들기, 목록, 편집 및 동영상 항목을 삭제할 수 있는 완벽 하 게 작동 하는 웹 응용 프로그램을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="1787c-129">응용 프로그램을 실행 하 고를 찾습니다는 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에 URL을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="1787c-130">응용 프로그램은 기본 라우팅에 의존 하므로 때문에 (에 정의 된는 *Global.asax* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값에 라우팅 된다고 `Index` 의 동작 메서드는 `Movies` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="1787c-131">즉, 브라우저 요청 `http://localhost:xxxxx/Movies` 브라우저 요청 동일은 사실상 `http://localhost:xxxxx/Movies/Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="1787c-132">결과 아직 추가 하지 때문에 빈 목록 영화,입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="1787c-133">동영상 만들기</span><span class="sxs-lookup"><span data-stu-id="1787c-133">Creating a Movie</span></span>

<span data-ttu-id="1787c-134">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-134">Select the **Create New** link.</span></span> <span data-ttu-id="1787c-135">동영상에 대 한 일부 세부 정보를 입력 한 다음 클릭는 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="1787c-136">클릭 하 고 **만들기** 단추를 클릭 하면 데이터베이스에 동영상 정보 저장 되는 서버에 게시 될 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="1787c-137">다음 리디렉션됩니다 하는 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="1787c-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span><span class="sxs-lookup"><span data-stu-id="1787c-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="1787c-139">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-139">Create a couple more movie entries.</span></span> <span data-ttu-id="1787c-140">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="1787c-141">생성된 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="1787c-141">Examining the Generated Code</span></span>

<span data-ttu-id="1787c-142">열기는 *Controllers\MoviesController.cs* 파일을 생성 된 검사 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1787c-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="1787c-143">영화 컨트롤러와의 일부는 `Index` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="1787c-144">다음 줄은 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="1787c-145">쿼리, 편집 및 삭제 영화를 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="1787c-146">요청을는 `Movies` 컨트롤러의 모든 항목이 반환는 `Movies` 영화 데이터베이스 테이블의 다음 결과를 전달는 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="1787c-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="1787c-147">강력한 형식 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="1787c-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="1787c-148">이 자습서의 앞부분에서 언급 했 듯이 어떻게 컨트롤러를 전달할 수 데이터 나 개체를 사용 하 여 뷰 서식 파일은 `ViewBag` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="1787c-149">`ViewBag` 정보 보기를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="1787c-150">또한 ASP.NET MVC는 강력 하 게 전달 하는 기능 입력 한 데이터 또는 개체 템플릿 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="1787c-151">이 접근 방식을 사용 하면 더 나은 컴파일 타임 검사 코드 및 Visual Studio 편집기에서 다양 한 IntelliSense의 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="1787c-152">Visual Studio에서 스 캐 폴딩 메커니즘이이 방법을 사용 하는 `MoviesController` 메서드 및 뷰를 만들 때 클래스와 보기 템플릿.</span><span class="sxs-lookup"><span data-stu-id="1787c-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="1787c-153">에 *Controllers\MoviesController.cs* 생성 된 파일 검사 `Details` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1787c-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="1787c-154">영화 컨트롤러와의 일부는 `Details` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="1787c-155">경우는 `Movie` 발견 되 면의 인스턴스는 `Movie` 모델 자세히 보기에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="1787c-156">내용을 검사는 *Views\Movies\Details.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="1787c-157">포함 하 여 한 `@model` 문을 보기 템플릿 파일 맨 위에 있는 보기를 필요로 하는 개체의 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="1787c-158">영화 컨트롤러를 만들 때 Visual Studio에서는 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="1787c-159">이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="1787c-160">예를 들어는 *Details.cshtml* 서식 파일을 코드는 각 영화 필드를 전달는 `DisplayNameFor` 및 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 도우미와 강력한 형식의 `Model` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="1787c-161">만들기 및 편집 메서드 및 템플릿 보기 동영상 모델 개체를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="1787c-162">검사는 *Index.cshtml* 템플릿 보기 및 `Index` 에서 메서드는 *MoviesController.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="1787c-163">코드 만드는 방법을 확인할 수는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출 되 면 개체는 `View` 의 도우미 메서드는 `Index` 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="1787c-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="1787c-164">그런 다음이 `Movies` 보기에는 컨트롤러에서 목록:</span><span class="sxs-lookup"><span data-stu-id="1787c-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="1787c-165">영화 컨트롤러를 만들 때 Visual Studio Express 다음 자동으로 포함 `@model` 맨 위에 있는 문에 *Index.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="1787c-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="1787c-166">이 `@model` 지시문을 사용 하면 컨트롤러 사용 하 여 보기에 전달 되는 동영상 목록을 액세스할 수 있습니다는 `Model` 강력한 형식 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="1787c-167">예를 들어는 *Index.cshtml* 서식 파일을 코드 반복 동영상 수행 하 여 한 `foreach` 문을 통해 강력한 형식의 `Model` 개체:</span><span class="sxs-lookup"><span data-stu-id="1787c-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="1787c-168">때문에 `Model` 개체는 강력한 형식 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에서 개체도 입력 된 `Movie`합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="1787c-169">여러 가지 이점을 얻을이 의미 가져오기 코드의 컴파일 타임 검사 하 고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="1787c-171">SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="1787c-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="1787c-172">제공 된 데이터베이스 연결 문자열이 가리키는 entity Framework Code First 감지는 `Movies` 데이터베이스 코드 첫 번째 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="1787c-173">검색 하 여 생성 되어 있는지 확인할 수 있습니다는 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="1787c-174">표시 되지 않으면는 *Movies.mdf* 파일을 클릭는 **모든 파일 표시** 단추는 **솔루션 탐색기** 도구 모음에서 클릭 된 **새로 고침** 단추를 선택한 다음 확장은 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="1787c-175">두 번 클릭 *Movies.mdf* 열려는 **데이터베이스 탐색기**, 다음 확장는 **테이블** 영화 테이블을 표시 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="1787c-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="1787c-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="1787c-177">데이터베이스 탐색기 표시 되지 않으면에서 **도구** 메뉴 선택 **데이터베이스에 연결**, 다음 취소는 **데이터 소스 선택** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="1787c-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="1787c-178">이렇게 하면 강제로 열려 데이터베이스 탐색기.</span><span class="sxs-lookup"><span data-stu-id="1787c-178">This will force open the database explorer.</span></span>


> [!NOTE]
> <span data-ttu-id="1787c-179">VWD 또는 Visual Studio 2010을 사용 하는 다음 중 하나에 유사한 오류가 발생할 경우:</span><span class="sxs-lookup"><span data-stu-id="1787c-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="1787c-180">데이터베이스 ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES 합니다. MDF' 706 버전 이기 때문에 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="1787c-181">이 서버 버전 655 및 이전 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="1787c-182">다운 그레이드 경로가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="1787c-183">&quot;InvalidOperation 예외가 사용자 코드에 의해 처리 되지 않은&quot; 제공 된 SqlConnection이 초기 카탈로그를 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="1787c-184">설치 해야는 [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) 및 [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="1787c-185">확인 된 `MovieDBContext` 이전 페이지에서 지정 된 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>


<span data-ttu-id="1787c-186">마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="1787c-187">마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 정의 열기** 구조는 Entity Framework Code First으로 생성 하는 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

<span data-ttu-id="1787c-188">![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")</span><span class="sxs-lookup"><span data-stu-id="1787c-188">![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")</span></span>

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="1787c-189">알림 방법을의 스키마는 `Movies` 테이블에 매핑되는 `Movie` 앞에서 만든 클래스.</span><span class="sxs-lookup"><span data-stu-id="1787c-189">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="1787c-190">Entity Framework Code First 자동으로이 스키마에 대해 만들어진에 따라 프로그램 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-190">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="1787c-191">완료 되 면 마우스 오른쪽 단추로 클릭 하 여 연결을 닫을 *MovieDBContext* 선택 하 고 **연결 닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-191">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="1787c-192">(연결을 닫은 하지 않는 경우 오류가 발생할 수 있습니다는 다음에 프로젝트를 실행할 때).</span><span class="sxs-lookup"><span data-stu-id="1787c-192">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="1787c-193">![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")</span><span class="sxs-lookup"><span data-stu-id="1787c-193">![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")</span></span>

<span data-ttu-id="1787c-194">이제는 데이터베이스와 여기에서 콘텐츠를 표시 하는 간단한 목록 페이지 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-194">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="1787c-195">다음 자습서에서는 합니다 스 캐 폴드 코드의 나머지 부분을 검사 하 고 추가 `SearchIndex` 메서드 및 `SearchIndex` 보기를이 데이터베이스에서 영화를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1787c-195">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1787c-196">[이전](adding-a-model.md)
> [다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="1787c-196">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
