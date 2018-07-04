---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: '2 부: 컨트롤러 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 2 부에서는 컨트롤러를 설명합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: a854feff675cae302b9927d209808257b7d087cb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381805"
---
<a name="part-2-controllers"></a><span data-ttu-id="15621-104">2 부: 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="15621-104">Part 2: Controllers</span></span>
====================
<span data-ttu-id="15621-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="15621-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="15621-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="15621-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="15621-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="15621-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="15621-109">2 부에서는 컨트롤러를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-109">Part 2 covers Controllers.</span></span>


<span data-ttu-id="15621-110">기존 웹 프레임 워크를 들어오는 Url은 일반적으로 디스크에 파일이 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="15621-111">예를 들어:와 같은 URL에 대 한 요청을 "/ 대" 하거나 "/ Products.php" "Products.aspx" 또는 "Products.php" 파일에서 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="15621-112">웹 기반 MVC 프레임 워크를 약간 다른 방식으로 서버 코드에 Url을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="15621-113">대신 들어오는 Url 파일을 대신 매핑할 Url 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="15621-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="15621-114">이러한 클래스는 "컨트롤러" 라고 하 고 사용자 입력을 처리 하는 들어오는 HTTP 요청을 처리 하는 일을 담당 하는 클라이언트 다시 검색, 데이터 저장 및 전송에 대 한 응답 결정 (HTML 표시 파일을 다운로드, 다른 리디렉션 URL 등)입니다.</span><span class="sxs-lookup"><span data-stu-id="15621-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="15621-115">HomeController를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-115">Adding a HomeController</span></span>

<span data-ttu-id="15621-116">MVC Music Store 응용 프로그램 사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 하 여 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="15621-117">ASP.NET MVC의 기본 명명 규칙을 준수 하 고 HomeController 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="15621-118">솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 [추가]를 선택한 다음 "컨트롤러..." 명령을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="15621-119">"컨트롤러 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="15621-120">"HomeController" 컨트롤러 이름과 추가 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="15621-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="15621-121">다음 코드를 사용 하 여 새 파일을 HomeController.cs에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="15621-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="15621-122">최대한 간단를 시작 하려면 보겠습니다 문자열로 반환 하는 간단한 메서드를 사용 하 여 인덱스 메서드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="15621-123">두 가지 변경을 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-123">We'll make two changes:</span></span>

- <span data-ttu-id="15621-124">ActionResult 대신 문자열을 반환 하도록 메서드를 변경</span><span class="sxs-lookup"><span data-stu-id="15621-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="15621-125">"Hello에서 홈" 반환할 return 문을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="15621-126">이제 메서드를 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="15621-127">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="15621-127">Running the Application</span></span>

<span data-ttu-id="15621-128">이제 사이트를 실행 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-128">Now let's run the site.</span></span> <span data-ttu-id="15621-129">수는 웹 서버를 시작 하 고 다음 중 하나를 사용 하 여 사이트를 사용해::</span><span class="sxs-lookup"><span data-stu-id="15621-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="15621-130">디버그 ⇨ 디버깅 시작 메뉴 항목 선택</span><span class="sxs-lookup"><span data-stu-id="15621-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="15621-131">도구 모음에서 녹색 화살표 단추를 클릭 합니다. ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="15621-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="15621-132">바로 가기, F5 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="15621-133">위의 단계를 사용 하 여 프로젝트를 컴파일 및 시작 하려면 Visual Web Developer에 기본 제공 되는 ASP.NET Development Server 인해 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="15621-134">알림을, ASP.NET Development Server를 시작 했음을 나타내기 위해 화면 하단 모서리에 나타나고 포트 번호를 표시 하에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="15621-135">Visual Web Developer는 웹 서버를 가리키는 URL 브라우저 창을 엽니다 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="15621-136">이렇게 하면 웹 응용 프로그램을 신속 하 게 사용해 주세요.</span><span class="sxs-lookup"><span data-stu-id="15621-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="15621-137">알겠습니다. 아주 빠른-새 웹 사이트를 만들었습니다를 선 함수를 추가 하 고 브라우저에서 텍스트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="15621-138">Rocket 과학 하지 이지만 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="15621-139">*참고: Visual Web Developer에 임의 무료 "port" 웹 사이트를 실행 하는 ASP.NET Development Server를 포함 합니다. 위의 스크린샷에서 사이트에서 실행 되 `http://localhost:26641/`이므로 26641 포트를 사용 하는 것입니다. 포트 번호에는 이와 다릅니다. 이 자습서에서는 like /Store/Browse URL에 대 한 이야기 하는 포트 번호 뒤 이동 됩니다. 26641 포트 번호를 가정 하 고/저장소/찾아보기로 이동 의미를 찾아 `http://localhost:26641/Store/Browse`합니다.*</span><span class="sxs-lookup"><span data-stu-id="15621-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="15621-140">StoreController 추가</span><span class="sxs-lookup"><span data-stu-id="15621-140">Adding a StoreController</span></span>

