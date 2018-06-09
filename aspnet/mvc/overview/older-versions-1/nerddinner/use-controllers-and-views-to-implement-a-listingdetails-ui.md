---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 컨트롤러와 뷰를 사용 하 여 목록/세부 정보 UI 구현할 | Microsoft Docs
author: microsoft
description: 4 단계에는 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해 모델의 이점을 활용 하는 응용 프로그램에는 컨트롤러를 추가 하는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: ac3568941eeef24bd9857c5787471aadea15fc7f
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "30875736"
---
<a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="2cd72-103">컨트롤러와 뷰를 사용 하 여 목록/세부 정보 UI를 구현 하려면</span><span class="sxs-lookup"><span data-stu-id="2cd72-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>
====================
<span data-ttu-id="2cd72-104">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2cd72-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2cd72-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="2cd72-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="2cd72-106">이 무료의 4 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="2cd72-107">4 단계에는 컨트롤러 업그레이드 되었으며 수정 사이트에서 dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해 모델의 이점을 활용 하는 응용 프로그램에 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="2cd72-108">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="2cd72-109">업그레이드 되었으며 수정 4 단계: 컨트롤러와 뷰</span><span class="sxs-lookup"><span data-stu-id="2cd72-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="2cd72-110">기존 웹 프레임 워크 (클래식 ASP, PHP, ASP.NET Web Forms, 등), 들어오는 Url은 일반적으로 디스크 파일에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="2cd72-111">예: URL에 대 한 요청 같은 "/ Products.aspx" 또는 "/ Products.php" "Products.aspx" 또는 "Products.php" 파일에서 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="2cd72-112">웹 기반 MVC 프레임 워크를 약간 다른 방식으로 서버 코드에 Url을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="2cd72-113">파일에 들어오는 Url 매핑, 대신 대신 Url에 매핑되는지 클래스에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="2cd72-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="2cd72-114">이러한 클래스는 "컨트롤러" 라고 하 고 사용자 입력을 처리 하는 들어오는 HTTP 요청을 처리 해야 하는, 검색 및 데이터를 저장 및 보내기에 대 한 응답을 결정 하는 클라이언트에 다시 (HTML을 표시, 파일을 다운로드, 다른 리디렉션 URL 등)입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="2cd72-115">업그레이드 되었으며 수정 응용 프로그램에 대 한를 기본 모델을 구축 했으므로, 이제는 사이트에서 Dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해의 이점을 활용 하는 응용 프로그램에 컨트롤러를 추가 하려면 다음 단계가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="2cd72-116">DinnersController 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="2cd72-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="2cd72-117">이 웹 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 알아보고 선택 하겠습니다는 **추가-&gt;컨트롤러** 메뉴 명령 (또한이 명령을 실행할 수 있습니다이 Ctrl-M, Ctrl + C를 입력 하 여):</span><span class="sxs-lookup"><span data-stu-id="2cd72-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="2cd72-118">그러면 "컨트롤러 추가" 대화 상자를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="2cd72-119">새 컨트롤러 "DinnersController" 이름을 알아보고 "추가" 단추를 클릭 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="2cd72-120">Visual Studio는 우리의 \Controllers 디렉터리 아래에 있는 DinnersController.cs 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="2cd72-121">코드 편집기 내에서 새 DinnersController 클래스를도 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="2cd72-122">Index () 및 Details() 작업 메서드를 DinnersController 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="2cd72-123">응용 프로그램을 사용 하 여 예정 된 dinners 목록을 찾아보고 항목에 대 한 특정 세부 정보를 보려면 목록에서 모든 Dinner 클릭할 수 있도록 하는 방문자를 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="2cd72-124">응용 프로그램에서 다음 Url을 게시 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="2cd72-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="2cd72-125">**URL**</span></span> | <span data-ttu-id="2cd72-126">**용도**</span><span class="sxs-lookup"><span data-stu-id="2cd72-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="2cd72-127">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="2cd72-127">*/Dinners/*</span></span> | <span data-ttu-id="2cd72-128">예정 된 dinners는 HTML 목록 표시</span><span class="sxs-lookup"><span data-stu-id="2cd72-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="2cd72-129">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="2cd72-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="2cd72-130">데이터베이스에 dinner DinnerID 일치시킬지 URL – 내에 포함 하는 "id" 매개 변수가 나타내는 특정 저녁에 대 한 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="2cd72-131">예를 들어: /Dinners/Details/2 해당 DinnerID 값이 2 저녁에 대 한 세부 정보와 함께 HTML 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="2cd72-132">아래와 같은 DinnersController 클래스에 두 개의 공용 "작업 방법"을 추가 하 여 이러한 Url의 초기 구현 발표 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="2cd72-133">다음 업그레이드 되었으며 수정 응용 프로그램을 실행 알아보고 브라우저를 사용 하 여 호출할 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="2cd72-134">에 입력 하는 *"/" (Dinners/* URL 하면 우리의 *index ()* 메서드 실행 시를 송신할 다시 다음 응답:</span><span class="sxs-lookup"><span data-stu-id="2cd72-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="2cd72-135">에 입력 하는 *"/ 2/세부 정보/Dinners"* URL 하면 우리의 *Details()* 메서드를 실행 하 고 다음 응답을 다시 보냅니다:</span><span class="sxs-lookup"><span data-stu-id="2cd72-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="2cd72-136">하는지에 대해-어떻게 ASP.NET MVC 것을 아시나요 DinnersController 클래스를 만들고 이러한 메서드를 호출 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="2cd72-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="2cd72-137">하겠습니다를 이해 하려면 라우팅의 작동 원리에 빠르게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="2cd72-138">이해 ASP.NET MVC 라우팅</span><span class="sxs-lookup"><span data-stu-id="2cd72-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="2cd72-139">ASP.NET MVC 컨트롤러 클래스에 Url 매핑하는 방식을 제어 시 유연성을 많이 제공 하는 강력한 URL 라우팅 엔진을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="2cd72-140">ASP.NET MVC 컨트롤러 클래스를 만드는 메서드를 호출할 수 있을 뿐만 아니라 다른 변수 수 수 자동으로 URL 쿼리 문자열에서 구문 분석 하 고 있는 방법 매개 변수로 메서드에 전달 된 구성할를 선택 하는 방법를 완전히 사용자 지정할 수 있도록 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="2cd72-141">완전히 SEO (검색 엔진 최적화)에 대 한 사이트 최적화 뿐만 아니라 응용 프로그램에서 원하는 모든 URL의 구조를 게시할 수 있는 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="2cd72-142">새 ASP.NET MVC 프로젝트는 기본적으로 미리 구성 된 이미 등록 URL 라우팅 규칙 집합이 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="2cd72-143">이렇게 하면 쉽게 시작 응용 프로그램에 아무 것도 명시적으로 구성할 필요 없이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="2cd72-144">기본 라우팅 규칙 등록 – 우리는 프로젝트의 루트에 있는 "Global.asax" 파일을 두 번 클릭 하 여 열 수 있는 프로젝트의 "Application" 클래스 내에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="2cd72-145">이 클래스의 "RegisterRoutes" 메서드 내에서 기본 ASP.NET MVC 라우팅 규칙을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="2cd72-146">"경로입니다. MapRoute() "위의 메서드 호출을 컨트롤러 클래스 URL 형식을 사용 하 여 들어오는 Url을 매핑하는 기본 라우팅 규칙을 등록:" / {controller} / {action} / {id} "– 여기서"컨트롤러 "는 인스턴스화할 컨트롤러 클래스의 이름을"action"의 이름인는 한 "id"를 호출 하는 공용 메서드는 메서드에 대 한 인수로 전달할 수 있는 URL 내에 포함 하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="2cd72-147">"MapRoute()" 메서드 호출에 전달 된 세 번째 매개 변수는 URL에 존재 하지 않는 컨트롤러/작업/id 값에 사용할 기본 값의 집합 (컨트롤러 동작 = "Home", "Index", Id = = "").</span><span class="sxs-lookup"><span data-stu-id="2cd72-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="2cd72-148">다음은 이러한 기본값을 사용 하 여 Url의 다양 한 방법을 보여 주는 테이블 매핑된 "<em>/ {컨트롤러} / {action} / {id}"</em>경로 규칙:</span><span class="sxs-lookup"><span data-stu-id="2cd72-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="2cd72-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="2cd72-149">**URL**</span></span> | <span data-ttu-id="2cd72-150">**컨트롤러 클래스**</span><span class="sxs-lookup"><span data-stu-id="2cd72-150">**Controller Class**</span></span> | <span data-ttu-id="2cd72-151">**동작 메서드**</span><span class="sxs-lookup"><span data-stu-id="2cd72-151">**Action Method**</span></span> | <span data-ttu-id="2cd72-152">**전달 된 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="2cd72-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2cd72-153">*/Dinners/Details/2*</span><span class="sxs-lookup"><span data-stu-id="2cd72-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="2cd72-154">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2cd72-154">DinnersController</span></span> | <span data-ttu-id="2cd72-155">Details(id)</span><span class="sxs-lookup"><span data-stu-id="2cd72-155">Details(id)</span></span> | <span data-ttu-id="2cd72-156">id=2</span><span class="sxs-lookup"><span data-stu-id="2cd72-156">id=2</span></span> |
| <span data-ttu-id="2cd72-157">*/Dinners/Edit/5*</span><span class="sxs-lookup"><span data-stu-id="2cd72-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="2cd72-158">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2cd72-158">DinnersController</span></span> | <span data-ttu-id="2cd72-159">Edit(id)</span><span class="sxs-lookup"><span data-stu-id="2cd72-159">Edit(id)</span></span> | <span data-ttu-id="2cd72-160">id=5</span><span class="sxs-lookup"><span data-stu-id="2cd72-160">id=5</span></span> |
| <span data-ttu-id="2cd72-161">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="2cd72-161">*/Dinners/Create*</span></span> | <span data-ttu-id="2cd72-162">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2cd72-162">DinnersController</span></span> | <span data-ttu-id="2cd72-163">Create)</span><span class="sxs-lookup"><span data-stu-id="2cd72-163">Create()</span></span> | <span data-ttu-id="2cd72-164">N/A</span><span class="sxs-lookup"><span data-stu-id="2cd72-164">N/A</span></span> |
| <span data-ttu-id="2cd72-165">*/Dinners*</span><span class="sxs-lookup"><span data-stu-id="2cd72-165">*/Dinners*</span></span> | <span data-ttu-id="2cd72-166">DinnersController</span><span class="sxs-lookup"><span data-stu-id="2cd72-166">DinnersController</span></span> | <span data-ttu-id="2cd72-167">Index)</span><span class="sxs-lookup"><span data-stu-id="2cd72-167">Index()</span></span> | <span data-ttu-id="2cd72-168">N/A</span><span class="sxs-lookup"><span data-stu-id="2cd72-168">N/A</span></span> |
| <span data-ttu-id="2cd72-169">*/Home*</span><span class="sxs-lookup"><span data-stu-id="2cd72-169">*/Home*</span></span> | <span data-ttu-id="2cd72-170">HomeController</span><span class="sxs-lookup"><span data-stu-id="2cd72-170">HomeController</span></span> | <span data-ttu-id="2cd72-171">Index)</span><span class="sxs-lookup"><span data-stu-id="2cd72-171">Index()</span></span> | <span data-ttu-id="2cd72-172">N/A</span><span class="sxs-lookup"><span data-stu-id="2cd72-172">N/A</span></span> |
| */* | <span data-ttu-id="2cd72-173">HomeController</span><span class="sxs-lookup"><span data-stu-id="2cd72-173">HomeController</span></span> | <span data-ttu-id="2cd72-174">Index)</span><span class="sxs-lookup"><span data-stu-id="2cd72-174">Index()</span></span> | <span data-ttu-id="2cd72-175">N/A</span><span class="sxs-lookup"><span data-stu-id="2cd72-175">N/A</span></span> |

<span data-ttu-id="2cd72-176">기본 값을 표시 하는 마지막 3 개의 행 (컨트롤러 = 가정, 작업 = 인덱스, Id = "") 사용 하 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="2cd72-177">"Index" 메서드 하나를 지정 하지 않으면 기본 동작 이름으로 등록 되므로 "/ Dinners" 및 "/ 홈" Url 원인 index () 동작 메서드를 해당 컨트롤러 클래스에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="2cd72-178">지정 하지 않고 "홈" 컨트롤러가 기본 컨트롤러로 등록 된, 하기 때문에 "/" URL HomeController 만들어야 하 고 index () 동작 메서드를 호출할 수 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="2cd72-179">이러한 기본 URL 라우팅 규칙, 마음에 들지 않으면 좋은 소식 쉽게 변경-바로 위의 RegisterRoutes 메서드 내에서 편집할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="2cd72-180">이 업그레이드 되었으며 수정 응용 프로그램에 대 한 하지만 기본 URL 라우팅 규칙을 변경 하려면 않겠습니다 – 대신 있습니다 사용할 것으로-됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="2cd72-181">우리의 DinnersController에서 DinnerRepository를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2cd72-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="2cd72-182">보겠습니다 DinnersController의 현재 구현은 이제 대체 index () 및 Details() 동작 메서드를 예제의 모델을 사용 하는 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="2cd72-183">동작을 구현 하려면 앞서 작성 DinnerRepository 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="2cd72-184">에서는 "NerdDinner.Models" 네임 스페이스를 참조 하는 "using" 문을 추가 하 여 시작 하 고 DinnerController 클래스에 필드로 취급 DinnerRepository의 인스턴스를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="2cd72-185">나중에이 장의에서는 합니다 "종속성 주입"의 개념을 소개 하 고 우리의 DinnerRepository의 인스턴스를 방금 만들겠습니다 이제 테스트 – 하지만 권한에 대 한 또 다른 방법은 더 나은 단위 수 있도록 DinnerRepository에 대 한 참조를 가져오려면이 컨트롤러에 대 한 표시 아래와 같은 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="2cd72-186">이제 검색 된 데이터 모델 개체를 사용 하 여 HTML 응답을 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="2cd72-187">이 컨트롤러와 뷰를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2cd72-187">Using Views with our Controller</span></span>

<span data-ttu-id="2cd72-188">조합 HTML을 사용 하 여이 작업 메서드 내에서 코드를 작성할 수 있지만 *Response.Write()* 클라이언트로 다시 전송할는 접근 방식을 통제 하기 힘들어집니다 매우 신속 하 게 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="2cd72-189">훨씬 더 나은 방법은 응용 프로그램 및 우리의 DinnersController 작업 메서드 내부의 데이터 논리를 수행 하 고 그런 다음 HTML 표현을 출력 하는 일을 담당 하는 별도 "보기" 서식 파일에 대 한 HTML 응답을 렌더링 하는 데 필요한 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="2cd72-190">잠시 후에 볼 수 있겠지만, "view" 템플릿은 일반적으로 포함 된 렌더링 코드와 HTML 태그를 포함 하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="2cd72-191">우리의 뷰 렌더링에서 트 컨트롤러 논리를 분리는 몇 가지 큰 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="2cd72-192">특히 응용 프로그램 코드와 UI 서식을/렌더링 코드 사이의 명확한 "문제의 분리" 적용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="2cd72-193">이렇게 하면 훨씬 쉽게 격리에 대 한 단위 테스트 응용 프로그램 논리를 UI 렌더링 논리에서.</span><span class="sxs-lookup"><span data-stu-id="2cd72-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="2cd72-194">예제에서는 쉽게 나중에 응용 프로그램 코드를 변경 하지 않고도 UI 렌더링 서식 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="2cd72-195">및 개발자와 디자이너가 프로젝트에 함께 공동 작업을 쉽게 만들 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="2cd72-196">DinnersController 클래스 뷰 템플릿을 사용 하 여 반환 형식이 "void" 대신 "ActionResult"의 반환 형식을 갖도록 하는 것과 두 개의 작업 메서드 메서드 시그니처를 변경 하 여 HTML UI 응답 반송 한다고 나타내는 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="2cd72-197">그런 다음를 호출할 수 있습니다는 *View()* 다시 반환 하는 컨트롤러 기본 클래스에서 도우미 메서드에 다음과 유사한 "ViewResult" 개체:</span><span class="sxs-lookup"><span data-stu-id="2cd72-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="2cd72-198">시그니처는 *View()* 위에 사용 하 여 도우미 메서드는 아래 같습니다:</span><span class="sxs-lookup"><span data-stu-id="2cd72-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="2cd72-199">첫 번째 매개 변수는 *View()* 도우미 메서드는 HTML 응답을 렌더링 하는 데 원하는 보기 템플릿 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="2cd72-200">두 번째 템플릿 보기 HTML 응답을 렌더링 하는 데 필요한 데이터를 포함 하는 모델 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="2cd72-201">우리 index () 작업 메서드 내에서 호출 된 *View()* 도우미 메서드와 dinners "Index" 뷰 템플릿을 사용 하는 HTML 목록이 렌더링 하려고 한다는 것을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="2cd72-202">전달 템플릿 보기 Dinner에서 목록을 생성 하는 개체 시퀀스의:</span><span class="sxs-lookup"><span data-stu-id="2cd72-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="2cd72-203">우리의 Details() 작업 메서드 내에서 URL 내에서 제공 하는 id를 사용 하 여 Dinner 개체를 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="2cd72-204">유효한 Dinner 이라고 발견 되는 *View()* 도우미 메서드를 "Details" 뷰 템플릿을 사용 하 여 검색 된 Dinner 개체를 렌더링 하도록 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="2cd72-205">म 렌더링 Dinner "NotFound" 뷰 템플릿을 사용 하 여 존재 하지 유용한 오류 메시지가 잘못 된 dinner 요청 된 경우 (및 오버 로드 된 버전의는 *View()* 템플릿 이름 원활한 도우미 메서드 ):</span><span class="sxs-lookup"><span data-stu-id="2cd72-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="2cd72-206">이제 템플릿 보기 "NotFound", "Details" 및 "인덱스"를 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="2cd72-207">템플릿 "NotFound" 보기를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="2cd72-208">요청 된 dinner를 찾을 수 없습니다 되었음을 나타내는 오류 메시지가 표시 하는 "NotFound" 보기 템플릿 – 구현부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="2cd72-209">म 합니다 컨트롤러 작업 메서드 내에서 텍스트 커서를 배치 하 여 새 보기 템플릿을 만들 다음 마우스 오른쪽 단추로 클릭 하 고 "추가" 메뉴 명령을 선택 (Ctrl-M, Ctrl + V를 입력 하 여이 명령은 또한 실행 수):</span><span class="sxs-lookup"><span data-stu-id="2cd72-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="2cd72-210">이 옵션은 아래와 같은 "뷰 추가" 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="2cd72-211">대화 상자에서 만들 뷰 이름을 미리 채워집니다 기본적으로 일치 하는 동작 메서드의 이름을 커서 시점의 대화 상자에 (이 경우 "Details") 시작 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="2cd72-212">"NotFound" 서식 파일을 먼저 구현 하고자 하기 때문에이 뷰 이름을 재정의 알아보고 "NotFound" 대신 되도록 설정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="2cd72-213">"추가" 단추를 클릭 Visual Studio 내에 만들 새 템플릿 "NotFound.aspx" 보기에는 "\Views\Dinners" 디렉터리 (생성 된 디렉터리는 존재 하지 않는 경우):</span><span class="sxs-lookup"><span data-stu-id="2cd72-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="2cd72-214">또한이 새 "NotFound.aspx" 보기 서식 파일을 코드 편집기에는 것이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="2cd72-215">기본적으로 템플릿 보기는 두 개의 "콘텐츠 영역" 내용 및 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="2cd72-216">첫 번째 "제목" HTML 페이지의 다시 전송를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="2cd72-217">두 번째 다시 전송 HTML 페이지의 "기본 콘텐츠"를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="2cd72-218">템플릿 우리의 "NotFound" 보기를 구현 하려면 몇 가지 기본 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="2cd72-219">에서는 다음 직접 시도해 볼 수 브라우저 내에서.</span><span class="sxs-lookup"><span data-stu-id="2cd72-219">We can then try it out within the browser.</span></span> <span data-ttu-id="2cd72-220">보겠습니다 이렇게 하려면 요청에서 *"/ 9999/Dinners/세부 정보"* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="2cd72-221">현재 데이터베이스에 존재 하지 않는 하 우리의 "NotFound" 보기 템플릿을 렌더링 하지 우리의 DinnersController.Details() 동작 메서드가 dinner 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="2cd72-222">한 가지 위의 스크린샷에 나와 있는 알 수입니다이 기본 보기 템플릿 html을 화면에 기본 콘텐츠를 둘러싸는 bunch를 상속 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="2cd72-223">사이트에서 모든 보기에 대해 일관 된 레이아웃을 적용할 수 있도록 해 주는 "마스터 페이지" 템플릿을 사용 하 여는 우리의 보기 템플릿을 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="2cd72-224">마스터 페이지이 자습서의 뒷부분에 나오는 부분에 더 많은 작동 방식에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="2cd72-225">템플릿 "Details" 보기를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="2cd72-226">단일 Dinner 모델에 대 한 HTML을 생성 하는 "Details" 뷰 템플릿에 – 이제 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="2cd72-227">म 합니다 우리의 텍스트 커서 Details 작업 메서드 내에서이 작업을 수행 하 고 마우스 오른쪽 단추로 클릭 하 고 "추가" 메뉴 명령을 선택 (또는 Ctrl-M, Ctrl + V를 눌러):</span><span class="sxs-lookup"><span data-stu-id="2cd72-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="2cd72-228">이 "뷰 추가" 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="2cd72-229">기본 뷰 이름 ("정보") 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="2cd72-230">도 대화 상자에서 "강력한 형식의 뷰 만들기" 확인란을 선택 하 고 보기에는 컨트롤러에서 전달 하는 모델 유형에의 이름 (combobox 드롭다운을 사용 하 여) 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="2cd72-231">이 보기에 대해 Dinner 개체를 전달 (이 형식에 대 한 정규화 된 이름이: "NerdDinner.Models.Dinner"):</span><span class="sxs-lookup"><span data-stu-id="2cd72-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="2cd72-232">여기서 "빈 보기"를 만들려면 선택한, 이전 서식 파일과 달리이 시간에 자동으로 선택 됩니다 "스 캐 폴드" "Details" 템플릿을 사용 하 여 보기.</span><span class="sxs-lookup"><span data-stu-id="2cd72-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="2cd72-233">위의 대화 상자에서 "콘텐츠 보기" 드롭다운을 변경 하 여 다음과 같이 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="2cd72-234">"스 캐 폴딩" Dinner 개체를 전달 하는 것에 따라 세부 정보 보기 템플릿 우리의의 구현이 초기에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="2cd72-235">이 보기 템플릿 구현에 신속 하 게 시작 하는 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="2cd72-236">"추가" 단추를 클릭 Visual Studio 내에 만들 새 "Details.aspx" 보기 템플릿 파일을 수행해 줍니다 우리의 "\Views\Dinners" 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="2cd72-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="2cd72-237">또한이 새 "Details.aspx" 보기 서식 파일을 코드 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="2cd72-238">저녁 모델을 기반으로 세부 정보 보기의 초기 스 캐 폴드 구현을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="2cd72-239">스 캐 폴딩 엔진.NET 리플렉션을 사용 하 여, 전달 된 클래스에 노출 된 공용 속성을 보고 하 고 찾은 각 형식에 따라 적절 한 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="2cd72-240">요청할 수는 *"/ 1/세부 정보/Dinners"* URL을 브라우저에서이 "details" 스 캐 폴드 구현 어떻게 나타나는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="2cd72-241">이 URL을 사용 하 여 우리가 처음 만들 때 수동으로 데이터베이스에 추가한 dinners 중 하나가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="2cd72-242">이 us 실행 되 고 신속 하 게 가져오고 우리의 Details.aspx 뷰가의 초기 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="2cd72-243">그런 다음 이동 하 고 우리의 만족도 UI를 사용자 지정 하도록 조정할 수 있습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="2cd72-244">더욱 긴밀 하 게 Details.aspx 서식 파일에서 살펴볼 때는 것에 정적 HTML 포함으로 렌더링 코드를 삽입 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="2cd72-245">&lt;% %&gt; 코드 너 템플릿 보기에서 렌더링할 때 코드를 실행 하 고 &lt;% = %&gt; 코드 너 그 안에 포함 된 코드를 실행 하 고 다음 서식 파일의 출력 스트림에 결과 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="2cd72-246">"모델" 강력한 형식의 속성을 사용 하 여 컨트롤러에서 전달 된 "Dinner" 모델 개체에 액세스 하는 뷰 내에서 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="2cd72-247">Visual Studio 측정할 전체 코드 intellisense 편집기 내에서이 "Model" 속성에 액세스할 때:</span><span class="sxs-lookup"><span data-stu-id="2cd72-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="2cd72-248">우리의 마지막 세부 정보 보기 템플릿에 대 한 소스 아래 모양이 되도록 몇 가지 변경을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="2cd72-249">액세스할 때의 *"/ 1/세부 정보/Dinners"* URL 다시 하므로 이제 다음과 유사한 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="2cd72-250">템플릿 "Index" 보기를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="2cd72-251">생성 하는 예정 된 Dinners 목록이 "Index" 보기 템플릿 – 이제 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="2cd72-252">이 인덱스 작업 메서드 내에서 텍스트 커서를 놓은 다음 마우스 오른쪽 단추로 합니다 म 클릭 하 고 "추가" 메뉴 명령을 선택 (또는 Ctrl-M, Ctrl + V를 눌러) 할 일입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="2cd72-253">"뷰 추가" 대화 상자 내에서 "Index" 라는 보기 템플릿을 유지 알아보고 "강력한 형식의 뷰 만들기" 확인란을 선택 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="2cd72-254">이 시간에서는 자동으로 "List" 보기 서식 파일을 생성 하 고 "NerdDinner.Models.Dinner" 모델 형식으로 뷰에 전달 선택를 선택 합니다 (있는 스 캐 폴딩 하는 것으로 가정 하는 뷰 추가 대화 상자의 하면 "목록" 생성 나타낸 것 때문에 전달 Dinner 개체 시퀀스의 컨트롤러에서 뷰로):</span><span class="sxs-lookup"><span data-stu-id="2cd72-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="2cd72-255">"추가" 단추를 클릭 Visual Studio는을 수행해 줍니다 새 "Index.aspx" 보기 템플릿 파일을 우리의 "\Views\Dinners" 디렉터리 내에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="2cd72-256">것은 "스 캐 폴드" 내 뷰에 전달 Dinners의 HTML 테이블 목록은를 제공 하는 초기 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="2cd72-257">된 액세스 권한 및 응용 프로그램을 실행할 때의 *"/" (Dinners/* 같이 URL dinners 목록의 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="2cd72-258">위의 테이블 솔루션 목록 Dinner 나열 마주보는 소비자에 대해 원하는 대로 매우이 Dinner 데이터 –의 표 형식 레이아웃에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="2cd72-259">Index.aspx 뷰 템플릿을 업데이트 하 고 더 적은 열 데이터를 나열 하 고 사용 하도록 수정 수는 &lt;ul&gt; 아래 코드를 사용 하 여 테이블 대신이 렌더링 하는 요소:</span><span class="sxs-lookup"><span data-stu-id="2cd72-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="2cd72-260">부문의 각 dinner 반복 것으로 위의 foreach 문 내에서 "var" 키워드를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="2cd72-261">C# 3.0에 잘 하는 것 이라는 dinner 개체가 런타임에 바인딩된 임을 의미 "var"를 사용 하 여 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="2cd72-262">대신 컴파일러가 "Model" 강력한 형식의 속성에 대해 형식 유추를 사용 하 고 있는지 의미 (가 형식의 "a b l e&lt;Dinner&gt;") 및 로컬 "dinner" 변수 얻을 수 있는 전체 즉 Dinner 유형 –으로 컴파일 intellisense 및 컴파일 시간에 대 한 코드 블록 내에서 확인 하는 중:</span><span class="sxs-lookup"><span data-stu-id="2cd72-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="2cd72-263">새로 고침을 누릅니다 우리는 */Dinners* 아래 우리의 업데이트 된 보기 이제 다음과 같은 브라우저에서 URL:</span><span class="sxs-lookup"><span data-stu-id="2cd72-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="2cd72-264">이 더 나은 – 찾고 하지만 아직 완전히 준비 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="2cd72-265">수행할 마지막 단계는 최종 사용자가 목록에서 개별 Dinners를 클릭 하 고에 대 한 세부 정보를 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="2cd72-266">이 우리의 DinnersController 세부 정보 동작 메서드에 연결 되는 HTML 하이퍼링크 요소를 렌더링 하 여 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="2cd72-267">두 가지 방법 중 하나에 인덱스, 뷰 내의이 하이퍼링크를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="2cd72-268">첫 번째는 HTML을 수동으로 만드는 &lt;는&gt; 포함에서는 아래와 같은 요소 &lt;% %&gt; 내에서 차단 된 &lt;는&gt; HTML 요소:</span><span class="sxs-lookup"><span data-stu-id="2cd72-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="2cd72-269">프로그래밍 방식으로 HTML을 만들기를 지 원하는 ASP.NET MVC에서 기본 제공 "Html.ActionLink()" 도우미 메서드를 활용 하는 다른 방법은 사용할 수는 &lt;는&gt; 에 다른 동작 메서드에 연결 하는 요소는 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="2cd72-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="2cd72-270">Html.ActionLink() 도우미 메서드를 사용 하는 첫 번째 매개 변수가 표시할 링크 텍스트입니다 (이 경우 제목 dinner의)에서 두 번째 매개 변수는 컨트롤러 동작 이름 (이 예제의 Details 메서드)에 대 한 링크를 생성 하려고 하 고 세 번째 매개 변수는 집합 작업 (속성 이름/값을 가진 익명 형식으로 구현 됨)로 전달할 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="2cd72-271">이 경우 여기서 지정 하는, 연결 하 고 ASP.NET MVC에서 규칙 기본 URL 라우팅 이므로 dinner의 "id" 매개 변수 "{Controller} / {Action} / {id}" Html.ActionLink() 도우미 메서드는 다음과 같은 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="2cd72-272">우리의 Index.aspx 보기에 대 한 Html.ActionLink() 도우미 메서드 접근 방식을 사용 알아보고 각 dinner 적절 한 세부 정보 URL에 목록 링크에 있는 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="2cd72-273">및 도달할 때 이제는 */Dinners* dinner 목록 아래 다음과 같은 URL:</span><span class="sxs-lookup"><span data-stu-id="2cd72-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="2cd72-274">목록에서 Dinners 중 하나를 클릭 하는 경우 항목에 대 한 자세한 내용을 보려면 이동할 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="2cd72-275">명명 규칙 기반 및 \Views 디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="2cd72-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="2cd72-276">기본적으로 ASP.NET MVC 응용 프로그램 템플릿 보기를 확인할 때 구조 이름 지정 규칙 기반 디렉터리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="2cd72-277">개발자를 정규화 위치 경로 컨트롤러 클래스 내에서 뷰를 참조할 때 필요가 없도록 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="2cd72-278">기본적으로 ASP.NET MVC 뷰 템플릿 파일 내에서 찾습니다는 * \Views\[ControllerName]\* 응용 프로그램 아래 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-278">By default ASP.NET MVC will look for the view template file within the *\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="2cd72-279">예를 들어 지금까지 작업 템플릿 세 가지 보기를 명시적으로 참조 DinnersController 클래스 –: "Index", "Details" 및 "NotFound"입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="2cd72-280">ASP.NET MVC에서는 기본적으로 찾습니다. 내에서 이러한 보기는 *\Views\Dinners* 우리의 응용 프로그램 루트 디렉터리 아래에 있는 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="2cd72-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="2cd72-281">어떻게 없어 위에 현재 프로젝트 내에서 세 가지 컨트롤러 클래스 (DinnersController, HomeController 및 AccountController-마지막 두 프로젝트를 만들 때 기본적으로 추가 된), 세 가지 하위 디렉터리 (마다 하나씩 되며 컨트롤러) \Views 디렉터리 내에서.</span><span class="sxs-lookup"><span data-stu-id="2cd72-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="2cd72-282">홈 및 계정 컨트롤러에서 참조 하는 뷰에 해당에서 보기 템플릿을 자동으로 해결 됩니다 *\Views\Home* 및 *\Views\Account* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="2cd72-283">*\Views\Shared* 하위 디렉터리를 다시 사용 되는 응용 프로그램 내의 여러 컨트롤러에서 템플릿 보기를 저장 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="2cd72-284">먼저 내에서 확인 ASP.NET MVC 템플릿 보기를 확인 하려고 시도 하는 경우는 *\Views\[컨트롤러]* 특정 디렉터리 템플릿 보기를 찾을 수 없는 경우 발생 표시 됩니다 내에서 *\Views\ 공유* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="2cd72-285">개별 보기 템플릿 이름 지정에 관한, 권장된 지침은 보기 템플릿 렌더링를 일으킨 작업 메서드와 동일한 이름을 공유 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="2cd72-286">예를 들어 우리의 "Index" 위에 동작 메서드가 뷰 결과 렌더링 하 "Index" 보기를 사용 및 "Details 라는" 작업 메서드 "Details" 보기를 사용 하 여 결과 렌더링 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="2cd72-287">따라서 쉽게 각 작업과 연결 된 것은 신속 하 게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="2cd72-288">개발자가 명시적으로 템플릿 보기에는 컨트롤러에서 호출 되는 동작 메서드가와 동일한 이름을 보기 템플릿 이름을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="2cd72-289">대신 방금에 전달할 수는 모델 개체 "View()" 도우미 메서드 (하지 않고 뷰 이름 지정) 및 ASP.NET MVC를 사용 하 여 자동으로 유추 됩니다는 *\Views\[ControllerName]\[ActionName]* 렌더링 하는 디스크에 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="2cd72-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="2cd72-290">따라서 약간, 컨트롤러 코드를 정리 하 고 코드에서 두 번 이름 중복을 피하기 위해 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="2cd72-291">위의 코드는 좋은 Dinner 등록/정보를 구현 하는 데 필요한 모든 사이트에 대 한 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="2cd72-292">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2cd72-292">Next Step</span></span>

<span data-ttu-id="2cd72-293">검색 환경 구축 멋진 Dinner를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="2cd72-294">CRUD (만들기, 읽기, 업데이트, 삭제) 데이터를 편집할 수 있도록 지원 이제 하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2cd72-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2cd72-295">[이전](build-a-model-with-business-rule-validations.md)
> [다음](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="2cd72-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
