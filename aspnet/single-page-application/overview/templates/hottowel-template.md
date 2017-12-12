---
uid: single-page-application/overview/templates/hottowel-template
title: "핫 수건 템플릿 | Microsoft Docs"
author: madskristensen
description: "HotTowel 서식 파일"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/09/2013
ms.topic: article
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: bfc6e2c884c422f44e8be5f4f29554ae86f7ecb6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="hot-towel-template"></a><span data-ttu-id="df2fb-103">핫 수건 서식 파일</span><span class="sxs-lookup"><span data-stu-id="df2fb-103">Hot Towel template</span></span>
====================
<span data-ttu-id="df2fb-104">여 [Kristensen Mads](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="df2fb-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="df2fb-105">John 예가 핫 수건 MVC 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="df2fb-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="df2fb-106">버전을 다운로드 하려면를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="df2fb-107">Visual Studio 2012에 대 한 핫 수건 MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="df2fb-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="df2fb-108">Visual Studio 2013에 대 한 핫 수건 MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="df2fb-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)


> <span data-ttu-id="df2fb-109">핫 수건: 하나가 없어서 SPA로 이동 하려고 하므로!</span><span class="sxs-lookup"><span data-stu-id="df2fb-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>


<span data-ttu-id="df2fb-110">SPA를 작성 하려고 하지만 시작 위치를 결정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="df2fb-111">핫 수건을 사용 하 여 및 초에서 해야 합니다.에 빌드하는 데 필요한 모든 도구와 한 SPA!</span><span class="sxs-lookup"><span data-stu-id="df2fb-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="df2fb-112">핫 수건은 단일 페이지 응용 프로그램 (SPA) ASP.NET으로 작성 하기 위한 좋은 출발점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="df2fb-113">즉시 있습니다 제공 모듈형 구조 코드, 보기 탐색, 데이터 바인딩, 다양 한 데이터 관리 및 스타일을 간단 하지만 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="df2fb-114">핫 수건 배관 하지 앱에 집중할 수는 SPA를 만드는 데 필요한 모든를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="df2fb-115">SPA를 구축 하는 방법에 대 한 자세한 정보 [John 예의 비디오, 자습서 및 Pluralsight 교육 과정](http://johnpapa.net/spa?vsix)합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>


## <a name="application-structure"></a><span data-ttu-id="df2fb-116">응용 프로그램 구조</span><span class="sxs-lookup"><span data-stu-id="df2fb-116">Application Structure</span></span>

<span data-ttu-id="df2fb-117">핫 수건 SPA 응용 프로그램을 정의 하는 JavaScript 및 HTML 파일을 포함 하는 응용 프로그램 폴더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="df2fb-118">응용 프로그램 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-118">Inside the App folder:</span></span>

- <span data-ttu-id="df2fb-119">durandal</span><span class="sxs-lookup"><span data-stu-id="df2fb-119">durandal</span></span>
- <span data-ttu-id="df2fb-120">서비스</span><span class="sxs-lookup"><span data-stu-id="df2fb-120">services</span></span>
- <span data-ttu-id="df2fb-121">viewmodel</span><span class="sxs-lookup"><span data-stu-id="df2fb-121">viewmodels</span></span>
- <span data-ttu-id="df2fb-122">뷰</span><span class="sxs-lookup"><span data-stu-id="df2fb-122">views</span></span>

