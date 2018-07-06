---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 컨트롤러 및 뷰 목록/세부 정보 UI 구현를 사용 하 여 | Microsoft Docs
author: microsoft
description: 4 단계 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해 모델을 활용 하는 응용 프로그램에는 컨트롤러를 추가 하는 방법을 표시 하는 중...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 7a0a057efb52a869a72722b24d7283cb883db858
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838587"
---
<a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="0cfe3-103">컨트롤러 및 뷰를 사용 하 여 목록/세부 정보 UI 구현</span><span class="sxs-lookup"><span data-stu-id="0cfe3-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>
====================
<span data-ttu-id="0cfe3-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0cfe3-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="0cfe3-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="0cfe3-106">이 무료의 4 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="0cfe3-107">4 단계 NerdDinner 사이트에서 dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해 모델을 활용 하는 응용 프로그램에는 컨트롤러를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="0cfe3-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="0cfe3-109">NerdDinner 4 단계: 컨트롤러 및 보기</span><span class="sxs-lookup"><span data-stu-id="0cfe3-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="0cfe3-110">기존 웹 프레임 워크 (클래식 ASP, PHP, ASP.NET Web Forms, 등)를 들어오는 Url은 일반적으로 디스크 파일에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="0cfe3-111">예를 들어:와 같은 URL에 대 한 요청을 "/ 대" 하거나 "/ Products.php" "Products.aspx" 또는 "Products.php" 파일에서 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="0cfe3-112">웹 기반 MVC 프레임 워크를 약간 다른 방식으로 서버 코드에 Url을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="0cfe3-113">대신 들어오는 Url 파일을 대신 매핑할 Url 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="0cfe3-114">이러한 클래스는 "컨트롤러" 라고 하 고 사용자 입력을 처리 하는 들어오는 HTTP 요청을 처리 하는 일을 담당 하는 클라이언트 다시 검색, 데이터 저장 및 전송에 대 한 응답 결정 (HTML 표시 파일을 다운로드, 다른 리디렉션 URL, 등)입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="0cfe3-115">에서는 기본 모델을 NerdDinner 응용 프로그램을 작성 했으므로 다음 단계 컨트롤러의 사이트에서 Dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해 활용 하는 응용 프로그램에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="0cfe3-116">DinnersController 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="0cfe3-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="0cfe3-117">에서는 웹 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 하 고 다음을 선택 합니다 **추가-&gt;컨트롤러** 메뉴 명령 (Ctrl-M, Ctrl + C를 입력 하 여이 명령을 실행 수):</span><span class="sxs-lookup"><span data-stu-id="0cfe3-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="0cfe3-118">"컨트롤러 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="0cfe3-119">새 컨트롤러 "DinnersController" 이름을 하 고 "추가" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="0cfe3-120">Visual Studio는 추가한 우리의 \Controllers 디렉터리 DinnersController.cs 파일:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="0cfe3-121">코드 편집기 내에서 새 DinnersController 클래스도 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="0cfe3-122">Index () 및 작업 메서드 Details() DinnersController 클래스에 추가</span><span class="sxs-lookup"><span data-stu-id="0cfe3-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="0cfe3-123">응용 프로그램을 사용 하 여 향후 dinners 목록을 검색에 대 한 특정 세부 정보를 보려면 목록에서 저녁 식사를 클릭할 수 있도록 하는 방문자를 사용 하도록 설정 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="0cfe3-124">응용 프로그램에서 다음 Url을 게시 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="0cfe3-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="0cfe3-125">**URL**</span></span> | <span data-ttu-id="0cfe3-126">**용도**</span><span class="sxs-lookup"><span data-stu-id="0cfe3-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="0cfe3-127">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="0cfe3-127">*/Dinners/*</span></span> | <span data-ttu-id="0cfe3-128">예정 된 dinners는 HTML 목록 표시</span><span class="sxs-lookup"><span data-stu-id="0cfe3-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="0cfe3-129">*/Dinners/Details/[id]*</span><span class="sxs-lookup"><span data-stu-id="0cfe3-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="0cfe3-130">데이터베이스의를 저녁 식사의 DinnerID 일치 하는 URL 내에 포함 하는 "id" 매개 변수가 가리키는 특정 dinner에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="0cfe3-131">예를 들어: /Dinners/Details/2 DinnerID 값인 2 저녁에 대 한 정보를 사용 하 여 HTML 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="0cfe3-132">이러한 Url의 초기 구현을 아래와 같은 DinnersController 클래스에 두 개의 공용 "작업 방법"을 추가 하 여 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="0cfe3-133">에서는 그런 다음 NerdDinner 응용 프로그램을 실행 하 고는 브라우저를 사용 하 여 이러한 명령을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="0cfe3-134">입력 된 *"/"이 (Dinners/* URL 하면 우리의 *index ()* 메서드를 실행 하며 다시 다음과 같은 응답이 전송 됩니다:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="0cfe3-135">에 입력 합니다 *"/ Dinners/세부 정보/2"* URL 하면 우리 *Details()* 를 실행 하 고 다음 응답을 보내는 방법:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="0cfe3-136">궁금할 수 있습니다-방법을 ASP.NET MVC 아십니까 DinnersController 클래스를 만들고 해당 메서드를 호출 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="0cfe3-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="0cfe3-137">보겠습니다 알아 라우팅 작동 방법을 빠르게 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="0cfe3-138">이해 ASP.NET MVC 라우팅</span><span class="sxs-lookup"><span data-stu-id="0cfe3-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="0cfe3-139">ASP.NET MVC에는 다양 한 Url을 컨트롤러 클래스 매핑되는 방식을 제어할 수 있는 유연성을 제공 하는 강력한 URL 라우팅 엔진을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="0cfe3-140">완전히 ASP.NET MVC 컨트롤러 클래스를 호출할 수 있을 뿐 아니라 다른 변수 수 수 자동으로 URL 쿼리 문자열에서 구문 분석 하 고 방법을 매개 변수로 메서드에 전달 된 구성 하는 메서드를 만듭니다를 선택 하는 방법을 사용자 지정할 수 있도록 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="0cfe3-141">완전히 SEO (검색 엔진 최적화)에 대 한 사이트 최적화 뿐만 아니라 응용 프로그램에서 원하는 모든 URL 구조를 게시 하는 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="0cfe3-142">기본적으로 새 ASP.NET MVC 프로젝트는 미리 구성 된 집합이 이미 등록 URL 라우팅 규칙을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="0cfe3-143">쉽게 시작 응용 프로그램에서 명시적으로 아무 것도 구성 하지 않고도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="0cfe3-144">기본 라우팅 규칙 등록 – 프로젝트의 루트에 "Global.asax" 파일을 두 번 클릭 하 여 열 수에서는 프로젝트의 "Application" 클래스 내에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="0cfe3-145">기본 ASP.NET MVC 라우팅 규칙은이 클래스의 "RegisterRoutes" 메서드 내에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="0cfe3-146">"경로입니다. MapRoute() "위 메서드 호출에는 들어오는 Url URL 형식을 사용 하 여 컨트롤러 클래스에 매핑되는 기본 라우팅 규칙을 등록:" / {컨트롤러} / {action} / {id} "– 인스턴스화 컨트롤러 클래스의 이름은"controller"위치"action "은 이름의 공용 메서드, 및 "id"를 호출 하는 메서드에 인수로 전달 될 수 있는 URL 내에 포함 된 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="0cfe3-147">"MapRoute()" 메서드 호출에 전달 된 세 번째 매개 변수를 URL에 없는 컨트롤러/작업/id 값에 사용할 기본 값의 집합이 (컨트롤러 작업 "홈" = = "Index", Id = "").</span><span class="sxs-lookup"><span data-stu-id="0cfe3-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="0cfe3-148">다음 Url의 다양 한 방법을 보여 주는 테이블 기본값을 사용 하 여 매핑된은 "<em>/ {컨트롤러} / {action} / {id}"</em>경로 규칙:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="0cfe3-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="0cfe3-149">**URL**</span></span> | <span data-ttu-id="0cfe3-150">**컨트롤러 클래스**</span><span class="sxs-lookup"><span data-stu-id="0cfe3-150">**Controller Class**</span></span> | <span data-ttu-id="0cfe3-151">**동작 메서드**</span><span class="sxs-lookup"><span data-stu-id="0cfe3-151">**Action Method**</span></span> | <span data-ttu-id="0cfe3-152">**전달 된 매개 변수**</span><span class="sxs-lookup"><span data-stu-id="0cfe3-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0cfe3-153">*/Dinners/Details/2*</span><span class="sxs-lookup"><span data-stu-id="0cfe3-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="0cfe3-154">DinnersController</span><span class="sxs-lookup"><span data-stu-id="0cfe3-154">DinnersController</span></span> | <span data-ttu-id="0cfe3-155">Details(id)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-155">Details(id)</span></span> | <span data-ttu-id="0cfe3-156">id=2</span><span class="sxs-lookup"><span data-stu-id="0cfe3-156">id=2</span></span> |
| <span data-ttu-id="0cfe3-157">*/Dinners/Edit/5*</span><span class="sxs-lookup"><span data-stu-id="0cfe3-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="0cfe3-158">DinnersController</span><span class="sxs-lookup"><span data-stu-id="0cfe3-158">DinnersController</span></span> | <span data-ttu-id="0cfe3-159">Edit(id)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-159">Edit(id)</span></span> | <span data-ttu-id="0cfe3-160">id=5</span><span class="sxs-lookup"><span data-stu-id="0cfe3-160">id=5</span></span> |
| <span data-ttu-id="0cfe3-161">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="0cfe3-161">*/Dinners/Create*</span></span> | <span data-ttu-id="0cfe3-162">DinnersController</span><span class="sxs-lookup"><span data-stu-id="0cfe3-162">DinnersController</span></span> | <span data-ttu-id="0cfe3-163">Create)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-163">Create()</span></span> | <span data-ttu-id="0cfe3-164">N/A</span><span class="sxs-lookup"><span data-stu-id="0cfe3-164">N/A</span></span> |
| <span data-ttu-id="0cfe3-165">*/Dinners*</span><span class="sxs-lookup"><span data-stu-id="0cfe3-165">*/Dinners*</span></span> | <span data-ttu-id="0cfe3-166">DinnersController</span><span class="sxs-lookup"><span data-stu-id="0cfe3-166">DinnersController</span></span> | <span data-ttu-id="0cfe3-167">Index)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-167">Index()</span></span> | <span data-ttu-id="0cfe3-168">N/A</span><span class="sxs-lookup"><span data-stu-id="0cfe3-168">N/A</span></span> |
| <span data-ttu-id="0cfe3-169">*/Home*</span><span class="sxs-lookup"><span data-stu-id="0cfe3-169">*/Home*</span></span> | <span data-ttu-id="0cfe3-170">HomeController</span><span class="sxs-lookup"><span data-stu-id="0cfe3-170">HomeController</span></span> | <span data-ttu-id="0cfe3-171">Index)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-171">Index()</span></span> | <span data-ttu-id="0cfe3-172">N/A</span><span class="sxs-lookup"><span data-stu-id="0cfe3-172">N/A</span></span> |
| */* | <span data-ttu-id="0cfe3-173">HomeController</span><span class="sxs-lookup"><span data-stu-id="0cfe3-173">HomeController</span></span> | <span data-ttu-id="0cfe3-174">Index)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-174">Index()</span></span> | <span data-ttu-id="0cfe3-175">N/A</span><span class="sxs-lookup"><span data-stu-id="0cfe3-175">N/A</span></span> |

<span data-ttu-id="0cfe3-176">마지막 세 개의 행에는 기본값을 표시 (컨트롤러 = 홈 작업 인덱스, Id = = "") 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="0cfe3-177">"Index" 메서드가 하나를 지정 하지 않으면 기본 동작 이름으로 등록 되어 있으므로 "/ Dinners" 및 "/ 홈" Url 원인 index () 작업 메서드는 컨트롤러 클래스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="0cfe3-178">"홈" 컨트롤러가 기본 컨트롤러로 하나 지정 되지 않은 경우에 등록 하기 때문에 "/" URL 사용 하면 만들려는 HomeController index () 동작 메서드를 호출 하는 데 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="0cfe3-179">이러한 기본 URL 라우팅 규칙, 마음에 들지 않으면 좋은 소식은 쉽게 변경-바로 위의 RegisterRoutes 메서드 내에서 편집할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="0cfe3-180">NerdDinner 응용 프로그램에서 하지만 기본 URL 라우팅 규칙을 하나라도 변경 않겠습니다 – 대신 사용으로-됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="0cfe3-181">우리의 DinnersController에서 DinnerRepository를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0cfe3-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="0cfe3-182">보겠습니다 DinnersController의 현재 구현은 이제 모델을 사용 하는 구현 사용 하 여 index () 및 Details() 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="0cfe3-183">동작을 구현 하려면 앞서 작성 DinnerRepository 클래스를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="0cfe3-184">"NerdDinner.Models" 네임 스페이스를 참조 하는 "using" 문을 추가 하 여 시작 하 고 DinnerController 클래스 우리의 DinnerRepository 인스턴스 필드로 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="0cfe3-185">이 장의 뒷부분에 나오는 "종속성 주입"의 개념을 소개 하 고 드리겠습니다 우리의 DinnerRepository 인스턴스의 방금 만들어 이제 테스트 – 하지만 오른쪽에 대 한 더 나은 단위 수 있게 해 주는 DinnerRepository에 대 한 참조를 가져오려면이 컨트롤러에 대 한 또 다른 방법은 표시 아래와 같은 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="0cfe3-186">이제이 검색된 된 데이터 모델 개체를 사용 하 여 HTML 응답을 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="0cfe3-187">뷰를 사용 하 여 컨트롤러를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0cfe3-187">Using Views with our Controller</span></span>

<span data-ttu-id="0cfe3-188">HTML을 조합 하 고 사용 하 여이 작업 메서드 내 코드를 작성할 수 있지만 합니다 *response.write ()* 도우미 메서드를 다시 보낼 클라이언트는 접근 방식을 통제 하기 힘들어집니다 매우 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="0cfe3-189">더 좋은 방법은에 응용 프로그램 및 우리의 DinnersController 작업 메서드 내에서 데이터 논리를 수행 하 고 다음 HTML 표시를 출력 하는 일을 담당 하는 별도 "view" 템플릿에 HTML 응답을 렌더링 하는 데 필요한 데이터를 전달 하는 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="0cfe3-190">잠시 후에 살펴보겠지만 "view" 템플릿은 일반적으로 HTML 태그 및 포함 된 렌더링 코드의 조합을 포함 하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="0cfe3-191">이 뷰 렌더링에서이 컨트롤러 논리를 분리 여러 큰 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="0cfe3-192">특히 응용 프로그램 코드와 UI 렌더링 형식 지정 코드를 명확히 "분리"를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="0cfe3-193">이 훨씬 쉽게 격리 된 상태에서 응용 프로그램 논리를 단위 테스트에서 UI 렌더링 논리.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="0cfe3-194">쉽게 나중에 응용 프로그램 코드를 변경 하지 않고 UI 렌더링 템플릿을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="0cfe3-195">및 개발자와 디자이너 프로젝트에서 공동 작업을 쉽게 만들 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="0cfe3-196">뷰 템플릿을 사용 하 여 "void" 대신 "ActionResult"의 반환 형식이로 반환 형식에서 두 작업 메서드 메서드 시그니처를 변경 하 여 HTML UI 응답을 반송 하려고 한다는 것을 나타내기 위해 DinnersController 클래스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="0cfe3-197">그런 다음 호출할 수 있습니다는 *View()* 아래와 같은 필요한 "ViewResult" 개체를 다시 반환할 기본 컨트롤러 클래스의 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="0cfe3-198">서명의 합니다 *View()* 도우미 메서드 위에 사용 하 여 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="0cfe3-199">첫 번째 매개 변수를 *View()* 도우미 메서드는 HTML 응답을 렌더링 하는 데 원하는 보기 템플릿 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="0cfe3-200">두 번째 매개 변수는 보기 템플릿에서 HTML 응답을 렌더링 하기 위해 필요한 데이터를 포함 하는 모델 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="0cfe3-201">index () 작업 메서드 내에서 호출 된 *View()* 도우미 메서드와 dinners "Index" 보기 템플릿을 사용 하는 HTML 목록을 렌더링 하려고 한다는 것을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="0cfe3-202">전달 보기 템플릿에서 Dinner에서 목록을 생성 하는 개체의 시퀀스:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="0cfe3-203">우리의 Details() 작업 메서드 내에서 URL 내에서 제공 하는 id를 사용 하 여 저녁 식사 개체를 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="0cfe3-204">호출을 올바른 Dinner 있으면 합니다 *View()* 도우미 메서드를 나타내는 "Details" 보기 템플릿을 사용 하 여 검색된 된 Dinner 개체를 렌더링 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="0cfe3-205">잘못 된 dinner 요청 된 경우 "NotFound" 보기 템플릿을 사용 하 여 Dinner 존재 하지 여부를 나타내는 유용한 오류 메시지를 렌더링 (및 오버 로드 된 버전의 합니다 *View()* 방금 템플릿 이름을 사용 하는 도우미 메서드 ):</span><span class="sxs-lookup"><span data-stu-id="0cfe3-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="0cfe3-206">이제 템플릿 보기 "NotFound", "정보" 및 "Index"를 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="0cfe3-207">템플릿 "NotFound" 보기 구현</span><span class="sxs-lookup"><span data-stu-id="0cfe3-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="0cfe3-208">요청 된 저녁 식사를 찾을 수 없습니다 나타내는 친숙 한 오류 메시지를 표시 하는 "NotFound" 보기 템플릿에서 – 구현부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="0cfe3-209">에서는 컨트롤러 동작 메서드를 내에서는 텍스트 커서를 배치 하 여 새 보기 템플릿을 만들 및 다음 마우스 오른쪽 단추로 클릭 하 고 "추가" 메뉴 명령을 선택 (Ctrl-M, Ctrl + V를 눌러이 명령은 실행할 수 있습니다):</span><span class="sxs-lookup"><span data-stu-id="0cfe3-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="0cfe3-210">이 아래와 같은 "뷰 추가" 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="0cfe3-211">대화 상자에서 만들 뷰 이름을 미리 채워집니다 기본적으로 동작 메서드의 이름과 일치 하도록 커서 시점의 대화 상자 (이 예제의 "세부 정보")에 시작 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="0cfe3-212">먼저 "NotFound" 템플릿 구현 하려는 것 이므로이 뷰 이름은 무시 하 고 "NotFound" 대신 되도록 설정 됩니다 것:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="0cfe3-213">"추가" 단추를 클릭 하는 경우 Visual Studio 새 "NotFound.aspx" 보기 템플릿을 만들지 우리 회사에 "\Views\Dinners" 디렉터리 (디렉터리 존재 하지 않는 경우에 생성 됩니다) 내에서:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="0cfe3-214">코드 편집기 내에서 새 "NotFound.aspx" 보기 템플릿의 등록도 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="0cfe3-215">보기 템플릿은 기본적으로 두 "콘텐츠 지역이 있기" 콘텐츠 및 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="0cfe3-216">첫 번째는 "title" HTML 페이지의 다시 전송 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="0cfe3-217">두 번째를 사용 하면 다시 전송 HTML 페이지의 "기본 콘텐츠"를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="0cfe3-218">"NotFound" 보기 템플릿은 구현 하려면 일부 기본 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="0cfe3-219">에서는 다음 시도해 볼 수 있습니다 브라우저 내에서.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-219">We can then try it out within the browser.</span></span> <span data-ttu-id="0cfe3-220">할 일이를 요청 합니다 *"/ Dinners/세부 정보/9999"* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="0cfe3-221">이 현재 데이터베이스에 존재 하지는 우리의 DinnersController.Details() 작업 방법 "NotFound" 보기 템플릿은 렌더링 하면 dinner를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="0cfe3-222">위의 스크린샷은에서 알 수는 기본 보기 템플릿은 다양 한 화면에서 기본 콘텐츠를 둘러싸는 HTML 상속한는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="0cfe3-223">보기 템플릿은 사이트의 모든 뷰에 일관 된 레이아웃을 적용할 수 있게 해 주는 "마스터 페이지" 템플릿을 사용 하는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="0cfe3-224">마스터 페이지이 자습서의 뒷부분에서 더 많은 작동 하는 방법을 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="0cfe3-225">템플릿 "Details" 보기 구현</span><span class="sxs-lookup"><span data-stu-id="0cfe3-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="0cfe3-226">이제는 단일 Dinner 모델에 대 한 HTML을 생성 하는 "Details" 뷰 템플릿에 –를 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="0cfe3-227">에서는에서는 세부 정보 작업 메서드 내에서 텍스트 커서를 사용 하 여이 작업을 수행 및 다음 마우스 오른쪽 단추로 클릭 하 고 "추가" 메뉴 명령을 선택 (또는 Ctrl-M, Ctrl + V 키를 누릅니다):</span><span class="sxs-lookup"><span data-stu-id="0cfe3-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="0cfe3-228">"뷰 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="0cfe3-229">기본 뷰 이름 ("정보") 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="0cfe3-230">에서는 또한 대화 상자에서 "강력한 형식의 뷰 만들기" 확인란을 선택 하 고 컨트롤러에서 보기로 전달 모델 형식의 이름입니다 (combobox 드롭다운을 사용 하 여) 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="0cfe3-231">이 보기에 대 한 Dinner 개체를 전달 (이 형식에 대 한 정규화 된 이름은: "NerdDinner.Models.Dinner"):</span><span class="sxs-lookup"><span data-stu-id="0cfe3-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="0cfe3-232">이전 템플릿에 선택한 보기를 만드는 "빈"와 달리이 시간에 자동으로 선택 "스 캐 폴드" "Details" 템플릿을 사용 하 여 보기.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="0cfe3-233">위 대화 상자에서 "콘텐츠 보기" 드롭다운을 변경 하 여이 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="0cfe3-234">"스 캐 폴딩" 전달 되도록 Dinner 개체를 기반으로 세부 정보 보기 템플릿은의 초기 구현을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="0cfe3-235">신속 하 게 시작 보기 템플릿 구현 하는 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="0cfe3-236">"추가" 단추를 클릭 하는 경우 Visual Studio는 우리 회사에 새 "Details.aspx" 보기 템플릿 파일을 우리의 "\Views\Dinners" 디렉터리 내에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="0cfe3-237">코드 편집기 내에서 새 "Details.aspx" 보기 템플릿의 등록도 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="0cfe3-238">초기 스 캐 폴드 구현의 Dinner 모델을 기반으로 세부 정보 보기를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="0cfe3-239">스 캐 폴딩 엔진은.NET 리플렉션을 사용 하 여, 전달 된 클래스에 노출 된 공용 속성을 보고 및 찾으면 각 형식에 따라 적절 한 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="0cfe3-240">요청 수를 *"/ 1/세부 정보/Dinners"* 보이는지 "details" 스 캐 폴드 구현이 브라우저에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="0cfe3-241">이 URL을 사용 하 여 수동으로 추가한 데이터베이스에 처음 만들었을 때 dinners 중 하나가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="0cfe3-242">이 미국 신속한 구축 및 실행을 가져오고 Details.aspx 보기의 초기 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="0cfe3-243">이동 하 고 열어서이 대 한 만족도에 UI를 사용자 지정할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="0cfe3-244">더욱 긴밀 하 게 Details.aspx 템플릿을 살펴볼 때는 또한 정적 HTML이 포함 되어 뿐만 렌더링 코드를 포함 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="0cfe3-245">&lt;% %&gt; 보기 템플릿에서 렌더링 되 면 코드 너 깃 코드를 실행 하 고 &lt;% = %&gt; 코드 너 깃 내에 포함 된 코드를 실행 하 고 다음 템플릿의 출력 스트림에 결과 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="0cfe3-246">"모델" 강력한 형식의 속성을 사용 하 여 컨트롤러에서 전달 된 "Dinner" 모델 개체에 액세스 하는 보기 내에서 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="0cfe3-247">Visual Studio 편집기 내에서이 "모델" 속성에 액세스 하는 경우 미국 전체 코드 intellisense를 사용 하 여 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="0cfe3-248">아래와 같이 최종 세부 정보 보기 템플릿은 원본 표시 되도록 몇 가지 변경을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="0cfe3-249">액세스 하는 것은 *"/ 1/세부 정보/Dinners"* URL 다시 됩니다 이제 아래와 같은 렌더링:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="0cfe3-250">"Index" 보기 템플릿에서 구현</span><span class="sxs-lookup"><span data-stu-id="0cfe3-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="0cfe3-251">예정 된 Dinners 목록을 생성 하는 "Index" 보기 템플릿에서 – 이제 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="0cfe3-252">인덱스 작업 메서드 내에서 텍스트 커서를 놓은 다음 마우스 오른쪽 단추로 됩니다 것이 클릭 하 고 "추가" 메뉴 명령을 선택 (또는 Ctrl-M, Ctrl + V를 눌러) to-do입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="0cfe3-253">"뷰 추가" 대화 상자 내에서는 "Index" 라는 보기 템플릿을 유지 하 고 "강력한 형식의 뷰 만들기" 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="0cfe3-254">이 이번에 자동으로 "List" 보기 템플릿을 생성 하 고 선택 "NerdDinner.Models.Dinner" 모델 형식으로 보기에 전달 하도록 선택할 것 (하는 스 캐 폴드 뷰 추가 대화 상자는 가정 하면 "목록"을 만들었습니다 나타낸 것 때문에 시퀀스를 전달 Dinner 개체의 컨트롤러에서 보기로):</span><span class="sxs-lookup"><span data-stu-id="0cfe3-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="0cfe3-255">"추가" 단추를 클릭 하는 경우 Visual Studio는 미국에 대 한 새 "Index.aspx" 보기 템플릿 파일을을 우리의 "\Views\Dinners" 디렉터리 내에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="0cfe3-256">이 "스 캐 폴드" 보기로 전달 Dinners는 HTML 테이블 목록이 제공 하는 그 초기 구현.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="0cfe3-257">된 액세스 권한 및 응용 프로그램을 실행할 때 합니다 *"/"이 (Dinners/* 같이 URL dinners 목록을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="0cfe3-258">위의 테이블 솔루션 매우 원하는 우리의 소비자 Dinner 목록에 없는 Dinner 데이터 –의 표 형태의 레이아웃을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="0cfe3-259">Index.aspx 보기 템플릿이 업데이트 되 고 데이터의 적은 개수의 열을 나열 하 고 사용 하도록 수정할 수는 &lt;ul&gt; 아래 코드를 사용 하 여 테이블 대신이 렌더링 하는 요소:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="0cfe3-260">모델에서 각 dinner 반복에서는 위의 foreach 문 내에서 "var" 키워드를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="0cfe3-261">C# 3.0을 사용 하 여 알 수 없는 것는 dinner 개체가 바인딩된 임을 의미 "var"를 사용 하 여 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="0cfe3-262">컴파일러는 강력한 형식의 "모델" 속성에 대해 형식 유추를 사용 하 여는 대신 의미 (형식인 "IEnumerable&lt;Dinner&gt;") 및 전체 얻게 즉 Dinner 형식 –으로 로컬 "dinner" 변수의 컴파일 intellisense 및 컴파일 시간에 대 한 코드 블록 내에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="0cfe3-263">새로 고침 도달할 때 합니다 */Dinners* 아래는 업데이트 된 보기 이제 다음과 같은 브라우저에서 URL:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="0cfe3-264">이 더 나은 – 하지만 아직 완전히 준비 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="0cfe3-265">마지막 단계는 최종 사용자 목록에서 개별 Dinners를 클릭 하 고 세부 정보를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="0cfe3-266">이 DinnersController 세부 정보 작업 메서드를 연결 하는 HTML 하이퍼링크 요소 렌더링 하 여 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="0cfe3-267">이러한 하이퍼링크 두 가지 방법 중 하나로 인덱스 보기 내에서 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="0cfe3-268">첫 번째 HTML을 수동으로 만드는 방법은 &lt;는&gt; 요소 아래에 포함할 위치와 같은 &lt;% %&gt; 내에서 차단 합니다 &lt;는&gt; HTML 요소:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="0cfe3-269">대 안으로 사용 하 여 프로그래밍 방식으로 HTML을 만들 수 있는 ASP.NET MVC에서 기본 제공 "Html.ActionLink()" 도우미 메서드를 활용 하는 것 &lt;는&gt; 에 다른 동작 메서드에 연결 되는 요소는 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="0cfe3-270">Html.ActionLink() 도우미 메서드를 사용 하는 첫 번째 매개 변수가 표시 하는 링크 텍스트입니다 (이 경우 제목의를 저녁 식사) 두 번째 매개 변수는 컨트롤러 작업 이름 (이 경우 세부 정보 메서드)에 대 한 링크를 생성 하려고 하 고 세 번째 매개 변수는 집합 작업 (속성 이름/값을 사용 하 여 익명 형식으로 구현 됨)로 전달할 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="0cfe3-271">이 경우에 연결 하 고 ASP.NET MVC의 규칙 기본 URL 라우팅을 이므로 dinner의 "id" 매개 변수에 지정 "{컨트롤러} / {Action} / {id}" Html.ActionLink() 도우미 메서드는 다음과 같은 출력이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="0cfe3-272">Index.aspx 뷰에 대해에서는 Html.ActionLink() 도우미 메서드 접근 방식을 사용 하 고 적절 한 세부 정보 URL 목록에 연결할 각 저녁에:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="0cfe3-273">도달할 때 이제 및 합니다 */Dinners* dinner 목록 아래와 같이 URL:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="0cfe3-274">목록의 Dinners 중 하나를 클릭 하는 경우에 대 한 자세한 내용은으로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="0cfe3-275">명명 규칙 기반 및 \Views 디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="0cfe3-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="0cfe3-276">기본적으로 ASP.NET MVC 응용 프로그램 템플릿 보기를 확인할 때 구조 명명 규칙 기반 디렉터리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="0cfe3-277">개발자를 정규화 위치 경로 컨트롤러 클래스 내에서 뷰를 참조할 때 필요가 없도록 하려면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="0cfe3-278">기본적으로 ASP.NET MVC 뷰 템플릿 파일 내에서 표시 됩니다는 * \Views\[ControllerName]\* 응용 프로그램 아래의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-278">By default ASP.NET MVC will look for the view template file within the *\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="0cfe3-279">예를 들어 지금까지 작업 세 가지 보기 템플릿을 명시적으로 참조 하는 DinnersController 클래스 –: "Index", "Details" 및 "NotFound"입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="0cfe3-280">ASP.NET MVC는 기본적으로 찾습니다 내에서 이러한 보기는 *\Views\Dinners* 는 응용 프로그램 루트 디렉터리 아래의 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="0cfe3-281">위에 있는 어떻게은 현재 프로젝트 내에서 세 가지 컨트롤러 클래스 (DinnersController 고 HomeController AccountController – 마지막 두 프로젝트를 만들 때 기본적으로 추가 된), 세 개의 하위 디렉터리 (각각에 하나 이며 컨트롤러) \Views 디렉터리 내에서.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="0cfe3-282">홈 및 계정 컨트롤러에서 참조 하는 뷰에 해당에서 템플릿 보기를 사용 하는 자동으로 해결 됩니다 *\Views\Home* 하 고 *\Views\Account* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="0cfe3-283">합니다 *\Views\Shared* 하위 디렉터리에 응용 프로그램 내의 여러 컨트롤러에서 다시 사용할 수 있는 템플릿 보기를 저장 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="0cfe3-284">ASP.NET MVC 뷰 템플릿 해결을 시도할 때 먼저 내에서 확인 합니다는 *\Views\[컨트롤러]* 특정 디렉터리 보기 템플릿을 찾을 수 없으면 있습니다 표시 됩니다 내는 *\Views\ 공유* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="0cfe3-285">개별 보기 템플릿 이름을 지정 하 고 있어 권장된 지침은 렌더링를 일으킨 작업 메서드와 동일한 이름을 공유 하는 뷰 템플릿에 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="0cfe3-286">예를 들어, "인덱스" 위에 작업 메서드는를 사용 하 여 "Index" 뷰에서 뷰 결과 렌더링 및 "Details" 동작 메서드를 "Details" 뷰를 사용 하 여 해당 결과 렌더링 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="0cfe3-287">이 쉽게 신속 하 게 각 작업과 연결 된 템플릿을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="0cfe3-288">개발자는 보기 템플릿은 컨트롤러에서 호출 되는 작업 메서드가 동일한 이름이 보기 템플릿 이름을 명시적으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="0cfe3-289">대신 방금에 전달할 수는 모델 개체 "View()" 도우미 메서드 (뷰 이름 지정) 없이 및 ASP.NET MVC 사용을 자동으로 유추 된 *\Views\[ControllerName]\[ActionName]* 렌더링 하는 디스크에서 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="0cfe3-290">따라서 컨트롤러 코드를 정리 하 고 코드에서 두 번 이름 중복을 피하기 위해:</span><span class="sxs-lookup"><span data-stu-id="0cfe3-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="0cfe3-291">위의 코드는 사이트에 대 한 환경 유용한 Dinner 목록/세부 정보를 구현 하는 데 필요한 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="0cfe3-292">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cfe3-292">Next Step</span></span>

<span data-ttu-id="0cfe3-293">이제 검색 환경을 구축 하는 훌륭한 Dinner가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="0cfe3-294">CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 편집 지원을 이제 사용할 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfe3-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0cfe3-295">[이전](build-a-model-with-business-rule-validations.md)
> [다음](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="0cfe3-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
