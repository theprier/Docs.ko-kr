---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: "3 부: 뷰와 Viewmodel | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 3 부에서는 뷰 및 Viewmodel 다룹니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 5b38f88283c5d2d93f0bab283dbd9451855d95e3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-3-views-and-viewmodels"></a><span data-ttu-id="615c5-104">3 부: 뷰와 Viewmodel</span><span class="sxs-lookup"><span data-stu-id="615c5-104">Part 3: Views and ViewModels</span></span>
====================
<span data-ttu-id="615c5-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="615c5-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="615c5-106">MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="615c5-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="615c5-107">MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="615c5-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="615c5-109">3 부에서는 뷰 및 Viewmodel 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-109">Part 3 covers Views and ViewModels.</span></span>


<span data-ttu-id="615c5-110">지금까지 म 했습니다 방금 된 문자열에서에서 반환 컨트롤러 작업.</span><span class="sxs-lookup"><span data-stu-id="615c5-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="615c5-111">컨트롤러의 작동 방식을 파악 하는 좋은 방법이 하지만 하지 어떻게 원할 실제 웹 응용 프로그램을 빌드하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="615c5-112">사이트를 방문 하는 브라우저에 다시 HTML을 생성 하기 위해 더 좋은 방법은 원하는 하겠습니다-템플릿 파일 보다 쉽게 HTML 콘텐츠를 사용자 지정 하려면 사용할 수는 있는 하나를 다시 보낼 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="615c5-113">뷰가 수행할 정확 하 게입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="615c5-114">보기 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="615c5-114">Adding a View template</span></span>

<span data-ttu-id="615c5-115">템플릿 보기를 사용 하려면 있는 ActionResult를 반환할 HomeController 인덱스 방법 변경 알아보고 아래와 같은 View()를 반환 하도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="615c5-116">대신 "보기"를 사용 하 여 결과 다시 생성 하려고, 위의 변경 내용을 문자열로 반환 대신 되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="615c5-117">이제이 프로젝트에는 적절 한 보기 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="615c5-118">이렇게 하려면 인덱스 작업 메서드 내에서 텍스트 커서의 위치를 한 다음 마우스 오른쪽 단추로 클릭 알아보고 하겠습니다 "추가 보기"를 선택.</span><span class="sxs-lookup"><span data-stu-id="615c5-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="615c5-119">그러면 뷰 추가 대화 상자를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="615c5-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="615c5-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="615c5-121">"뷰 추가" 대화 상자를 쉽고 빠르게 보기 템플릿 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="615c5-122">"추가 된 보기" 기본적으로 대화 상자를 사용 하 여 동작 메서드가 일치 하도록 만드는 보기 템플릿의 이름을 미리 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="615c5-123">우리의 HomeController의 index () 동작 메서드 내에서 "추가 보기" 상황에 맞는 메뉴를 사용 하기 때문에 위의 "뷰 추가" 대화 자기 "Index" 기본적으로 미리 채워진 뷰 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="615c5-124">이 대화 상자에서 옵션 변경, 이므로 추가 단추를 클릭 합니다. 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="615c5-125">추가 단추를 클릭 하면 Visual Web Developer 보기 서식 파일을 수행해 줍니다 경우 폴더를 만들면 \Views\Home 디렉터리에 존재 하지 않는 새 Index.cshtml 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="615c5-126">"Index.cshtml" 파일의 이름과 폴더 위치는 중요 하며, 기본 ASP.NET MVC 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="615c5-127">디렉터리 이름, \Views\Home, HomeController 이름으로 지정 된 컨트롤러와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="615c5-128">보기 템플릿 이름, 인덱스, 보기를 표시 하는 컨트롤러 동작 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="615c5-129">ASP.NET MVC는 뷰를 반환 하려면이 명명 규칙을 사용 하면 이름 또는 뷰 서식 파일의 위치를 명시적으로 지정할 필요가 없도록를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="615c5-130">기본적으로 렌더링 합니다 \Views\Home\Index.cshtml 보기 템플릿 우리의 HomeController 내에서 아래와 같은 코드를 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="615c5-131">Visual Web Developer 만들어지고 템플릿 "Index.cshtml" 보기 "뷰 추가" 대화 상자 내에서 "추가" 단추를 클릭 했습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="615c5-132">Index.cshtml의 내용은 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="615c5-133">이 보기는 ASP.NET Web Forms 및 이전 버전의 ASP.NET MVC에서 사용 하는 Web Forms 뷰 엔진이 보다 더욱 간결 하 게 하는 Razor 구문을 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="615c5-134">Web Forms 뷰 엔진은 ASP.NET MVC 3에서 계속 사용할 수 있지만 많은 개발자 들이 Razor 뷰 엔진 ASP.NET MVC 개발 잘 맞는 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="615c5-135">처음 세 줄 ViewBag.Title를 사용 하 여 페이지 제목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="615c5-136">페이지 보기 알아보고 텍스트 제목 텍스트가 과정에서 자세히 곧 하지만 먼저 보겠습니다 업데이트를 확인 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="615c5-137">업데이트는 &lt;h2&gt; 아래와 같이 "이 되는 홈 페이지"를 태그 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="615c5-138">응용 프로그램은 홈 페이지에 표시 되는 새 텍스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="615c5-139">일반적인 사이트 요소에 대 한 레이아웃을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="615c5-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="615c5-140">대부분의 웹 사이트에는 여러 페이지 간에 공유 되는 콘텐츠가 있는: 탐색, 바닥글, 로고 이미지, 스타일 시트 참조 등입니다. Razor 뷰 엔진을 편리 라는 페이지를 사용 하 여 관리할 \_Layout.cshtml 자동으로 작성 된 우리/뷰/공유 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="615c5-141">아래에 표시 됩니다는 내용을 보려면이 폴더에 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="615c5-142">우리의 개별 보기에서 콘텐츠를 표시 하는 @RenderBody() 명령 및 있는 외부에서 표시 하려는 기타 일반적인 콘텐츠 배포에 추가할 수는 \_Layout.cshtml 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="615c5-143">MVC 음악 스토어 있도록 바로 위에 있는 서식 파일에 추가 하는 사이트에 있는 모든 페이지는 홈 페이지 및 저장소 영역에 대 한 링크가 있는 공용 헤더를 할 수 있음 @RenderBody() 문입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="615c5-144">스타일 시트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-144">Updating the StyleSheet</span></span>

