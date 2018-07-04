---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3 부: 보기 및 ViewModels | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 3 부에서는 보기 및 ViewModels를 설명합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 0cfdc2864221a0efc81eb362571c72f20eb05af8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368737"
---
<a name="part-3-views-and-viewmodels"></a><span data-ttu-id="a1392-104">3 부: 보기 및 ViewModels</span><span class="sxs-lookup"><span data-stu-id="a1392-104">Part 3: Views and ViewModels</span></span>
====================
<span data-ttu-id="a1392-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="a1392-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="a1392-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="a1392-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="a1392-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="a1392-109">3 부에서는 보기 및 ViewModels를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-109">Part 3 covers Views and ViewModels.</span></span>


<span data-ttu-id="a1392-110">지금까지에서는 했습니다만 된 문자열을 반환 컨트롤러 작업에서.</span><span class="sxs-lookup"><span data-stu-id="a1392-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="a1392-111">컨트롤러의 작동 방식을 파악 하는 유용한 방법 이지만 하지는 원하는 실제 웹 응용 프로그램을 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="a1392-112">HTML 사이트를 방문 하는 브라우저를 다시 생성 하는 더 나은 방법을 사용할 예정 – 템플릿 파일 HTML 콘텐츠를 보다 쉽게 사용자 지정에 사용 하는 우리를 반송 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="a1392-113">이것이 뷰 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="a1392-114">보기 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="a1392-114">Adding a View template</span></span>

<span data-ttu-id="a1392-115">템플릿 보기를 사용 하려면 ActionResult를 반환 하도록 HomeController 인덱스 메서드를 변경 하 고 아래와 같은 View()를 반환 하도록 하겠습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="a1392-116">위의 변경을 나타냅니다.이 반환 되는 대신 문자열 대신 "View"를 사용 하 여 결과 다시 생성 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="a1392-117">이제 프로젝트에 적절 한 보기 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="a1392-118">이렇게 하려면에서는 인덱스 작업 메서드 내에 텍스트 커서를 배치 다음 마우스 오른쪽 단추로 클릭 고 "추가 보기"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="a1392-119">뷰 추가 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="a1392-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a1392-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="a1392-121">"뷰 추가" 대화 상자를 사용 하면 빠르고 쉽게 보기 템플릿 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="a1392-122">"추가 보기" 기본적으로 대화 상자를 사용 하는 작업 메서드를 일치 시킬 수 있도록 만드는 보기 템플릿의 이름을 미리 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="a1392-123">우리의 HomeController의 index () 작업 메서드 내에서 "추가 보기" 상황에 맞는 메뉴를 사용 하기 때문에 위의 "뷰 추가" 대화 상자에 "Index" 기본적으로 미리 채워진 뷰 이름으로</span><span class="sxs-lookup"><span data-stu-id="a1392-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="a1392-124">에서는이 대화 상자에서 옵션 중 하나를 변경 하려면 추가 단추 클릭 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="a1392-125">추가 단추를 클릭 하면 Visual Web Developer는 존재 하지 않는 경우 폴더를 만들면 \Views\Home 디렉터리에 우리 회사에 뷰 템플릿에 새 Index.cshtml 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="a1392-126">"Index.cshtml" 파일의 이름 및 폴더 위치는 중요 하 고 기본 ASP.NET MVC 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="a1392-127">디렉터리 이름, \Views\Home, HomeController 라는 컨트롤러-일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="a1392-128">보기 템플릿 이름으로 인덱스 보기를 표시 하는 컨트롤러 동작 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="a1392-129">ASP.NET MVC를 사용 하면 뷰를 반환 하려면이 명명 규칙을 사용할 때 이름 또는 뷰 템플릿의 위치를 명시적으로 지정할 필요가 없도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="a1392-130">기본적으로 렌더링 됩니다 \Views\Home\Index.cshtml 보기 템플릿에서 HomeController 내에서 아래와 같은 코드를 작성할 때:</span><span class="sxs-lookup"><span data-stu-id="a1392-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="a1392-131">Visual Web Developer가 만들어지고 "뷰 추가" 대화 상자 내에서 "추가" 단추를 클릭 한 후 "Index.cshtml" 보기 템플릿이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="a1392-132">Index.cshtml의 콘텐츠는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="a1392-133">이 보기에는 ASP.NET Web Forms 및 ASP.NET MVC의 이전 버전에 사용 되는 Web Forms 뷰 엔진 보다 더 간결한는 Razor 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="a1392-134">Web Forms 뷰 엔진은 ASP.NET MVC 3에서 계속 사용할 수 있지만 많은 개발자 들이 Razor 보기 엔진 ASP.NET MVC 개발 잘 맞는.</span><span class="sxs-lookup"><span data-stu-id="a1392-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="a1392-135">처음 세 줄 ViewBag.Title를 사용 하 여 페이지 제목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="a1392-136">에서는에서는 작동 방식을 자세히 먼저 곧 보겠습니다 업데이트 텍스트 제목 텍스트를 살펴보고 페이지 보기.</span><span class="sxs-lookup"><span data-stu-id="a1392-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="a1392-137">업데이트를 &lt;h2&gt; 아래와 같이 "이 되는 홈 페이지"를 태그 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="a1392-138">새 텍스트 홈 페이지에 표시 되는 응용 프로그램은 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="a1392-139">일반적인 사이트 요소에 대 한 레이아웃을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a1392-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="a1392-140">대부분의 웹 사이트에 여러 페이지 간에 공유 되는 내용이: 탐색, 바닥글, 로고 이미지, 스타일 시트 참조 등입니다. Razor 보기 엔진 쉽게이 라는 페이지를 사용 하 여 관리할 \_Layout.cshtml에 자동으로 만들어진/뷰/공유 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="a1392-141">이 폴더 아래에 나와 있는 내용을 보려면 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="a1392-142">개별 뷰에서 콘텐츠를 표시 합니다 @RenderBody() 명령 및 벗어나는 표시 하고자 하는 일반적인 내용을 추가할 수 있습니다는 \_Layout.cshtml 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="a1392-143">바로 위의 템플릿에 추가 해 보겠습니다 사이트에서 모든 페이지에는 홈 페이지 및 저장소 영역에 대 한 링크를 사용 하 여 공용 헤더 할 우리의 MVC Music Store 하 려 @RenderBody() 문입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="a1392-144">스타일 시트를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="a1392-144">Updating the StyleSheet</span></span>

