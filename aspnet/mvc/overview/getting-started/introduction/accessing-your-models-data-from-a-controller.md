---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 16f4a61d048e90b7962f038e90e0721883726c44
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834812"
---
<a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="fcb56-102">컨트롤러에서 모델의 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="fcb56-102">Accessing Your Model's Data from a Controller</span></span>
====================
<span data-ttu-id="fcb56-103">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="fcb56-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="fcb56-104">이 섹션에서는 새 만듭니다 `MoviesController` 클래스 및 영화 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="fcb56-105">**응용 프로그램을 빌드할** 다음 단계로 진행 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="fcb56-106">응용 프로그램을 작성 하지 않아도 오류가 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="fcb56-107">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더 및 클릭 한 다음 **추가**, 한 다음 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="fcb56-108">에 **스 캐 폴드 추가** 대화 상자, 클릭 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="fcb56-109">선택 **Movie (MvcMovie.Models)** 모델 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="fcb56-110">선택 **MovieDBContext (MvcMovie.Models)** 데이터 컨텍스트 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="fcb56-111">컨트롤러 이름을 입력 **MoviesController**합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="fcb56-112">아래 이미지에서는 완료 된 대화 상자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="fcb56-113">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-113">Click **Add**.</span></span> <span data-ttu-id="fcb56-114">(오류가 발생 하면 아마도 빌드하지 않은 컨트롤러 추가 시작 하기 전에 응용 프로그램입니다.) Visual Studio는 다음 파일 및 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="fcb56-115">*MoviesController.cs* 파일을 *컨트롤러* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="fcb56-116">A *Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="fcb56-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, 및 *Index.cshtml* 새 *Views\Movies* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="fcb56-118">Visual Studio에서 자동으로 작성 된 [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰 있습니다 (자동으로 만들도록 CRUD 작업 메서드와 뷰 스 캐 폴딩이라고).</span><span class="sxs-lookup"><span data-stu-id="fcb56-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="fcb56-119">이제 모든 기능을 갖춘 웹 응용 프로그램을 만들기, 나열, 편집 및 동영상 항목을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="fcb56-120">응용 프로그램을 실행 하 고 클릭 합니다 **MVC 동영상** 링크 (찾아보거나 합니다 `Movies` 추가 하 여 컨트롤러 */Movies* 브라우저의 주소 표시줄에서 URL로).</span><span class="sxs-lookup"><span data-stu-id="fcb56-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="fcb56-121">응용 프로그램은 기본 라우팅을 의존 하기 때문에 (에 정의 된를 앱\_start\ 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값으로 라우팅됩니다 `Index` 합니다 의동작메서드`Movies` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="fcb56-122">브라우저 요청 말해 `http://localhost:xxxxx/Movies` 같습니다 효과적으로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="fcb56-123">결과 빈 목록을 영화, 이므로 아직 추가 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="fcb56-124">영화를 만들기</span><span class="sxs-lookup"><span data-stu-id="fcb56-124">Creating a Movie</span></span>

<span data-ttu-id="fcb56-125">**새로 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-125">Select the **Create New** link.</span></span> <span data-ttu-id="fcb56-126">영화에 대 한 일부 정보를 입력 한 다음 클릭 합니다 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-126">Enter some details about a movie and then click the **Create** button.</span></span>