<span data-ttu-id="615c5-145">빈 프로젝트 템플릿 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="615c5-146">디자이너 우리의 몇 가지 추가 CSS 이미지를 제공 지금에 추가 하므로 사이트에 대 한 디자인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="615c5-147">업데이트 된 CSS 파일 및 이미지에서 제공 되는 MvcMusicStore Assets.zip의 콘텐츠 디렉터리에 포함 된 [MVC 음악 저장소](https://github.com/evilDave/MVC-Music-Store)합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="615c5-148">Windows 탐색기에서 둘 모두를 선택 하 고 아래와 같이 Visual Web Developer에서 솔루션의 콘텐츠 폴더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="615c5-149">기존 Site.css 파일을 덮어쓸 것인지를 확인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="615c5-150">예를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="615c5-151">응용 프로그램의 콘텐츠 폴더에 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="615c5-152">이제 응용 프로그램을 실행 하 고 홈 페이지에서 변경 내용이 어떻게 표시 되는지 확인 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="615c5-153">변경 된 기능을 검토해 보겠습니다: 및의 HomeController 인덱스 동작 메서드가 두 개 우리의 보기 템플릿 뒤에 표준 명명 규칙 때문에 코드에 "반환 View()" 라고 하는 경우에 \Views\Home\Index.cshtmlView 서식 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="615c5-154">홈 페이지를 \Views\Home\Index.cshtml 보기 템플릿 내에 정의 된 간단한 환영 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="615c5-155">홈 페이지를 사용 하 여 우리의 \_Layout.cshtml 템플릿을 시작 메시지 표준 사이트 HTML 레이아웃 내에 포함 되어 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="615c5-156">모델을 사용 하 여이 보기에 정보를 전달</span><span class="sxs-lookup"><span data-stu-id="615c5-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="615c5-157">방금 하드 코드 된 HTML을 표시 하는 뷰 템플릿이 없는 매우 흥미로운 웹 사이트를 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="615c5-158">동적 웹 사이트를 만들려면 것 대신 하고자 우리의 템플릿 보기에는 컨트롤러 작업에서 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="615c5-159">모델-뷰-컨트롤러 패턴 모델 이란 용어는 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="615c5-160">모델 개체에 해당 데이터베이스의 테이블은 대개 하지만 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="615c5-161">컨트롤러 작업 메서드에 있는 ActionResult를 반환 하는 보기에 모델 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="615c5-162">따라서 적절 한 HTML 응답을 생성 하는 데 응답을 생성 하 고 다음 템플릿 보기를이 정보를 전달 하는 데 필요한 모든 정보를 명확 하 게 패키지에는 컨트롤러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="615c5-163">이제 시작 하겠습니다 하므로, 작업에서 확인 하 여 이해 하기 가장 쉽고입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="615c5-164">먼저 스토어 내의 장르와 앨범을 나타내기 위해 일부 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="615c5-165">장르 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="615c5-166">프로젝트 내에서 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "클래스 추가" 옵션을 선택한 파일의 이름을 "Genre.cs"입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="615c5-167">생성 된 클래스에 공용 string Name 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="615c5-168">*참고: 본다면, 경우에는 {get; 설정;을 (를) 표기 하는 C#의 자동 구현 속성 기능을 사용 합니다. 이 목록에 속성의 이점을 없이 지원 필드를 선언할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="615c5-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="615c5-169">다음으로 제목 및 장르 속성이 있는 앨범 클래스 (Album.cs 라고 함)를 만들려면 동일한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="615c5-170">이제이 모델에서 동적 정보를 표시 하는 뷰를 사용 하도록 StoreController 수정할 수 있을 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="615c5-171">경우-설명을 위해 지금은-이름을 요청 ID에 따라 우리의 앨범, 아래의 보기에서와 같이 해당 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="615c5-172">단일 앨범에 대 한 정보를 표시 하므로 저장소 세부 정보 동작을 변경 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="615c5-173">맨 위에 "using" 문을 추가 **StoreControllers** 클래스 앨범 클래스를 사용 하 려 할 때마다 MvcMusicStore.Models.Album 입력할 필요가 없습니다 MvcMusicStore.Models 네임 스페이스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="615c5-174">해당 클래스의 "using" 섹션 표시 되 고 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="615c5-175">다음으로 업데이트 하는 세부 정보 컨트롤러 동작은 문자열이 아니라는 ActionResult 반환 되도록 HomeController의 Index 메서드와 동일한 방식으로.</span><span class="sxs-lookup"><span data-stu-id="615c5-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="615c5-176">이제 보기로 앨범 개체를 반환 하는 논리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="615c5-177">이 자습서의 뒷부분에 나오는 우리는 수 데이터는 데이터베이스에서 검색 – 하지만 지금 바로 사용 합니다 "데이터는 dummy"를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="615c5-178">*참고: C#과 함께 잘 모르는 경우으로 추정할 수 있습니다이 앨범 변수는 런타임에 바인딩 이라는 var을 사용 하 여 의미 합니다. C# 컴파일러에서 형식 유추를 기반으로 하는 해당 앨범이 유형이 앨범을 결정 하는 변수에 할당 및 기능 컴파일 타임 검사 및 Visual Studio code 편집기 하므로 로컬 앨범 변수 앨범 유형으로 컴파일할를 사용 하는 –는 올바르지 않습니다. 이 옵션을 지원 합니다.*</span><span class="sxs-lookup"><span data-stu-id="615c5-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="615c5-179">이제 우리의 앨범을 사용 하 여 HTML 응답을 생성 하는 보기 서식 파일을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="615c5-180">그 전에 프로젝트를 빌드하려면 뷰 추가 대화 상자는 새로 만든된 앨범 클래스에 대 한 알 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="615c5-181">메뉴 항목 Debug⇨Build MvcMusicStore를 선택 하 여 프로젝트를 빌드할 수 있습니다 (추가 신용에 대 한 사용할 수 있습니다 Ctrl-Shift-B 바로 가기 프로젝트를 빌드하려면).</span><span class="sxs-lookup"><span data-stu-id="615c5-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="615c5-182">지원 클래스를 설정 했으므로 준비가 우리의 보기 서식 파일을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="615c5-183">세부 정보 메서드 내에서 마우스 오른쪽 단추로 누르고 "추가 보기..."</span><span class="sxs-lookup"><span data-stu-id="615c5-183">Right-click within the Details method and select "Add View…"</span></span> <span data-ttu-id="615c5-184">상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-184">from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="615c5-185">HomeController 사용 하기 전에 수행한 것 처럼 새 보기 템플릿을 만들려면 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-185">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="615c5-186">StoreController에서 만드는 것 때문에 기본적으로 생성 됩니다 \Views\Store\Index.cshtml 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-186">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="615c5-187">와 달리 이전에 것 이며 "강력한 형식의 만들기" 보기 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-187">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="615c5-188">다음을 하겠습니다 "데이터-클래스 보기" 드롭 downlist 내에서 "앨범" 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-188">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="615c5-189">이렇게 하면 개체를 사용 하도록에 전달 될 앨범에는 필요한 뷰 템플릿을 만들려면 "뷰 추가" 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="615c5-189">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="615c5-190">"추가" 단추를 클릭 하면 다음 코드가 포함 된, 우리의 \Views\Store\Details.cshtml 보기 템플릿을 만들 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-190">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="615c5-191">첫 번째 줄이이 보기에서는 앨범 클래스에 강력한 형식의 하다는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-191">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="615c5-192">Razor 뷰 엔진 되었습니다 통과 했다고 앨범 개체 하므로 쉽게 모델 속성에 액세스 하 고 Visual Web Developer 편집기에서 IntelliSense는 이점이 있을 수를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-192">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="615c5-193">업데이트는 &lt;h2&gt; 태그를 다음과 같이 표시 해당 줄을 수정 하 여 앨범의 Title 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-193">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="615c5-194">뒤에 마침표를 입력 하는 때 IntelliSense 트리거되는 것을 알는 @Model 키워드, 속성 및 앨범 클래스에서 지 원하는 메서드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-194">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="615c5-195">보겠습니다 이제이 프로젝트를 다시 실행 하 고 저장소/세부 정보/5 URL을 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-195">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="615c5-196">아래와 같은 앨범의 세부 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-196">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="615c5-197">이제 저장소 찾아보기 동작 메서드에 대 한 유사한 업데이트를 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-197">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="615c5-198">ActionResult 반환 하도록 메서드를 업데이트 하 고 메서드 논리를 수정 하 여 새 장르 개체를 만들고 있으므로 보기로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-198">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="615c5-199">찾아보기 메서드 단추로 클릭 하 고 "추가 보기..."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-199">Right-click in the Browse method and select "Add View…"</span></span> <span data-ttu-id="615c5-200">상황에 맞는 메뉴에서 다음 보기를 강력한 형식의 추가 강력한 형식의 장르 클래스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-200">from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="615c5-201">업데이트는 &lt;h2&gt; 보기의 요소 (의 코드 /Views/Store/Browse.cshtml) 장르 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-201">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="615c5-202">이제이 프로젝트를 다시 실행 하 고 찾아보기/저장소/찾아보기 하겠습니다. 장르 디스코 URL = 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-202">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="615c5-203">찾아보기 페이지와 같은 아래에 표시를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-203">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="615c5-204">마지막으로, आ म च ी에 대 한 약간 더 복잡 한 업데이트는 **저장 인덱스** 작업 메서드와 뷰를 스토어에 모든 장르의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-204">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="615c5-205">단일 장르 뿐이 아닌 모델 개체는 장르 목록을 사용 하 여를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-205">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="615c5-206">저장소 인덱스 작업 메서드에서 고 이전에 모델 클래스로 장르를 선택 하 고 추가 단추를 눌러 처럼 뷰 추가 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-206">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="615c5-207">먼저 변경 합니다는 @model 하나만 대신 나타내려면 보기 여러 장르 제공 될 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-207">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="615c5-208">다음과 같이 /Store/Index.cshtml의 첫 번째 줄을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-208">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="615c5-209">작업 하는 여러 장르 개체를 저장할 수 있는 모델 개체와 함께 Razor 뷰 엔진을 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-209">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="615c5-210">IEnumerable에서는&lt;장르&gt; 목록 대신&lt;장르&gt; 일반적 이므로, IEnumerable 인터페이스를 지 원하는 모든 개체 형식에 나중에 모델 유형을 변경 하도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-210">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="615c5-211">그런 다음 아래 코드 완성 된 보기에에서 표시 된 대로 모델의 장르 개체 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-211">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="615c5-212">있는지 완벽 하 게 IntelliSense 지원에서는이 코드를 입력 하는 대로 입력할 때 있도록 공지 "@Model."</span><span class="sxs-lookup"><span data-stu-id="615c5-212">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="615c5-213">메서드 및 형식 Genre의 IEnumerable에서 지 원하는 속성 모두 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-213">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="615c5-214">우리의 "foreach" 루프 내 Visual Web Developer 임을 알고 각 항목 장르 형식의 IntelliSence 각각에 대해 표시 되므로 장르 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-214">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSence for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="615c5-215">다음으로, 스 캐 폴딩 기능 장르 개체를 검사 하 고 확인 하므로 전체를 반복 하 고 작성 하는 Name 속성이 했습니다 됩니다 각각. 또한 각 개별 항목에 대 한 편집, 정보 및 삭제 링크를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-215">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="615c5-216">활용 하는 저장소 관리자 인의 뒷부분에 나오는 살펴보겠습니다 하지만 지금은 간단한 목록 대신가 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-216">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="615c5-217">응용 프로그램을 실행 하 고 /Store 찾아보기, 개수와 장르 목록에 표시 되도록 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-217">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="615c5-218">페이지 간 링크 추가</span><span class="sxs-lookup"><span data-stu-id="615c5-218">Adding Links between pages</span></span>

<span data-ttu-id="615c5-219">현재 장르를 나열 하 여 /Store URL 일반 텍스트로 단순히 장르 이름을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-219">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="615c5-220">보겠습니다이 모양을 변경 할 수 있도록 하는 대신 일반 텍스트 대신 적절 한 저장소/찾아보기 URL에 대 한 장르 이름 링크를 클릭 하면 "Disco" / 저장소/찾아보기도 이동 되는 like 음악 장르? 장르 = Disco URL입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-220">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="615c5-221">이러한 링크를 사용 하 여 아래와 같은 코드 출력으로 우리의 \Views\Store\Index.cshtml 뷰 템플릿을 업데이트할 수 있습니다 **(에 입력 하지 않은-에 개선 하 여)**:</span><span class="sxs-lookup"><span data-stu-id="615c5-221">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="615c5-222">에 성공 하지만 하드 코드 된 문자열에 의존 하므로 나중에 문제를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-222">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="615c5-223">예를 들어, 컨트롤러의 이름을 바꾸려면 있으니까요 해야 우리의 원하는 코드를 업데이트 해야 하는 링크를 통해 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-223">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="615c5-224">다른 방법은 사용할 수는 HTML 도우미 메서드를 활용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-224">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="615c5-225">ASP.NET MVC는 다양 한이 같은 일반적인 작업을 수행 하는 보기 템플릿 코드에서 사용할 수 있는 HTML 도우미 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-225">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="615c5-226">Html.ActionLink() 도우미 메서드는은 특히 유용 한을 손쉽게 HTML 만들려는 &lt;는&gt; 연결 하는 URL로 인코딩된 URL 경로가 제대로 확인 같은 번거로울 세부 사항을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-226">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="615c5-227">Html.ActionLink() 링크에 필요한 만큼 많은 정보를 지정할 수는 몇 가지 다른 오버 로드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-227">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="615c5-228">가장 간단한 경우 고 링크 텍스트와 클라이언트에서 하이퍼링크를 클릭할 때 이동할 동작 메서드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-228">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="615c5-229">예를 들어 "/ 저장소 /" 된 링크 텍스트 이동에 저장소 "인덱스" 다음 호출을 사용 하는 저장소 세부 정보 페이지 index () 메서드를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-229">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="615c5-230">*참고:이 경우 하지 않은 해야 것 바로 연결 하 고 현재 뷰를 렌더링 하는 동일한 컨트롤러에서 다른 작업 때문에 컨트롤러의 이름을 지정 합니다.*</span><span class="sxs-lookup"><span data-stu-id="615c5-230">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="615c5-231">찾아보기 페이지에 대 한 링크는 세 가지 매개 변수를 사용 하는 Html.ActionLink 메서드의 다른 오버 로드에서는 하므로 매개 변수 전달, 하지만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-231">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="615c5-232">링크 텍스트는 장르 이름이 표시 됩니다</span><span class="sxs-lookup"><span data-stu-id="615c5-232">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="615c5-233">컨트롤러 동작 이름 (찾아보기)</span><span class="sxs-lookup"><span data-stu-id="615c5-233">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="615c5-234">(장르) 이름 및 값 (장르 이름)을 모두 지정 하는 경로 매개 변수 값</span><span class="sxs-lookup"><span data-stu-id="615c5-234">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="615c5-235">배치 한꺼번에 모두 여기 인지 어떻게 이러한 링크 저장소 인덱스 뷰를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-235">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="615c5-236">이제이 프로젝트를 다시 실행 하 고 /Store/ URL에 액세스 했습니다 장르 목록을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-236">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="615c5-237">클릭할 때 각각은 하이퍼링크 – us에 걸리는 우리의/저장소/찾아보기? 장르 =*[장르]* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-237">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="615c5-238">HTML 장르 목록에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="615c5-238">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]


>[!div class="step-by-step"]
<span data-ttu-id="615c5-239">[이전](mvc-music-store-part-2.md)
[다음](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="615c5-239">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
