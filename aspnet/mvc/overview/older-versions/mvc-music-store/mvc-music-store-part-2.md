---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: '2 단계: 컨트롤러 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 2 부에서는 컨트롤러에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 680cdea388d9b01961bd626643c0fd91c9205ed7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878700"
---
<a name="part-2-controllers"></a><span data-ttu-id="36723-104">2 부: 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="36723-104">Part 2: Controllers</span></span>
====================
<span data-ttu-id="36723-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="36723-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="36723-106">MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="36723-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="36723-107">MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="36723-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="36723-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="36723-109">2 부에서는 컨트롤러에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-109">Part 2 covers Controllers.</span></span>


<span data-ttu-id="36723-110">기존 웹 프레임 워크와 함께 들어오는 Url은 일반적으로 디스크 파일에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="36723-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="36723-111">예: URL에 대 한 요청 같은 "/ Products.aspx" 또는 "/ Products.php" "Products.aspx" 또는 "Products.php" 파일에서 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="36723-112">웹 기반 MVC 프레임 워크를 약간 다른 방식으로 서버 코드에 Url을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="36723-113">파일에 들어오는 Url 매핑, 대신 대신 Url에 매핑되는지 클래스에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="36723-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="36723-114">이러한 클래스는 "컨트롤러" 라고 하 고 사용자 입력을 처리 하는 들어오는 HTTP 요청을 처리 해야 하는, 검색 및 데이터를 저장 및 보내기에 대 한 응답을 결정 하는 클라이언트에 다시 (HTML을 표시, 파일을 다운로드, 다른 리디렉션 URL, 등)입니다.</span><span class="sxs-lookup"><span data-stu-id="36723-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="36723-115">HomeController 추가</span><span class="sxs-lookup"><span data-stu-id="36723-115">Adding a HomeController</span></span>

<span data-ttu-id="36723-116">사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 하 여 MVC 음악 스토어 응용 프로그램을 먼저 실행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="36723-117">ASP.NET MVC의 기본 명명 규칙에 따라 알아보고 HomeController 호출 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="36723-118">솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "추가" 및 "컨트롤러..."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…"</span></span> <span data-ttu-id="36723-119">명령입니다.</span><span class="sxs-lookup"><span data-stu-id="36723-119">command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="36723-120">이 "컨트롤러 추가" 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-120">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="36723-121">"HomeController" 컨트롤러 이름을 지정 하 고 추가 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="36723-121">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="36723-122">HomeController.cs, 새 파일을 다음 코드로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="36723-122">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="36723-123">가능한 한 간단 하 게 시작 하는 문자열만 반환 하는 간단한 방법을 인덱스 메서드를 바꿉니다 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-123">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="36723-124">두 가지 변경을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-124">We'll make two changes:</span></span>

- <span data-ttu-id="36723-125">ActionResult 대신 문자열을 반환 방법 변경</span><span class="sxs-lookup"><span data-stu-id="36723-125">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="36723-126">반환할 Hello에서 "홈" return 문을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-126">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="36723-127">메서드는 이제 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36723-127">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="36723-128">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="36723-128">Running the Application</span></span>