<span data-ttu-id="df2fb-123">응용 프로그램 폴더는 모듈의 컬렉션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="df2fb-124">이러한 모듈의 기능을 캡슐화 하 고 다른 모듈에 대해 종속성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="df2fb-125">Views 폴더에는 응용 프로그램에 대 한 HTML 포함 되 고 viewmodel 폴더 뷰 (공통 MVVM 패턴)에 대 한 프레젠테이션 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="df2fb-126">서비스 폴더는 응용 프로그램 예: HTTP 데이터 검색 또는 로컬 저장소의 상호 작용 해야 하는 모든 공통 서비스 보유할 수 있도록 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="df2fb-127">것에 대 한 여러 viewmodel 서비스 모듈에서 코드 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="df2fb-128">ASP.NET MVC 서버 쪽 응용 프로그램 구조</span><span class="sxs-lookup"><span data-stu-id="df2fb-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="df2fb-129">핫 수건 친숙 하 고 강력한 ASP.NET MVC 구조 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="df2fb-130">응용 프로그램\_시작</span><span class="sxs-lookup"><span data-stu-id="df2fb-130">App\_Start</span></span>
- <span data-ttu-id="df2fb-131">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="df2fb-131">Content</span></span>
- <span data-ttu-id="df2fb-132">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="df2fb-132">Controllers</span></span>
- <span data-ttu-id="df2fb-133">모델</span><span class="sxs-lookup"><span data-stu-id="df2fb-133">Models</span></span>
- <span data-ttu-id="df2fb-134">스크립트</span><span class="sxs-lookup"><span data-stu-id="df2fb-134">Scripts</span></span>
- <span data-ttu-id="df2fb-135">보기</span><span class="sxs-lookup"><span data-stu-id="df2fb-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="df2fb-136">추천된 라이브러리</span><span class="sxs-lookup"><span data-stu-id="df2fb-136">Featured Libraries</span></span>