<span data-ttu-id="15621-141">사이트의 홈 페이지를 구현 하는 간단한 HomeController 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="15621-142">지금 사용 하 여 음악 스토어의 검색 기능을 구현 하는 다른 컨트롤러를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="15621-143">저장소 컨트롤러는 세 가지 시나리오를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="15621-144">음악 스토어에서 음악 장르 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="15621-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="15621-145">특정 장르에 음악 앨범의 모든를 나열 하는 찾아보기 페이지</span><span class="sxs-lookup"><span data-stu-id="15621-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="15621-146">특정 음악 앨범에 대 한 정보를 보여 주는 세부 정보 페이지</span><span class="sxs-lookup"><span data-stu-id="15621-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="15621-147">새 StoreController 클래스를 추가 하 여 시작 하겠습니다...</span><span class="sxs-lookup"><span data-stu-id="15621-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="15621-148">이미 않았다면 브라우저를 닫거나 디버그 ⇨ 디버깅 중지 메뉴 항목을 선택 하 여 응용 프로그램 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="15621-149">이제 새 StoreController를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-149">Now add a new StoreController.</span></span> <span data-ttu-id="15621-150">HomeController를 사용 하 여 수행한 것 처럼에서는 이렇게 솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 하 고 추가-&gt;컨트롤러 메뉴 항목</span><span class="sxs-lookup"><span data-stu-id="15621-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="15621-151">이 새 StoreController는 "Index" 메서드가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="15621-152">음악 스토어에서 모든 장르를 나열 하는 목록 페이지를 구현 하려면이 "Index" 메서드가 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="15621-153">두 가지 다른 시나리오를 처리 하는 StoreController 원하는 구현 하는 두 개의 추가 메서드 추가: 찾아보기 및 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="15621-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="15621-154">컨트롤러 내에서 이러한 메서드 (인덱스, 찾아보기 및 세부 정보) "컨트롤러 작업" 라고 이며 HomeController.Index () 작업 메서드를 사용 하 여 이미 살펴보았듯이, 업무 URL 요청에 응답 하 고 (일반적) 콘텐츠를 확인 하려면 브라우저 또는 URL을 호출 하는 사용자에 게 다시 전송 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="15621-155">TheIndex() "Hello에서 Store.Index()" 문자열을 반환 하는 방법을 변경 하 여 StoreController 구현을 먼저 및 browse () 및 Details() 이와 유사한 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="15621-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="15621-156">프로젝트를 다시 실행 하 고 다음 Url을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="15621-157">/ 저장소</span><span class="sxs-lookup"><span data-stu-id="15621-157">/Store</span></span>
- <span data-ttu-id="15621-158">/ 저장소/찾아보기</span><span class="sxs-lookup"><span data-stu-id="15621-158">/Store/Browse</span></span>
- <span data-ttu-id="15621-159">/ 저장소/세부 정보</span><span class="sxs-lookup"><span data-stu-id="15621-159">/Store/Details</span></span>

<span data-ttu-id="15621-160">이러한 Url 액세스 컨트롤러 내의 작업 메서드를 호출 되며 문자열 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="15621-161">잘 되는 되지만 이러한 방금 상수 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="15621-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="15621-162">보겠습니다 있도록 동적 URL에서 정보를 사용 하 고 페이지 출력에 표시할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="15621-163">먼저 URL에서 쿼리 문자열 값을 검색 하는 찾아보기 작업 메서드를 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15621-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="15621-164">이 동작 메서드에 "장르" 매개 변수를 추가 하 여이 작업을 수행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="15621-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="15621-165">이 작업을 수행 하는 경우 ASP.NET MVC는 모든 쿼리 문자열 또는 폼 post 라는 매개 변수 "장르"는 작업 메서드를 호출 하면 자동으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="15621-166">*참고: HttpUtility.HtmlEncode 유틸리티 메서드를 사용 하 여 사용자 입력을 삭제 하는 것입니다. 이로써 /Store/Browse와 같은 링크를 사용 하 여 뷰에 Javascript 주입에서 사용자? 장르 =&lt;스크립트&gt;window.location = 'http://hackersite.com'&lt;/script&gt;합니다.*</span><span class="sxs-lookup"><span data-stu-id="15621-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="15621-167">이제/저장소 / 찾아보기 탐색 해 보겠습니다. 장르 Disco =</span><span class="sxs-lookup"><span data-stu-id="15621-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="15621-168">보겠습니다 읽고 ID 라는 이름의 입력된 매개 변수를 표시 하는 세부 정보 작업을 다음 변경</span><span class="sxs-lookup"><span data-stu-id="15621-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="15621-169">이전 메서드와 달리 쿼리 문자열 매개 변수로 ID 값을를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="15621-170">대신 URL 자체 내에서 직접 포함 됩니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15621-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="15621-171">예를 들어: /Store/Details/5 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="15621-172">ASP.NET MVC 쉽게 아무 것도 구성 하지 않고도 이렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="15621-173">ASP.NET MVC의 기본 라우팅 규칙 작업 메서드 이름 뒤에 "ID" 라는 매개 변수를 URL의 세그먼트를 처리 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15621-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="15621-174">동작 메서드에서 ID 라는 매개 변수가 있으면 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="15621-175">응용 프로그램을 실행 하 고 /Store/Details/5를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="15621-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="15621-176">지금까지 수행한 지금 정리해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="15621-177">Visual Web Developer에서 새 ASP.NET MVC 프로젝트를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="15621-178">ASP.NET MVC 응용 프로그램의 기본 폴더 구조에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="15621-179">ASP.NET Development Server를 사용 하 여 웹 사이트를 실행 하는 방법을 알게합니다</span><span class="sxs-lookup"><span data-stu-id="15621-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="15621-180">두 컨트롤러 클래스를 만들었습니다: HomeController 및는 StoreController</span><span class="sxs-lookup"><span data-stu-id="15621-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="15621-181">URL 요청에 응답 하 고 브라우저에 텍스트를 반환 하는 컨트롤러 작업 메서드에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15621-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="15621-182">[이전](mvc-music-store-part-1.md)
> [다음](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="15621-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