<span data-ttu-id="36723-129">이제 사이트를 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-129">Now let's run the site.</span></span> <span data-ttu-id="36723-130">웹 서버를 시작 하 고 다음 중 하나를 사용 하는 사이트를 체험할 수 있습니다::</span><span class="sxs-lookup"><span data-stu-id="36723-130">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="36723-131">디버그 ⇨ 디버깅 시작 메뉴 항목 선택</span><span class="sxs-lookup"><span data-stu-id="36723-131">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="36723-132">도구 모음에서 녹색 화살표 단추를 클릭 합니다. ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="36723-132">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="36723-133">바로 가기 키, f5 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-133">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="36723-134">위의 단계를 사용 하 여이 프로젝트를 컴파일하 되 고 그러면 ASP.NET Development Server를 시작 하려면 Visual Web Developer에 기본 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36723-134">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="36723-135">알림을, ASP.NET Development Server가 시작 되었음을 나타내기 위해 화면 아래에 나타나고에서 실행 되 고 있는지 포트 번호가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36723-135">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="36723-136">Visual Web Developer 웹 서버를 가리키는 URL 브라우저 창을 엽니다 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36723-136">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="36723-137">이렇게 하면를 웹 응용 프로그램을 신속 하 게 시험해 수: 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-137">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="36723-138">알겠습니다 상당히 빠른-새 웹 사이트에서 만든 했던 삼 선 함수를 추가 하 고 브라우저에서 텍스트 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-138">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="36723-139">로켓 과학 하지 이지만 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-139">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="36723-140">*참고: Visual Web Developer 웹 사이트 포트"임의의 무료" 번호에서 실행 ASP.NET 개발 서버를 포함 합니다. 또한 위의 스크린 샷에서 사이트에서 실행 중인 `http://localhost:26641/`, 26641 포트를 사용 하 고 있습니다. 포트 번호 달라 집니다. 이 자습서에서는 like /Store/Browse URL에 대해 논의할 하는 포트 번호 뒤 이동 됩니다. 26641의 포트 번호를 가정할 때/저장소/찾아보기로 이동은 의미를 찾아 `http://localhost:26641/Store/Browse`합니다.*</span><span class="sxs-lookup"><span data-stu-id="36723-140">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="36723-141">StoreController 추가</span><span class="sxs-lookup"><span data-stu-id="36723-141">Adding a StoreController</span></span>

<span data-ttu-id="36723-142">사이트의 홈 페이지를 구현 하는 간단한 HomeController 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-142">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="36723-143">이제 음악 스토어의 검색 기능을 구현 하는을 사용 해야 하는 다른 컨트롤러를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-143">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="36723-144">저장소 컨트롤러는 세 가지 시나리오를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-144">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="36723-145">음악 스토어에서 음악 장르 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="36723-145">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="36723-146">특정 장르의 음악 앨범을 모두 나열 하는 찾아보기 페이지</span><span class="sxs-lookup"><span data-stu-id="36723-146">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="36723-147">특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지</span><span class="sxs-lookup"><span data-stu-id="36723-147">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="36723-148">새 StoreController 클래스를 추가 하 여 시작 합니다...</span><span class="sxs-lookup"><span data-stu-id="36723-148">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="36723-149">아직 하지 않는 경우 브라우저를 닫거나 디버그 ⇨ 디버깅 중지 메뉴 항목을 선택 하 여 응용 프로그램 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-149">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="36723-150">이제 새 StoreController를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-150">Now add a new StoreController.</span></span> <span data-ttu-id="36723-151">솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 기능 선택 하 여 수행 됩니다 HomeController 사용 했던 것 처럼&gt;컨트롤러 메뉴 항목</span><span class="sxs-lookup"><span data-stu-id="36723-151">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="36723-152">새 우리의 StoreController "Index" 메서드가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-152">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="36723-153">음악 스토어에서 모든 장르를 나열 하는 가격 목록 페이지를 구현 하려면이 "Index" 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-153">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="36723-154">시나리오를 구현 하는 두 개의 다른 우리의 StoreController 처리 하기 원하는 두 개의 추가 메서드 추가: 찾아보기 및 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="36723-154">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="36723-155">컨트롤러 내에서 이러한 메서드 (인덱스, 찾아보기 및 세부 정보)에 "컨트롤러 작업" 라고 하며 HomeController.Index () 동작 메서드로 앞서 설명한 바가 작업 하는 것 (일반적) 콘텐츠를 확인 하 고 URL 요청에 응답 브라우저 또는 URL을 호출 하는 사용자에 게 다시 전송 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-155">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="36723-156">StoreController 구현은 theIndex() "Hello에서 Store.Index()" 문자열을 반환 하는 방법을 변경 하 여 시작 합니다 및 browse () 및 Details() 비슷한 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-156">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="36723-157">프로젝트를 다시 실행 하 고 다음 Url을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-157">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="36723-158">/ 저장소</span><span class="sxs-lookup"><span data-stu-id="36723-158">/Store</span></span>
- <span data-ttu-id="36723-159">/ 저장소/찾아보기</span><span class="sxs-lookup"><span data-stu-id="36723-159">/Store/Browse</span></span>
- <span data-ttu-id="36723-160">/ 저장소/세부 정보</span><span class="sxs-lookup"><span data-stu-id="36723-160">/Store/Details</span></span>

