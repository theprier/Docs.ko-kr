---
title: "MVC 응용 프로그램에 뷰 추가"
author: Rick-Anderson
description: "MVC 응용 프로그램에 뷰 추가"
ms.author: riande
manager: wpickett
ms.date: 09/1721/2017
ms.topic: article
ms.technology: dotnet-mvc
ms.prod: .net-framework
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: 86887f0dafa31ff3eb6597284c469c4b3053b6b7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="adding-a-view"></a><span data-ttu-id="95d53-103">뷰 추가</span><span class="sxs-lookup"><span data-stu-id="95d53-103">Adding a View</span></span>
====================
<span data-ttu-id="95d53-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="95d53-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="95d53-105">이 섹션에 수정 하려는 `HelloWorldController` 템플릿 파일을 명확 하 게 캡슐화 하는 프로세스를 클라이언트에 HTML 응답을 생성 하는 뷰를 사용 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-105">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span> 

<span data-ttu-id="95d53-106">사용 하 여 보기 템플릿 파일 만듭니다는 [Razor 뷰 엔진](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-106">You'll create a view template file using the [Razor view engine](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md).</span></span> <span data-ttu-id="95d53-107">Razor 기반 보기 템플릿에 *.cshtml* 파일 확장명이 및 C#을 사용 하 여 출력 하는 HTML을 만들기 위해 세련 된 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-107">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="95d53-108">Razor 뷰 템플릿을 작성할 때 필요한 키 입력 및 문자 수를 최소화 하 고 워크플로 코딩 빠르지 유체를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-108">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="95d53-109">현재 `Index` 메서드는 컨트롤러 클래스에서 하드 코딩된 메시지 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-109">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="95d53-110">변경 된 `Index` 반환 하는 메서드는 `View` 다음 코드와 같이 개체:</span><span class="sxs-lookup"><span data-stu-id="95d53-110">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

<span data-ttu-id="95d53-111">`Index` 위의 방법을 템플릿 보기를 사용 하 여 브라우저에 대 한 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-111">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="95d53-112">컨트롤러 메서드 (라고도 [작업 메서드](http://rachelappel.com/asp.net-mvc-actionresults-explained))와 같은 `Index` 위의 메서드는 일반적으로 반환 된 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (또는 클래스에서 파생 된 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx))와 같은 문자열 하지 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-112">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="95d53-113">마우스 오른쪽 단추로 클릭는 *Views\HelloWorld* 폴더 **추가**, 클릭 **(Razor) 레이아웃이 있는 MVC 5 뷰 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-113">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image1.png)   
  
<span data-ttu-id="95d53-114">에 **항목에 대 한 이름 지정** 대화 상자에 입력 *인덱스*, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-114">In the **Specify Name for Item** dialog box, enter *Index*, and then click **OK**.</span></span>  
  
![](adding-a-view/_static/image2.png)  
  
<span data-ttu-id="95d53-115">에 **레이아웃 페이지 선택** 대화 상자에서 기본값을 적용  **\_Layout.cshtml** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-115">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image3.png)  
  
<span data-ttu-id="95d53-116">위의 대화 상자에는 *Views\Shared* 왼쪽된 창에서 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-116">In the dialog above, the *Views\Shared* folder is selected in the left pane.</span></span> <span data-ttu-id="95d53-117">다른 폴더에 사용자 지정 레이아웃 파일을 설치한 경우에이 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-117">If you had a custom layout file in another folder, you could select it.</span></span> <span data-ttu-id="95d53-118">이 자습서의 뒷부분에 나오는 레이아웃 파일에 대 한 설명</span><span class="sxs-lookup"><span data-stu-id="95d53-118">We'll talk about the layout file later in the tutorial</span></span>

<span data-ttu-id="95d53-119">*MvcMovie\Views\HelloWorld\Index.cshtml* 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-119">The *MvcMovie\Views\HelloWorld\Index.cshtml* file is created.</span></span>

![](adding-a-view/_static/image4.png)

<span data-ttu-id="95d53-120">강조 표시 된 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-120">Add the following highlighted markup.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

<span data-ttu-id="95d53-121">마우스 오른쪽 단추로 클릭 하 고 *Index.cshtml* 파일을 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-121">Right click the *Index.cshtml* file and select **View in Browser**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="95d53-123">마우스 오른쪽 단추를 클릭할 수도 있습니다는 *Index.cshtml* 파일을 선택 **페이지 검사기에서 보기.**</span><span class="sxs-lookup"><span data-stu-id="95d53-123">You can also right click the *Index.cshtml* file and select **View in Page Inspector.**</span></span> <span data-ttu-id="95d53-124">참조는 [페이지 검사기 자습서](../../views/using-page-inspector-in-aspnet-mvc.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-124">See the [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) for more information.</span></span>

<span data-ttu-id="95d53-125">또는 응용 프로그램을 실행 하 고를 찾습니다는 `HelloWorld` 컨트롤러 (`http://localhost:xxxx/HelloWorld`).</span><span class="sxs-lookup"><span data-stu-id="95d53-125">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="95d53-126">`Index` 메서드 컨트롤러에서 많은 작업을 수행 하지 않으면 문은 단순히 실행 `return View()`, 메서드가 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿 파일을 사용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-126">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="95d53-127">ASP.NET MVC를 사용 하 여 기본값으로 사용할 보기 템플릿 파일의 이름을 명시적으로 지정 하지 않은, 때문에 *Index.cshtml* 에서 파일 보기는 *\Views\HelloWorld* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-127">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="95d53-128">아래 이미지 문자열을 보여 줍니다. &quot;우리의 보기 템플릿에서 Hello!&quot; 보기에 하드 코딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-128">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="95d53-129">잘 보입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-129">Looks pretty good.</span></span> <span data-ttu-id="95d53-130">그러나가 표시 브라우저의 제목 표시줄 &quot;인덱스-내 ASP.NET 응용 프로그램 "페이지 위쪽의 큰 링크"응용 프로그램 이름입니다."라고 표시 하 고</span><span class="sxs-lookup"><span data-stu-id="95d53-130">However, notice that the browser's title bar shows &quot;Index - My ASP.NET Appli" and the big link on the top of the page says "Application name."</span></span> <span data-ttu-id="95d53-131">브라우저 창의 만들면 작은 방식에 따라 보려면 오른쪽 위에 있는 세 개의 막대는 클릭 해야 할 수 있습니다는 하는 **홈**, **에 대 한**, **연락처**, **등록** 및 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-131">Depending on how small you make your browser window, you might need to click the three bars in the upper right to see the to the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="95d53-132">레이아웃 페이지 및 뷰 변경</span><span class="sxs-lookup"><span data-stu-id="95d53-132">Changing Views and Layout Pages</span></span>

<span data-ttu-id="95d53-133">변경 하려면 먼저는 &quot;응용 프로그램 이름&quot; 페이지 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-133">First, you want to change the &quot;Application name&quot; link at the top of the page.</span></span> <span data-ttu-id="95d53-134">텍스트를 모든 페이지에 공통적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-134">That text is common to every page.</span></span> <span data-ttu-id="95d53-135">응용 프로그램에서 모든 페이지에 표시 되지만 실제로 프로젝트에만 한 곳에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-135">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="95d53-136">이동 하는 */뷰/공유* 폴더에 **솔루션 탐색기** 엽니다는  *\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-136">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="95d53-137">이 파일은 라고는 *레이아웃 페이지* 및 다른 모든 페이지를 사용 하는 공유 폴더에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-137">This file is called a *layout page* and it's in the shared folder that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="95d53-139">레이아웃 서식 파일을 사용 하면 한 곳에서 사이트의 HTML 컨테이너 레이아웃을 지정 하 고 다음 사이트에서 여러 페이지에 걸쳐 적용 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-139">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="95d53-140">`@RenderBody()` 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-140">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="95d53-141">`RenderBody`는 사용자가 만드는 모든 보기 전용 페이지가 표시되는 자리 표시자이며 레이아웃 페이지에서 &quot;래핑됩니다&quot;.</span><span class="sxs-lookup"><span data-stu-id="95d53-141">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="95d53-142">예를 들어, 선택 하는 경우는 **에 대 한** 링크를는 *Views\Home\About.cshtml* 내 뷰가 렌더링 되는 `RenderBody` 메서드.</span><span class="sxs-lookup"><span data-stu-id="95d53-142">For example, if you select the **About** link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="95d53-143">제목 요소의 콘텐츠를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-143">Change the contents of the title element.</span></span> <span data-ttu-id="95d53-144">변경 된 [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) 레이아웃 서식 파일에 &quot;응용 프로그램 이름&quot; 를 &quot;MVC 영화&quot; 와 컨트롤러에서 `Home` 를 `Movies`합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-144">Change the [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) in the layout template from &quot;Application name&quot; to &quot;MVC Movie&quot; and the controller from `Home` to `Movies`.</span></span> <span data-ttu-id="95d53-145">전체 레이아웃 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-145">The complete layout file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

<span data-ttu-id="95d53-146">응용 프로그램을 지금 표시는 실행 &quot;MVC 영화 &quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-146">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="95d53-147">클릭는 **에 대 한** 링크 하 고 해당 페이지 표시 하는 방법을 참조 &quot;MVC 영화&quot;도 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-147">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="95d53-148">레이아웃 템플릿을 한 번 변경 사항을 적용할 수 있었습니다 하 고 사이트에 있는 모든 페이지에 새 제목의 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-148">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="95d53-149">처음 만든 경우의 *Views\HelloWorld\Index.cshtml* 파일을 다음 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-149">When we first created the *Views\HelloWorld\Index.cshtml* file, it contained the following code:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="95d53-150">위의 Razor 코드 페이지 레이아웃 페이지 명시적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-150">The Razor code above is explicitly setting the layout page.</span></span> <span data-ttu-id="95d53-151">검사는 *뷰\\_viewstart.vbhtml* 파일을 정확 하 게 동일한 Razor 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-151">Examine the *Views\\_ViewStart.cshtml* file, it contains the exact same Razor markup.</span></span> <span data-ttu-id="95d53-152">*[뷰\\_viewstart.vbhtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)*  모든 보기에서 사용할 일반적인 레이아웃을 정의 하는 파일, out 또는 해당 코드에서 제거를 설명할 수 있도록 따라서는 *Views\HelloWorld\ Index.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-152">The *[Views\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* file defines the common layout that all views will use, therefore you can comment out or remove that code from the *Views\HelloWorld\Index.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

<span data-ttu-id="95d53-153">`Layout` 속성을 사용하여 다른 레이아웃 보기를 설정하거나 레이아웃 파일을 사용하지 않도록 `null`로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-153">You can use the `Layout` property to set a different layout view, or set it to `null` so no layout file will be used.</span></span>

<span data-ttu-id="95d53-154">이제 인덱스 보기의 제목을 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-154">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="95d53-155">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="95d53-155">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="95d53-156">변경 하는 두 곳: 먼저 텍스트 표시 되는 브라우저의 제목에 찾은 다음 보조 헤더에서 (의 `<h2>` 요소).</span><span class="sxs-lookup"><span data-stu-id="95d53-156">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="95d53-157">어떤 코드에서 어떤 앱의 부분을 변경하는지 볼 수 있도록 약간 다르게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-157">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

<span data-ttu-id="95d53-158">나타내는 집합 위의 코드를 표시 하려면 HTML 제목은 `Title` 의 속성은 `ViewBag` 개체 (에 *Index.cshtml* 템플릿 보기).</span><span class="sxs-lookup"><span data-stu-id="95d53-158">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="95d53-159">다음에 유의 레이아웃 템플릿 ( *Views\Shared\\_Layout.cshtml* )에서이 값을 사용 하 여는 `<title>` 의 일환으로 요소는 `<head>` 이전에 수정한 HTML의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-159">Notice that the layout template ( *Views\Shared\\_Layout.cshtml* ) uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

<span data-ttu-id="95d53-160">이 사용 하 여 `ViewBag` 방법을 쉽게 간에 전달할 수 있습니다 다른 매개 변수 보기 템플릿과 레이아웃 파일.</span><span class="sxs-lookup"><span data-stu-id="95d53-160">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="95d53-161">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-161">Run the application.</span></span> <span data-ttu-id="95d53-162">브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-162">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="95d53-163">(브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-163">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="95d53-164">브라우저에서 Ctrl+F5 키를 눌러 로드될 서버에서 응답을 강제로 적용합니다.) 브라우저의 제목으로 만들어집니다는 `ViewBag.Title` 설정는 *Index.cshtml* 템플릿 및 추가 보기 &quot;-만든 동영상 앱&quot; 레이아웃 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-164">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="95d53-165">또한 방법을의 콘텐츠는 *Index.cshtml* 템플릿 보기 병합 된는  *\_Layout.cshtml* 템플릿 보기와 하나의 HTML 응답을 브라우저에 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-165">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="95d53-166">레이아웃 템플릿을 사용하면 응용 프로그램의 모든 페이지에 걸쳐 적용되는 변경 내용을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-166">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="95d53-167">우리의 약간의 &quot;데이터&quot; (이 경우에 &quot;우리의 보기 템플릿에서 Hello!&quot; 메시지) 하지만 하드 코딩 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-167">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="95d53-168">MVC 응용 프로그램에는 &quot;V&quot; (뷰) 구현할 수는 &quot;C&quot; (컨트롤러) 없는 &quot;M&quot; (모델) 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-168">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="95d53-169">잠시 후, 데이터베이스를 만들고 여기에서 모델 데이터를 검색 하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-169">Shortly, we'll walk through how to create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="95d53-170">컨트롤러에서 보기로 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="95d53-170">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="95d53-171">데이터베이스를 이동 하 고 모델에 대해 설명 하는, 하지만 먼저에 대해 살펴보기 보기에는 컨트롤러에서 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-171">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="95d53-172">컨트롤러 클래스는 들어오는 URL 요청에 대 한 응답으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-172">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="95d53-173">컨트롤러 클래스는 들어오는 브라우저를 처리 하는 코드를 요청, 데이터베이스에서 데이터를 검색 하 고 브라우저에 다시 전송할 응답의 유형을 결정을 내립니다 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-173">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="95d53-174">템플릿 보기를 생성 하 고 브라우저에 대 한 HTML 응답 형식을 지정 하는 컨트롤러에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-174">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="95d53-175">컨트롤러는 모든 데이터 나 개체 브라우저에 대 한 응답을 렌더링 하는 보기 템플릿에 대 한 순서에 필요한 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-175">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="95d53-176">가장 좋은 방법은: **템플릿 보기 비즈니스 논리를 수행 하거나 데이터베이스와 직접 상호 작용 안**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-176">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="95d53-177">대신 템플릿 보기에는 컨트롤러에 의해 제공 되는 데이터 에서만 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-177">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="95d53-178">이 유지 관리 &quot;문제의 분리&quot; 명확 하 고 더 쉽게 유지 관리할 테스트 가능한 코드를 유지할 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-178">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="95d53-179">현재는 `Welcome` 의 동작 메서드에 `HelloWorldController` 걸립니다 클래스는 `name` 및 `numTimes` 매개 변수 및 브라우저에 직접 값을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-179">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="95d53-180">이 응답을 문자열로 렌더링 되는 컨트롤러를 갖는 대신 보기 서식 파일을 대신 사용 하는 컨트롤러를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-180">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="95d53-181">보기 템플릿은 동적 응답을 생성합니다. 즉, 응답을 생성하기 위해 컨트롤러에서 보기로 일부 적절한 데이터를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-181">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="95d53-182">컨트롤러 템플릿 보기에는 동적 데이터 (매개 변수)를 배치 하 여이 수행할 수는 `ViewBag` 템플릿 보기에 액세스할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-182">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="95d53-183">돌아가서는 *HelloWorldController.cs* 파일을 변경는 `Welcome` 를 추가 하려면 메서드는 `Message` 및 `NumTimes` 값을 `ViewBag` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-183">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="95d53-184">`ViewBag`넣을 수 있습니다에 원하는 것을 의미 하는 동적 개체 `ViewBag` 내부 요소를 넣으면 될 때까지 개체에 정의 된 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-184">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="95d53-185">[ASP.NET MVC 모델 바인딩 시스템이](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 자동으로 명명 된 매개 변수를 매핑합니다 (`name` 및 `numTimes`) 메서드의 매개 변수에 주소 표시줄에 쿼리 문자열에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-185">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="95d53-186">전체 *HelloWorldController.cs* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-186">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

<span data-ttu-id="95d53-187">이제는 `ViewBag` 개체가 자동으로 보기에 전달 되는 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-187">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span> <span data-ttu-id="95d53-188">다음으로 시작 뷰 서식 파일이 필요 있습니다!</span><span class="sxs-lookup"><span data-stu-id="95d53-188">Next, you need a Welcome view template!</span></span> <span data-ttu-id="95d53-189">에 **빌드** 메뉴 선택 **솔루션 빌드** (또는 Ctrl + Shift + B) 프로젝트가 컴파일될 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-189">In the **Build** menu, select **Build Solution** (or Ctrl+Shift+B) to make sure the project is compiled.</span></span> <span data-ttu-id="95d53-190">마우스 오른쪽 단추로 클릭는 *Views\HelloWorld* 폴더 **추가**, 클릭 **(Razor) 레이아웃이 있는 MVC 5 뷰 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-190">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image10.png)   
  
<span data-ttu-id="95d53-191">에 **항목에 대 한 이름 지정** 대화 상자에 입력 *시작*, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-191">In the **Specify Name for Item** dialog box, enter *Welcome*, and then click **OK**.</span></span>   
  
<span data-ttu-id="95d53-192">에 **레이아웃 페이지 선택** 대화 상자에서 기본값을 적용  **\_Layout.cshtml** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-192">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image11.png)   

<span data-ttu-id="95d53-193">*MvcMovie\Views\HelloWorld\Welcome.cshtml* 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-193">The *MvcMovie\Views\HelloWorld\Welcome.cshtml* file is created.</span></span>

<span data-ttu-id="95d53-194">태그에 바꿉니다는 *Welcome.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-194">Replace the markup in the *Welcome.cshtml* file.</span></span> <span data-ttu-id="95d53-195">라고 표시 하는 루프를 만들게 &quot;Hello&quot; 사용자가 예상 횟수 만큼 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-195">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="95d53-196">전체 *Welcome.cshtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-196">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

<span data-ttu-id="95d53-197">응용 프로그램을 실행 하 고 다음 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-197">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="95d53-198">이제 데이터 URL에서 가져온 것 이며 사용 하 여 컨트롤러에 전달 되는 [모델 바인더](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-198">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="95d53-199">컨트롤러에 데이터를 패키지 한 `ViewBag` 개체 및 보기에 해당 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-199">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="95d53-200">뷰는 다음 사용자에 게 HTML로 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-200">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="95d53-201">위의 예제에서 사용 된 `ViewBag` 보기에는 컨트롤러에서 데이터를 전달 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-201">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="95d53-202">자습서의 뒷부분에서 보기 모델을 사용하여 컨트롤러에서 보기로 데이터를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-202">Later in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="95d53-203">뷰 모음 방식에 비해 데이터를 전달 하는 보기 모델 방법은 일반적으로 훨씬 많이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-203">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="95d53-204">블로그 항목을 참조 [동적 V 강력한 형식의 뷰](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-204">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span> 

<span data-ttu-id="95d53-205">하 한 종류의는 &quot;M&quot; 모델을 제외한 데이터베이스 종류 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-205">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="95d53-206">지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="95d53-206">Let's take what we've learned and create a database of movies.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="95d53-207">[이전](adding-a-controller.md)
[다음](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="95d53-207">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