![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="fcb56-127">Price 필드에서 소수점 또는 쉼표를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="fcb56-128">쉼표를 사용 하는 영어가 아닌 로캘의 jQuery 유효성 검사를 지원 하도록 (&quot;,&quot;), 소수점 및 미국 영어가 아닌 날짜 형식에 대 한 포함 해야 합니다 *globalize.js* 및 특정  *cultures/globalize.cultures.js* 파일 (에서 [ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 및 JavaScript를 사용 하 여 `Globalize.parseFloat`입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="fcb56-129">다음 자습서에서이 작업을 수행 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="fcb56-130">이제 10 같은 정수를 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-130">For now, just enter whole numbers like 10.</span></span>


<span data-ttu-id="fcb56-131">클릭 하는 **만들기** 단추 하면 폼이 데이터베이스에서 동영상 정보가 저장 된 서버에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="fcb56-132">다음으로 리디렉션됩니다 합니다 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="fcb56-133">나머지 몇 개의 동영상 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-133">Create a couple more movie entries.</span></span> <span data-ttu-id="fcb56-134">모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="fcb56-135">생성된 된 코드 검사</span><span class="sxs-lookup"><span data-stu-id="fcb56-135">Examining the Generated Code</span></span>

<span data-ttu-id="fcb56-136">엽니다는 *Controllers\MoviesController.cs* 파일을 생성 된 검사 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="fcb56-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="fcb56-137">영화 컨트롤러와의 일부를 `Index` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="fcb56-138">요청을를 `Movies` 컨트롤러의 모든 항목을 반환 합니다 `Movies` 테이블 및 결과를 전달 합니다는 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="fcb56-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="fcb56-139">다음 줄을 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="fcb56-140">쿼리, 편집 및 삭제 영화에 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="fcb56-141">강력한 형식의 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="fcb56-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="fcb56-142">이 자습서의 앞부분에서 컨트롤러를 전달 하는 방법 데이터 또는 개체를 사용 하 여 뷰 템플릿 본는 `ViewBag` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="fcb56-143">`ViewBag` 뷰 정보를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="fcb56-144">MVC를 전달 하는 기능도 제공 *강력한* 보기 템플릿에 개체를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="fcb56-145">이 강력한 형식의 방법을 더 나은 컴파일 타임 풍부 하 고 코드 검사를 사용 하면 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="fcb56-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="fcb56-146">이 방법을 사용 하는 Visual Studio에서 스 캐 폴딩 메커니즘 (즉, 전달를 *강력한* 형식화 된 모델) 사용 하 여는 `MoviesController` 메서드 및 뷰를 만들면 템플릿 클래스 및 보기.</span><span class="sxs-lookup"><span data-stu-id="fcb56-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="fcb56-147">에 *Controllers\MoviesController.cs* 생성 된 파일 검사 `Details` 메서드.</span><span class="sxs-lookup"><span data-stu-id="fcb56-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="fcb56-148">`Details` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="fcb56-149">`id` 매개 변수는 경로 데이터 변수로 예를 들어 전달 일반적으로 `http://localhost:1234/movies/details/1` 영화 컨트롤러에 동작을 컨트롤러 설정이 `details` 및 `id` 1입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="fcb56-150">또한 다음과 전달할 수 있습니다 일괄 처리 id는 쿼리 문자열을 사용 하 여 다음과 같이</span><span class="sxs-lookup"><span data-stu-id="fcb56-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="fcb56-151">경우는 `Movie` 발견 되는 인스턴스의 합니다 `Movie` 모델에 전달 되는 `Details` 보기:</span><span class="sxs-lookup"><span data-stu-id="fcb56-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="fcb56-152">콘텐츠를 검사 합니다 *Views\Movies\Details.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="fcb56-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="fcb56-153">포함 하 여를 `@model` 보기 템플릿 파일의 맨 위에 있는 문을 뷰에서 필요로 하는 개체의 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="fcb56-154">영화 컨트롤러를 만들 때 Visual Studio에서는 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="fcb56-155">이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="fcb56-156">예를 들어, 합니다 *Details.cshtml* 템플릿 코드는 각 영화 필드를 전달 합니다 `DisplayNameFor` 및 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 도우미와 강력한 형식의 `Model` 개체.</span><span class="sxs-lookup"><span data-stu-id="fcb56-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="fcb56-157">합니다 `Create` 및 `Edit` 메서드 및 보기 템플릿은 동영상 모델 개체를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="fcb56-158">검사는 *Index.cshtml* 템플릿 보기 및 `Index` 의 메서드를 *MoviesController.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="fcb56-159">코드를 만드는 방법을 확인할 수 있습니다는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출할 때 개체를 `View` 의 도우미 메서드에 `Index` 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="fcb56-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="fcb56-160">그런 다음이 `Movies` 에서 나열 된 `Index` 보기로 작업 메서드:</span><span class="sxs-lookup"><span data-stu-id="fcb56-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="fcb56-161">다음에 Visual Studio 영화 컨트롤러를 만들 때 자동으로 포함 `@model` 맨 위에 있는 문을 합니다 *Index.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="fcb56-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="fcb56-162">이렇게 `@model` 지시문을 사용 하면 사용 하 여 컨트롤러에서 보기로 전달 하는 영화 목록에 액세스할 수 있습니다는 `Model` 개체는 강력한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="fcb56-163">예를 들어 합니다 *Index.cshtml* 수행 하 여 영화를 통해 템플릿 코드를 루프를 `foreach` 는 강력한 형식의 문을 `Model` 개체:</span><span class="sxs-lookup"><span data-stu-id="fcb56-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="fcb56-164">때문에 `Model` 개체는 강력한 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에 있는 개체 형식의 `Movie`합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="fcb56-165">다른 이점과 함께이 의미는 코드의 컴파일 타임 검사을 얻고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="fcb56-167">SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="fcb56-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="fcb56-168">제공 된 데이터베이스 연결 문자열을 가리키는 entity Framework Code First 검색을 `Movies` Code First 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="fcb56-169">확인 하 여 생성 된 것을 확인할 수 있습니다 합니다 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="fcb56-170">표시 되지 않는 경우는 *Movies.mdf* 파일을 클릭 합니다 **모든 파일 표시** 단추를 **솔루션 탐색기** 도구 모음에서 클릭는 **새로 고침** 단추를 클릭 한 다음를 확장 합니다 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="fcb56-171">두 번 클릭 *Movies.mdf* 열려는 **서버 탐색기**를 차례로 확장 합니다 **테이블** 영화 표를 참조 하는 폴더.</span><span class="sxs-lookup"><span data-stu-id="fcb56-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="fcb56-172">Note id입니다. 옆에 있는 키 아이콘</span><span class="sxs-lookup"><span data-stu-id="fcb56-172">Note the key icon next to ID.</span></span> <span data-ttu-id="fcb56-173">기본적으로 EF는 기본 키 ID 라는 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="fcb56-174">EF 및 MVC에 대 한 자세한 내용은 Tom Dykstra 훌륭한 자습서를 참조 하세요 [MVC 및 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="fcb56-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="fcb56-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="fcb56-176">마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="fcb56-177">마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 정의 열기** 구조체는 Entity Framework Code First를 생성 하는 테이블을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="fcb56-178">알림 방법의 스키마를 `Movies` 테이블에 매핑됩니다는 `Movie` 앞에서 만든 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="fcb56-179">Entity Framework Code First 자동으로 생성이 스키마에 따라 프로그램 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="fcb56-180">완료 되 면, 마우스 오른쪽 단추로 클릭 하 여 연결을 닫습니다 *MovieDBContext* 를 선택 하 고 **연결 닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="fcb56-181">(연결을 닫으려면 없는 경우 하면 오류가 발생할 수 다음에 프로젝트를 실행할 때).</span><span class="sxs-lookup"><span data-stu-id="fcb56-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="fcb56-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span><span class="sxs-lookup"><span data-stu-id="fcb56-182">![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")</span></span>

<span data-ttu-id="fcb56-183">이제 데이터를 표시, 편집, 업데이트 및 삭제할 데이터베이스 및 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-183">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="fcb56-184">다음 자습서에서에서는 스 캐 폴드 된 코드의 나머지 부분을 검사 하 고 추가 된 `SearchIndex` 메서드 및 `SearchIndex` 영화가이 데이터베이스에 대 한 검색할 수 있는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-184">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="fcb56-185">MVC와 함께 Entity Framework를 사용 하는 방법은 참조 하세요 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fcb56-185">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fcb56-186">[이전](creating-a-connection-string.md)
> [다음](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="fcb56-186">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