<span data-ttu-id="36723-161">이러한 Url에 액세스 컨트롤러 내에서 작업 메서드를 호출 하 고 문자열 응답 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36723-161">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="36723-162">아니지만 방금 상수 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="36723-162">That's great, but these are just constant strings.</span></span> <span data-ttu-id="36723-163">보겠습니다 있도록 동적으로 URL에서 정보를 가져올 없도록 페이지 출력에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-163">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="36723-164">먼저 URL에서 쿼리 문자열 값을 검색 하는 찾아보기 동작 메서드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-164">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="36723-165">이 동작 메서드에 "장르" 매개 변수를 추가 하 여 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-165">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="36723-166">이 작업을 수행 하는 경우 ASP.NET MVC가 호출 되 면이 동작 메서드에 "장르" 라는 모든 쿼리 문자열 또는 폼 게시 매개를 자동으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-166">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="36723-167">*참고:에서는 HttpUtility.HtmlEncode 유틸리티 메서드를 사용자 입력을 삭제 합니다. 따라서 사용자를 /Store/Browse 같은 링크와 함께 보기에 Javascript를 삽입 수 없습니다. 장르 =&lt;스크립트&gt;window.location='http://hackersite.com'&lt;/script&gt;합니다.*</span><span class="sxs-lookup"><span data-stu-id="36723-167">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="36723-168">이제/저장소/찾아보기를 찾아보겠습니다? Genre Disco =</span><span class="sxs-lookup"><span data-stu-id="36723-168">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="36723-169">이제 다음 변경 상세 작업 읽고 입력된 매개 변수를 표시 하 라는 id입니다.</span><span class="sxs-lookup"><span data-stu-id="36723-169">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="36723-170">이 이전 메서드와 달리 쿼리 문자열 매개 변수로 ID 값을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-170">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="36723-171">대신 URL 자체 내에서 직접 포함할 것 했습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-171">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="36723-172">예를 들어: /Store/Details/5 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-172">For example: /Store/Details/5.</span></span>

<span data-ttu-id="36723-173">ASP.NET MVC를 통해이 이상 구성할 필요 없이 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-173">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="36723-174">ASP.NET MVC의 기본 라우팅 규칙 동작 메서드 이름 뒤에 오는 "ID" 라는 매개 변수를 URL의 세그먼트를 처리 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="36723-174">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="36723-175">작업 메서드에 매개 변수 ID 이름 경우 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-175">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="36723-176">응용 프로그램을 실행 하 고 /Store/Details/5로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="36723-176">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="36723-177">지금까지 수행한 무엇 요약해 보면:</span><span class="sxs-lookup"><span data-stu-id="36723-177">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="36723-178">Visual Web Developer에서 새 ASP.NET MVC 프로젝트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-178">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="36723-179">ASP.NET MVC 응용 프로그램의 기본 폴더 구조에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-179">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="36723-180">ASP.NET 개발 서버를 사용 하 여 웹 사이트를 실행 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-180">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="36723-181">두 개의 컨트롤러 클래스 만들었습니다:는 HomeController 및는 StoreController</span><span class="sxs-lookup"><span data-stu-id="36723-181">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="36723-182">작업 메서드는 URL 요청에 응답 하 고 브라우저에 텍스트를 반환 합니다.이 컨트롤러를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="36723-182">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="36723-183">[이전](mvc-music-store-part-1.md)
> [다음](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="36723-183">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