- <span data-ttu-id="df2fb-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="df2fb-137">ASP.NET MVC</span></span>
- <span data-ttu-id="df2fb-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="df2fb-138">ASP.NET Web API</span></span>
- <span data-ttu-id="df2fb-139">ASP.NET 웹 최적화-묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="df2fb-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="df2fb-140">[Breeze.js](http://Breezejs.com) -다양 한 데이터 관리</span><span class="sxs-lookup"><span data-stu-id="df2fb-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="df2fb-141">[Durandal.js](http://Durandaljs.com) -탐색 및 보기 구성</span><span class="sxs-lookup"><span data-stu-id="df2fb-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="df2fb-142">[Knockout.js](http://Knockoutjs.com) -데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="df2fb-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="df2fb-143">[Require.js](http://requirejs.org) -모듈화 AMD 및 최적화</span><span class="sxs-lookup"><span data-stu-id="df2fb-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="df2fb-144">[Toastr.js](http://jpapa.me/c7toastr) -팝업 메시지</span><span class="sxs-lookup"><span data-stu-id="df2fb-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="df2fb-145">[부트스트랩 twitter](http://twitter.github.com/bootstrap/) -강력한 CSS 스타일 지정</span><span class="sxs-lookup"><span data-stu-id="df2fb-145">[Twitter Bootstrap](http://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="df2fb-146">Visual Studio 2012 핫 수건 SPA 서식 파일을 통해 설치</span><span class="sxs-lookup"><span data-stu-id="df2fb-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="df2fb-147">Visual Studio 2012 템플릿으로 핫 수건을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="df2fb-148">클릭 하기만 `File`  |  `New Project` 선택 `ASP.NET MVC 4 Web Application`합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="df2fb-149">다음을 선택 된 ' 핫 수건 단일 페이지 응용 프로그램 "템플릿과 실행!</span><span class="sxs-lookup"><span data-stu-id="df2fb-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="df2fb-150">NuGet 패키지를 통해 설치</span><span class="sxs-lookup"><span data-stu-id="df2fb-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="df2fb-151">핫 수건 기존 빈 ASP.NET MVC 프로젝트를 확대 하는 NuGet 패키지 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="df2fb-152">Nuget을 사용 하 여 설치 하 고 실행!</span><span class="sxs-lookup"><span data-stu-id="df2fb-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="df2fb-153">핫 수건 토대로 방법</span><span class="sxs-lookup"><span data-stu-id="df2fb-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="df2fb-154">단순히 코드 추가 시작!</span><span class="sxs-lookup"><span data-stu-id="df2fb-154">Simply start adding code!</span></span>

1. <span data-ttu-id="df2fb-155">가급적 Entity Framework와 WebAPI (Breeze.js와 줄)에 사용자 고유의 서버 쪽 코드 추가</span><span class="sxs-lookup"><span data-stu-id="df2fb-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="df2fb-156">뷰를 추가 `App/views` 폴더</span><span class="sxs-lookup"><span data-stu-id="df2fb-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="df2fb-157">Viewmodel에 추가 `App/viewmodels` 폴더</span><span class="sxs-lookup"><span data-stu-id="df2fb-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="df2fb-158">새 보기에 HTML 및 Knockout 데이터 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="df2fb-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="df2fb-159">탐색 경로 업데이트 합니다.`shell.js`</span><span class="sxs-lookup"><span data-stu-id="df2fb-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="df2fb-160">HTML/JavaScript의 연습</span><span class="sxs-lookup"><span data-stu-id="df2fb-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="df2fb-161">Views/HotTowel/index.cshtml</span><span class="sxs-lookup"><span data-stu-id="df2fb-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="df2fb-162">index.cshtml는 시작 경로 및 MVC 응용 프로그램에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="df2fb-163">모든 표준 메타 태그, css 링크 및 예상 되는 JavaScript 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="df2fb-164">포함 하는 하나의 본문 `<div>` 즉, 모든 콘텐츠 (views) 배치 될 위치 요청 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="df2fb-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="df2fb-165">`@Scripts.Render` Require.js를 사용 하 여에 포함 되어 있는 응용 프로그램의 코드에 대 한 진입점을 실행 하는 `main.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="df2fb-166">시작 화면을 응용 프로그램에서 로드 되는 동안 시작 화면을 만드는 방법을 보여 주기 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="df2fb-167">App/main.js</span><span class="sxs-lookup"><span data-stu-id="df2fb-167">App/main.js</span></span>

<span data-ttu-id="df2fb-168">`main.js` 파일에 코드가 사용자 응용 프로그램이 로드 되는 즉시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="df2fb-169">탐색 경로 정의 뷰, 시작 및 모든 설치/부트스트래핑 응용 프로그램의 데이터를 priming 등을 수행 하려면 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="df2fb-170">`main.js` 시작 응용 프로그램 준비 수 있도록 durandal의 모듈의 여러 파일을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="df2fb-171">정의 문의 함수에 대해 사용할 수 있도록 모듈 종속성을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="df2fb-172">먼저는 디버깅 메시지를 사용할 수을 수행 하 고 콘솔 창에 있는 이벤트에 대 한 메시지를 보낼입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="df2fb-173">App.start 코드 응용 프로그램을 시작 하기 위해 durandal 프레임 워크를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="df2fb-174">규칙은 durandal 모든 보기를 알고 있으며 각각와 같은 명명 된 폴더에 포함 된 viewmodel 되도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="df2fb-175">마지막으로 `app.setRoot` 로드를 시작 하기 전에 `shell` 사용 하 여 미리 정의 된 `entrance` 애니메이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="df2fb-176">보기</span><span class="sxs-lookup"><span data-stu-id="df2fb-176">Views</span></span>

<span data-ttu-id="df2fb-177">보기에서 발견 되는 `App/views` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="df2fb-178">shell.html</span><span class="sxs-lookup"><span data-stu-id="df2fb-178">shell.html</span></span>

<span data-ttu-id="df2fb-179">`shell.html` HTML에 대 한 마스터 레이아웃을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="df2fb-180">다른 보기의 모든 작성 되는 곳 쪽에 프로그램 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="df2fb-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="df2fb-181">핫 수건 제공는 `shell` 이러한 3 개의 영역으로: 헤더, 콘텐츠 영역 및 바닥글입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="df2fb-182">이러한 각 지역와 함께 로드 됩니다 내용을 요청 될 때 다른 보기를 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="df2fb-183">`compose` 머리글 및 바닥글에 대 한 바인딩을 하드 코드 되지를 가리키도록 핫 수건에는 `nav` 및 `footer` 각각 봅니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="df2fb-184">섹션에 대 한 작성 바인딩을 `#content` 바인딩되는 `router` 모듈의 활성 항목.</span><span class="sxs-lookup"><span data-stu-id="df2fb-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="df2fb-185">즉,를 클릭할 때 해당 보기가 탐색 링크를이 영역에 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="df2fb-186">nav.html</span><span class="sxs-lookup"><span data-stu-id="df2fb-186">nav.html</span></span>

<span data-ttu-id="df2fb-187">`nav.html` 는 SPA에 대 한 탐색 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="df2fb-188">메뉴 구조 배치할 수 있는 위치, 예를 들어입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="df2fb-189">자주이 통해 데이터 바인딩된 (Knockout 사용)는 `router` 모듈에 정의 된 탐색을 표시 하는 `shell.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="df2fb-190">데이터 바인딩 특성 및이를 바인딩합니다 knockout 찾습니다는 `shell` viewmodel 탐색 경로 표시 하 고 progressbar (Twitter 부트스트랩 사용)을 표시 하기 경우는 `router` 하나의 뷰에서 다른 (참조 탐색 중에 모듈은 `router.isNavigating`).</span><span class="sxs-lookup"><span data-stu-id="df2fb-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="df2fb-191">home.html 및 details.html</span><span class="sxs-lookup"><span data-stu-id="df2fb-191">home.html and details.html</span></span>

<span data-ttu-id="df2fb-192">이러한 뷰는 사용자 지정 보기에 대 한 HTML을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="df2fb-193">때는 `home` 연결에 `nav` 보기의 메뉴를 클릭 하면는 `home` 보기의 콘텐츠 영역에 표시 됩니다는 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="df2fb-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="df2fb-194">이러한 뷰를 확장 또는 사용자 지정 보기 아래 템플릿으로 바뀝니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="df2fb-195">footer.html</span><span class="sxs-lookup"><span data-stu-id="df2fb-195">footer.html</span></span>

<span data-ttu-id="df2fb-196">`footer.html` 바닥글의 맨 아래에 표시 되는 HTML이 포함 되어는 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="df2fb-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="df2fb-197">Viewmodel</span><span class="sxs-lookup"><span data-stu-id="df2fb-197">ViewModels</span></span>

<span data-ttu-id="df2fb-198">Viewmodel에서 발견 되는 `App/viewmodels` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="df2fb-199">shell.js</span><span class="sxs-lookup"><span data-stu-id="df2fb-199">shell.js</span></span>

<span data-ttu-id="df2fb-200">`shell` viewmodel 포함 속성 및 함수에 바인딩되는 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="df2fb-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="df2fb-201">메뉴 탐색 바인딩을 발견 되 이름인 경우가 많습니다 (참조는 `router.mapNav` 논리).</span><span class="sxs-lookup"><span data-stu-id="df2fb-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="df2fb-202">home.js 및 details.js</span><span class="sxs-lookup"><span data-stu-id="df2fb-202">home.js and details.js</span></span>

<span data-ttu-id="df2fb-203">이러한 viewmodel 포함 속성 및 함수에 바인딩되는 `home` 보기.</span><span class="sxs-lookup"><span data-stu-id="df2fb-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="df2fb-204">또한 보기에 대 한 프레젠테이션 논리를 포함 하 고 데이터와 뷰 간에 작업은 합니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="df2fb-205">서비스</span><span class="sxs-lookup"><span data-stu-id="df2fb-205">Services</span></span>

<span data-ttu-id="df2fb-206">서비스 응용 프로그램/서비스 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="df2fb-207">이상적으로 가져오고 원격 데이터를 게시 하는 일을 담당 하는 dataservice 모듈과 같은 향후 서비스를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="df2fb-208">logger.js</span><span class="sxs-lookup"><span data-stu-id="df2fb-208">logger.js</span></span>

<span data-ttu-id="df2fb-209">핫 수건 제공는 `logger` 서비스 폴더에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="df2fb-210">`logger` 모듈 로깅 메시지를 콘솔 및 알림 팝업에서 사용자에 게 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="df2fb-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