<span data-ttu-id="a1392-145">빈 프로젝트 템플릿 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="a1392-146">일부 추가 CSS 및 이미지 이제에 추가 해 보겠습니다이 사이트의 모양과 느낌을 정의 하는 디자이너 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="a1392-147">업데이트 된 CSS 파일 및 이미지에서 사용할 수 있는 MvcMusicStore Assets.zip의 콘텐츠 디렉터리에 포함 된 [MVC 음악 스토어](https://github.com/evilDave/MVC-Music-Store)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="a1392-148">Windows 탐색기에서 둘 다 선택 하 고 아래와 같이 Visual Web developer에서 솔루션의 콘텐츠 폴더에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="a1392-149">기존 Site.css 파일을 덮어쓸 것인지 확인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="a1392-150">예를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="a1392-151">응용 프로그램의 콘텐츠 폴더에 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="a1392-152">이제 응용 프로그램을 실행 하 고 홈 페이지에서 변경 내용이 어떻게 표시 되는지 확인 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="a1392-153">변경 된 기능을 검토해 보겠습니다: The HomeController의 Index 작업 메서드에 찾아서 코드 보기 템플릿은 표준 명명 규칙을 따른 때문에 "반환 View()"를 호출 하는 경우에 \Views\Home\Index.cshtmlView 템플릿을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="a1392-154">홈 페이지 \Views\Home\Index.cshtml 보기 템플릿 내에 정의 된 간단한 환영 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="a1392-155">홈 페이지를 사용 하 여이 \_Layout.cshtml 템플릿 이므로 환영 메시지는 표준 사이트 HTML 레이아웃 내에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="a1392-156">정보 보기를 전달 하는 모델을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a1392-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="a1392-157">방금 하드 코드 된 HTML을 표시 하는 뷰 템플릿이 되지 매우 흥미로운 웹 사이트를 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="a1392-158">동적 웹 사이트를 만들려면에서는 대신 하려고 우리의 보기 템플릿에 컨트롤러 작업에서 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="a1392-159">모델-뷰-컨트롤러 패턴 모델 이란 용어는 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="a1392-160">대개 데이터베이스의 테이블에 모델 개체에 해당 하지만 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="a1392-161">ActionResult를 반환 하는 컨트롤러 작업 메서드에서 보기로 모델 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="a1392-162">이렇게 하면 적절 한 HTML 응답을 생성 하는 데는 컨트롤러를 응답을 생성 한 다음 보기 템플릿에이 정보를 전달 하는 데 필요한 모든 정보를 명확 하 게 패키지를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="a1392-163">작업에서 확인 하 여 이해 하 고 시작 하겠습니다 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="a1392-164">먼저 스토어 내 앨범 및 장르를 표현 하는 일부 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="a1392-165">장르 클래스를 만들어 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="a1392-166">프로젝트 내에서 "Models" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "클래스 추가" 옵션을 선택 "Genre.cs" 파일의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="a1392-167">생성 된 클래스에는 공용 문자열 이름 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="a1392-168">*참고: 궁금한 경우에는 {get; 설정;} 표기법은 수행 하는 C#의 자동 구현 속성 기능을 사용 합니다. 지원 필드를 선언 하기를 요구 하지 않고 속성의 이점을 제공 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a1392-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="a1392-169">다음으로 제목과 장르 속성이 있는 앨범 클래스 (Album.cs 라는)를 만들려면 동일한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="a1392-170">이제 모델에서 동적 정보를 표시 하는 뷰를 사용 하 여 StoreController 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="a1392-171">지금-데모용 우리의 앨범 요청 ID를 기준으로 이름이 것 인 경우-아래 보기와 같이 해당 정보를 표시할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="a1392-172">단일 앨범에 대 한 정보를 표시 하므로 저장소 세부 정보 동작을 변경 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="a1392-173">맨 위에 "using" 문을 추가 합니다 **StoreControllers** 되므로 앨범 클래스를 사용 하려고 할 때마다 MvcMusicStore.Models.Album를 입력할 필요가 없습니다 MvcMusicStore.Models 네임 스페이스를 포함 하도록 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="a1392-174">해당 클래스의 "using" 섹션을 표시 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="a1392-175">다음으로, 업데이트 세부 정보 컨트롤러 작업 문자열 보다는 ActionResult 반환 되도록 HomeController의 인덱스 메서드를 사용 하 여 했던 것 처럼.</span><span class="sxs-lookup"><span data-stu-id="a1392-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="a1392-176">이제 보기로 앨범 개체를 반환 하는 논리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="a1392-177">이 자습서의 뒷부분에서 우리는 검색 데이터 데이터베이스에서 하지만 지금은 사용 "더미 데이터"를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="a1392-178">*참고: C#을 사용 하 여 잘 모르는 경우으로 추정할 수 있습니다는 앨범 변수는 런타임에 바인딩된은 var을 사용 하 여 의미 합니다. C# 컴파일러를 사용 하 여 형식 유추 기반으로 새로운는 앨범 형식의 해당 앨범을 인지 합니다. 변수를 할당 하 고 컴파일 시간 검사 및 Visual Studio 코드 편집기를 얻게 되므로 로컬 앨범 변수의 앨범 유형으로 컴파일하는 –는 올바르지 않습니다. 이 옵션을 지원 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a1392-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="a1392-179">이제 HTML 응답을 생성 하는 데는 앨범을 사용 하는 템플릿 보기를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="a1392-180">작업을 수행 하기 전에 프로젝트를 빌드하려면 뷰 추가 대화 상자에서 새로 만든된 앨범 클래스에 대 한 알 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="a1392-181">메뉴 항목 Debug⇨Build MvcMusicStore를 선택 하 여 프로젝트를 빌드할 수 있습니다 (추가 크레딧을 사용할 수 있습니다 Ctrl-Shift-B 바로 가기 프로젝트를 빌드하려면).</span><span class="sxs-lookup"><span data-stu-id="a1392-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="a1392-182">지원 클래스를 설정 했으므로 이제 준비가 보기 템플릿은 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="a1392-183">세부 정보 메서드 내에서 마우스 상황에 맞는 메뉴에서 "추가 보기..."를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="a1392-184">HomeController를 사용 하 여 전에 수행한 것과 같이 새 보기 템플릿을 만들려면 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="a1392-185">StoreController에서 만드는 것 때문에 기본적으로 생성 됩니다 \Views\Store\Index.cshtml 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="a1392-186">달리 이전 하겠습니다 "강력한 형식의 만들기" 보기 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="a1392-187">그런 다음 하겠습니다 "보기 데이터-클래스" drop downlist 내 "앨범" 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="a1392-188">이렇게 하면 개체를 사용 하 여 전달할 앨범을 필요로 하는 뷰 템플릿을 만들려면 "뷰 추가" 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a1392-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="a1392-189">"추가" 단추를 클릭할 때 \Views\Store\Details.cshtml 보기 템플릿은 만들어집니다, 다음 코드를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="a1392-190">이 보기는 강력한 앨범 클래스를 나타내는 첫 번째 줄을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="a1392-191">Razor 보기 엔진 이해 되었습니다 통과 했다고 앨범 개체를 쉽게 모델 속성에 액세스 하는 Visual Web Developer 편집기의 IntelliSense의 이점은 있을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="a1392-192">업데이트를 &lt;h2&gt; 태그는 Album Title 속성이 다음과 같이 표시할 줄을 수정 하 여 표시 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="a1392-193">뒤에 마침표를 입력 하면 IntelliSense 트리거한 확인는 @Model 키워드, 앨범 클래스를 지 원하는 메서드와 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="a1392-194">보겠습니다 이제 프로젝트를 다시 실행 하 고 저장소/세부 정보/5 URL을 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="a1392-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="a1392-195">아래와 같은 앨범의 세부 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="a1392-196">이제 저장소 찾아보기 동작 메서드에 대 한 유사한 업데이트를 만들 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="a1392-197">ActionResult를 반환 하도록 메서드를 업데이트 하 고 새 장르 개체를 만들고 뷰를 반환 하므로 메서드는 논리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="a1392-198">뷰를 강력한 형식의 추가한 찾아보기 메서드를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 "추가 보기..."를 선택 강력한 형식의 장르 클래스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="a1392-199">업데이트를 &lt;h2&gt; 뷰에서 요소 코드 (/Views/Store/Browse.cshtml) 장르 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="a1392-200">이제 프로젝트를 다시 실행 하 고/저장소/찾아보기로 이동 하겠습니다. 장르 = Disco URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="a1392-201">아래와 비슷하게 표시 되지만 찾아보기 페이지를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="a1392-202">마지막으로 약간 더 복잡 한 업데이트를 확인 합니다 **인덱스 저장** 작업 메서드 및 스토어에서 모든 장르 목록을 표시 하려면 보기.</span><span class="sxs-lookup"><span data-stu-id="a1392-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="a1392-203">장르 목록 장르를 방금 아닌은 모델 개체를 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="a1392-204">저장소 인덱스 작업 메서드에서 마우스 추가 뷰 이전 모델 클래스로 장르를 선택 하 고 추가 단추를 눌러 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="a1392-205">에서는 변경 먼저는 @model 하나만 대신 선언 뷰는 몇 가지 장르 예상 수를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="a1392-206">첫 번째 부분은 /Store/Index.cshtml을 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="a1392-207">몇 가지 장르 개체를 보유할 수 있는 모델 개체를 사용 하 여 작동 하는 Razor 보기 엔진을 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="a1392-208">IEnumerable을 사용 하는 것&lt;장르&gt; 목록 대신&lt;장르&gt; 보다 일반적인 이므로 IEnumerable 인터페이스를 지 원하는 모든 개체 형식에는 모델 형식을 나중에 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="a1392-209">그런 다음 아래 코드는 완료 된 보기에 표시 된 대로 모델의 장르 개체 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="a1392-210">있습니다 전체 IntelliSense 지원이이 코드를 입력으로 입력 하면 되도록 "@Model."</span><span class="sxs-lookup"><span data-stu-id="a1392-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="a1392-211">모든 메서드 및 장르 형식의 IEnumerable을 지 원하는 속성을 참조 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="a1392-212">이 "foreach" 루프 내에서 Visual Web Developer 임을 알고 있습니다 각 항목 Genre 형식의 각 IntelliSence 보 장르 형식.</span><span class="sxs-lookup"><span data-stu-id="a1392-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSence for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="a1392-213">다음으로, 스 캐 폴딩 기능은 장르 개체를 검사 및 각 되어 Name 속성을 반복 하 고 작성 하 있도록 결정 합니다. 또한 각 개별 항목에 대 한 편집, 세부 정보 및 삭제 링크를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="a1392-214">에서는 사용 하는 나중에 저장소 관리자에에서 있지만 지금은 목록이 간단한 대신 하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="a1392-215">응용 프로그램을 실행 하 고 /Store 이동, 개수 및 장르 목록을 모두 표시 되도록을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="a1392-216">페이지 간 링크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-216">Adding Links between pages</span></span>

<span data-ttu-id="a1392-217">/Store URL 현재 장르를 나열 하는 일반 텍스트로 단순히 장르 이름을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="a1392-218">바꿔보겠습니다 일반 텍스트 대신 대신 수 있도록 적절 한 저장소/찾아보기 URL 장르 이름 링크를 "Disco" 이동/저장소/찾아보기와 같은 음악 장르를 클릭할 수 있도록? 장르 = Disco URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="a1392-219">다음이 링크를 사용 하 여 아래와 같은 코드 출력 \Views\Store\Index.cshtml 보기 템플릿은 업데이트 수 **(이 입력 하지 않은-를 개선 하려고)**:</span><span class="sxs-lookup"><span data-stu-id="a1392-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="a1392-220">이런 방법도 있지만 하드 코드 된 문자열에 의존 하므로 나중에 문제를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="a1392-221">예를 들어 컨트롤러를 바꾸려면 싶으면 업데이트 해야 하는 링크에 대 한 확인 코드를 통해 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="a1392-222">대 안으로 사용할 수 있습니다는 HTML 도우미 메서드를 활용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="a1392-223">ASP.NET MVC는 다양 한이 같은 일반적인 작업을 수행 하는 보기 템플릿 코드에서 사용할 수 있는 HTML 도우미 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="a1392-224">Html.ActionLink() 도우미 메서드는 특히 유용 합니다 및 HTML 빌드 쉽게 &lt;는&gt; 링크 및 URL 경로 URL로 인코딩된 제대로 되었는지 같은 성가신 세부 사항을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="a1392-225">Html.ActionLink() 링크에 필요한 만큼 많은 정보를 지정할 수 있도록 몇 가지 다른 오버 로드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="a1392-226">가장 간단한 경우에만 링크 텍스트 및 클라이언트에서 하이퍼링크를 클릭할 때 이동할 작업 메서드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="a1392-227">예를 들어, "저장소 /" "이동 하는 저장소 인덱스" 다음 호출을 사용 하 여 링크 텍스트를 사용 하 여 저장소 세부 정보 페이지의 index () 메서드를 연결할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="a1392-228">*참고:이 예에서는 필요가 없었습니다 현재 보기를 렌더링 하는 동일한 컨트롤러 내의 다른 작업에만 연결 하는 것 때문에 컨트롤러의 이름을 지정 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a1392-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="a1392-229">찾아보기 페이지에 대 한 링크는 3 개의 매개 변수는 Html.ActionLink 메서드의 다른 오버 로드 사용 하므로 매개 변수 전달, 그러나 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="a1392-230">장르 이름을 표시 하는 링크 텍스트</span><span class="sxs-lookup"><span data-stu-id="a1392-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="a1392-231">컨트롤러 작업 이름 (찾아보기)</span><span class="sxs-lookup"><span data-stu-id="a1392-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="a1392-232">경로 매개 변수 값을 이름 (장르)과 값 (장르 이름)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="a1392-233">모두를 함께 여기서는 저장소 인덱스 보기에 이러한 링크를 작성 하는 방법을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="a1392-234">이제 프로젝트를 다시 실행 하 고 /Store/ URL에 액세스 하는 경우 장르 목록이 표시 됩니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="a1392-235">클릭할 때 하이퍼링크 – 각 장르에는 우리의/저장소 / 찾아보기 걸립니다? 장르 =*[장르]* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="a1392-236">장르 목록에 대 한 HTML은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1392-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]


> [!div class="step-by-step"]
> <span data-ttu-id="a1392-237">[이전](mvc-music-store-part-2.md)
> [다음](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="a1392-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
