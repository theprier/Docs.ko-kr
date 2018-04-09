---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: d3dfa079c334e04f368531456ec2ec4e9728f893
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="d5b81-102">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="d5b81-102">Accessing Your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="d5b81-103">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="d5b81-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="d5b81-104">이 섹션에서는 새 만들어 `MoviesController` 클래스 및 동영상 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="d5b81-105">**응용 프로그램을 빌드합니다** 다음 단계를 진행 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="d5b81-106">응용 프로그램을 작성 하지 않아도 컨트롤러 추가 오류가 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="d5b81-107">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더와 클릭 **추가**, 다음 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="d5b81-108">에 **스 캐 폴드를 추가** 대화 상자를 클릭 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 5 컨트롤러**, 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="d5b81-109">선택 **동영상 (MvcMovie.Models)** 모델 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="d5b81-110">선택 **MovieDBContext (MvcMovie.Models)** 데이터 컨텍스트 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="d5b81-111">컨트롤러 이름에 대 한 입력 **MoviesController**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="d5b81-112">아래 이미지 완료 된 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="d5b81-113">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-113">Click **Add**.</span></span> <span data-ttu-id="d5b81-114">(오류가 발생 하는 경우 직접 아마도 빌드하지 않은 컨트롤러 추가 시작 하기 전에 응용 프로그램입니다.) Visual Studio는 다음과 같은 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="d5b81-115">*MoviesController.cs* 파일에 *컨트롤러* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="d5b81-116">A *Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="d5b81-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, 및 *Index.cshtml* 새 *Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="d5b81-118">Visual Studio에서 자동으로 작성 된 [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (만들기, 읽기, 업데이트 및 삭제) 작업 메서드 및 (CRUD 작업 메서드 및 보기의 자동 만들기가 스 캐 폴딩은) 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="d5b81-119">만들기, 목록, 편집 및 동영상 항목을 삭제할 수 있는 완벽 하 게 작동 하는 웹 응용 프로그램을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="d5b81-120">응용 프로그램을 실행 하 고 클릭는 **MVC 영화** 링크 (또는 검색 하는 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에서 URL로).</span><span class="sxs-lookup"><span data-stu-id="d5b81-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="d5b81-121">응용 프로그램은 기본 라우팅에 의존 하므로 때문에 (에 정의 된는 *앱\_Start\RouteConfig.cs* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값에 라우팅 된다고 `Index` 는 의동작메서드`Movies` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="d5b81-122">즉, 브라우저 요청 `http://localhost:xxxxx/Movies` 브라우저 요청 동일은 사실상 `http://localhost:xxxxx/Movies/Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="d5b81-123">결과 아직 추가 하지 때문에 빈 목록 영화,입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="d5b81-124">동영상 만들기</span><span class="sxs-lookup"><span data-stu-id="d5b81-124">Creating a Movie</span></span>

<span data-ttu-id="d5b81-125">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-125">Select the **Create New** link.</span></span> <span data-ttu-id="d5b81-126">동영상에 대 한 일부 세부 정보를 입력 한 다음 클릭는 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-126">Enter some details about a movie and then click the **Create** button.</span></span>


![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="d5b81-127">Price 필드에서 소수점이 하 또는 쉼표를 입력할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="d5b81-128">쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하기 위해 (&quot;,&quot;) 소수점 및 미국 영어가 아닌 날짜 형식을 포함 해야 *globalize.js* 및 특정  *cultures/globalize.cultures.js* 파일 (에서 [ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 및 사용 하는 JavaScript `Globalize.parseFloat`합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="d5b81-129">다음 자습서에서이 작업을 수행 하는 방법을 보여 드리 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="d5b81-130">이제 10 같은 정수를 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-130">For now, just enter whole numbers like 10.</span></span>


<span data-ttu-id="d5b81-131">클릭 하 고 **만들기** 단추를 클릭 하면 데이터베이스에 동영상 정보 저장 되는 서버에 게시 될 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="d5b81-132">다음 리디렉션됩니다 하는 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="d5b81-133">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-133">Create a couple more movie entries.</span></span> <span data-ttu-id="d5b81-134">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="d5b81-135">생성된 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="d5b81-135">Examining the Generated Code</span></span>

<span data-ttu-id="d5b81-136">열기는 *Controllers\MoviesController.cs* 파일을 생성 된 검사 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d5b81-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="d5b81-137">영화 컨트롤러와의 일부는 `Index` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="d5b81-138">요청을는 `Movies` 컨트롤러의 모든 항목이 반환는 `Movies` 테이블을 다음에 결과 전달 합니다.는 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="d5b81-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="d5b81-139">다음 줄은 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="d5b81-140">쿼리, 편집 및 삭제 영화를 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="d5b81-141">강력한 형식 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="d5b81-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="d5b81-142">이 자습서의 앞부분에서 언급 했 듯이 어떻게 컨트롤러를 전달할 수 데이터 나 개체를 사용 하 여 뷰 서식 파일은 `ViewBag` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="d5b81-143">`ViewBag` 정보 보기를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="d5b81-144">MVC 전달 하는 기능도 제공 *강력한* 템플릿 보기에 개체를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="d5b81-145">이 강력한 형식의 방법을 더 나은 컴파일 타임 검사 코드 및 다양 한를 사용 하면 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="d5b81-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="d5b81-146">Visual Studio에서 스 캐 폴딩 메커니즘이이 방법을 사용 하는 (즉, 전달는 *강력한* 형식화 된 모델)와 `MoviesController` 메서드 및 뷰를 만들 때 클래스와 보기 템플릿.</span><span class="sxs-lookup"><span data-stu-id="d5b81-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="d5b81-147">에 *Controllers\MoviesController.cs* 생성 된 파일 검사 `Details` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d5b81-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="d5b81-148">`Details` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="d5b81-149">`id` 매개 변수는 일반적으로 예: 전달 된 경로 데이터로 `http://localhost:1234/movies/details/1` 컨트롤러 영화 컨트롤러 동작을 설정 합니다 `details` 및 `id` 1입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="d5b81-150">전달할 수 있습니다도 쿼리 문자열이 포함 된 id에 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="d5b81-151">경우는 `Movie` 발견 되 면의 인스턴스는 `Movie` 모델에 전달 되는 `Details` 보기:</span><span class="sxs-lookup"><span data-stu-id="d5b81-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="d5b81-152">내용을 검사는 *Views\Movies\Details.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="d5b81-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="d5b81-153">포함 하 여 한 `@model` 문을 보기 템플릿 파일 맨 위에 있는 보기를 필요로 하는 개체의 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="d5b81-154">영화 컨트롤러를 만들 때 Visual Studio에서는 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="d5b81-155">이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="d5b81-156">예를 들어는 *Details.cshtml* 서식 파일을 코드는 각 영화 필드를 전달는 `DisplayNameFor` 및 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 도우미와 강력한 형식의 `Model` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="d5b81-157">`Create` 및 `Edit` 메서드 및 템플릿 보기 동영상 모델 개체를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="d5b81-158">검사는 *Index.cshtml* 템플릿 보기 및 `Index` 에서 메서드는 *MoviesController.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="d5b81-159">코드 만드는 방법을 확인할 수는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출 되 면 개체는 `View` 의 도우미 메서드는 `Index` 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="d5b81-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="d5b81-160">그런 다음이 `Movies` 에서 나열 된 `Index` 보기로 동작 메서드:</span><span class="sxs-lookup"><span data-stu-id="d5b81-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="d5b81-161">Visual Studio에서 다음을 자동으로 포함 영화 컨트롤러를 만들 때 `@model` 맨 위에 있는 문에 *Index.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="d5b81-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="d5b81-162">이 `@model` 지시문을 사용 하면 컨트롤러 사용 하 여 보기에 전달 되는 동영상 목록을 액세스할 수 있습니다는 `Model` 강력한 형식 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="d5b81-163">예를 들어는 *Index.cshtml* 서식 파일을 코드 반복 동영상 수행 하 여 한 `foreach` 문을 통해 강력한 형식의 `Model` 개체:</span><span class="sxs-lookup"><span data-stu-id="d5b81-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="d5b81-164">때문에 `Model` 개체는 강력한 형식 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에서 개체도 입력 된 `Movie`합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="d5b81-165">여러 가지 이점을 얻을이 의미 가져오기 코드의 컴파일 타임 검사 하 고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="d5b81-167">SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="d5b81-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="d5b81-168">제공 된 데이터베이스 연결 문자열이 가리키는 entity Framework Code First 감지는 `Movies` 데이터베이스 코드 첫 번째 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="d5b81-169">검색 하 여 생성 되어 있는지 확인할 수 있습니다는 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="d5b81-170">표시 되지 않으면는 *Movies.mdf* 파일을 클릭는 **모든 파일 표시** 단추는 **솔루션 탐색기** 도구 모음에서 클릭 된 **새로 고침** 단추를 선택한 다음 확장은 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="d5b81-171">두 번 클릭 *Movies.mdf* 열려는 **서버 탐색기**, 다음 확장는 **테이블** 영화 테이블을 표시 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="d5b81-172">Note 열쇠 아이콘 옆에 있는 id입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-172">Note the key icon next to ID.</span></span> <span data-ttu-id="d5b81-173">기본적으로 EF 라는 기본 키 ID 속성이 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="d5b81-174">EF 및 MVC에 대 한 자세한 내용은 Tom Dykstra 뛰어난 자습서에서 참조 [MVC 및 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="d5b81-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="d5b81-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="d5b81-176">마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="d5b81-177">마우스 오른쪽 단추로 클릭는 `Movies` 테이블을 선택한 **테이블 정의 열기** 구조는 Entity Framework Code First으로 생성 하는 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="d5b81-178">알림 방법을의 스키마는 `Movies` 테이블에 매핑되는 `Movie` 앞에서 만든 클래스.</span><span class="sxs-lookup"><span data-stu-id="d5b81-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="d5b81-179">Entity Framework Code First 자동으로이 스키마에 대해 만들어진에 따라 프로그램 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="d5b81-180">완료 되 면 마우스 오른쪽 단추로 클릭 하 여 연결을 닫을 *MovieDBContext* 선택 하 고 **연결 닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="d5b81-181">(연결을 닫은 하지 않는 경우 오류가 발생할 수 있습니다는 다음에 프로젝트를 실행할 때).</span><span class="sxs-lookup"><span data-stu-id="d5b81-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="d5b81-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span><span class="sxs-lookup"><span data-stu-id="d5b81-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span></span>

<span data-ttu-id="d5b81-183">이제 데이터를 표시, 편집, 업데이트 및 삭제할 데이터베이스 및 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-183">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="d5b81-184">다음 자습서에서는 합니다 스 캐 폴드 코드의 나머지 부분을 검사 하 고 추가 `SearchIndex` 메서드 및 `SearchIndex` 보기를이 데이터베이스에서 영화를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-184">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="d5b81-185">MVC와 함께 Entity Framework를 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d5b81-185">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d5b81-186">[이전](creating-a-connection-string.md)
> [다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="d5b81-186">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
