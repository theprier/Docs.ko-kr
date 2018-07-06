---
uid: single-page-application/overview/templates/hottowel-template
title: Hot Towel 템플릿 | Microsoft Docs
author: madskristensen
description: HotTowel 템플릿
ms.author: aspnetcontent
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: 6145a34286ef113002b92d722e227005657098d9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825139"
---
<a name="hot-towel-template"></a><span data-ttu-id="92712-103">Hot Towel 템플릿</span><span class="sxs-lookup"><span data-stu-id="92712-103">Hot Towel template</span></span>
====================
<span data-ttu-id="92712-104">[제작: Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="92712-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="92712-105">John Papa에서 작성 되었습니다. Hot Towel MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="92712-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="92712-106">다운로드할 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="92712-107">Visual Studio 2012 용 hot Towel MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="92712-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="92712-108">Visual Studio 2013 용 hot Towel MVC 템플릿</span><span class="sxs-lookup"><span data-stu-id="92712-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="92712-109">핫 수건: 없으면 SPA 이동할 않으려고 하기 때문에!</span><span class="sxs-lookup"><span data-stu-id="92712-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>


<span data-ttu-id="92712-110">SPA를 작성 하 고 싶지만 시작 위치를 결정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="92712-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="92712-111">핫 수건을 사용 하 고 (초)에서 수 있고 SPA를 토대로 하는 데 필요한 모든 도구!</span><span class="sxs-lookup"><span data-stu-id="92712-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="92712-112">핫 수건 단일 페이지 응용 프로그램 (SPA) ASP.NET 사용 하 여 구축 하기 위한 좋은 시작점이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92712-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="92712-113">즉시 있습니다 제공 모듈형 구조 코드, 뷰 탐색, 데이터 바인딩, 다양 한 데이터 관리 및 간단 하지만 세련 된 스타일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="92712-114">핫 수건은 앱을 연결 하지에 집중할 수 있도록 SPA를 작성 하는 데 필요한 모든 것을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="92712-115">SPA를 빌드하는 방법을 자세히 알아봅니다 [John Papa의 비디오, 자습서 및 Pluralsight 과정](http://johnpapa.net/spa?vsix)합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>


## <a name="application-structure"></a><span data-ttu-id="92712-116">응용 프로그램 구조</span><span class="sxs-lookup"><span data-stu-id="92712-116">Application Structure</span></span>

<span data-ttu-id="92712-117">핫 수건 SPA 응용 프로그램을 정의 하는 JavaScript 및 HTML 파일을 포함 하는 앱 폴더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="92712-118">앱 폴더:</span><span class="sxs-lookup"><span data-stu-id="92712-118">Inside the App folder:</span></span>

- <span data-ttu-id="92712-119">durandal</span><span class="sxs-lookup"><span data-stu-id="92712-119">durandal</span></span>
- <span data-ttu-id="92712-120">서비스</span><span class="sxs-lookup"><span data-stu-id="92712-120">services</span></span>
- <span data-ttu-id="92712-121">viewmodel</span><span class="sxs-lookup"><span data-stu-id="92712-121">viewmodels</span></span>
- <span data-ttu-id="92712-122">뷰</span><span class="sxs-lookup"><span data-stu-id="92712-122">views</span></span>

<span data-ttu-id="92712-123">앱 폴더 모듈의 컬렉션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="92712-124">이러한 모듈 기능을 캡슐화 및 다른 모듈에 종속성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="92712-125">Views 폴더에는 HTML 응용 프로그램을 포함 하 고 viewmodels 폴더 보기 (일반적인 MVVM 패턴)에 대 한 프레젠테이션 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="92712-126">Services 폴더에는 응용 프로그램 예: HTTP 데이터 검색 또는 로컬 저장소 상호 작용 해야 할 수 있는 모든 공통 서비스를 보유할 수 있도록 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="92712-127">하기가 여러 viewmodel에 대 한 일반적인 다시 서비스 모듈의 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="92712-128">Asp.net 서버 쪽 응용 프로그램 구조</span><span class="sxs-lookup"><span data-stu-id="92712-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="92712-129">핫 수건 친숙 하 고 강력한 ASP.NET MVC 구조를 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="92712-130">앱\_시작</span><span class="sxs-lookup"><span data-stu-id="92712-130">App\_Start</span></span>
- <span data-ttu-id="92712-131">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="92712-131">Content</span></span>
- <span data-ttu-id="92712-132">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="92712-132">Controllers</span></span>
- <span data-ttu-id="92712-133">모델</span><span class="sxs-lookup"><span data-stu-id="92712-133">Models</span></span>
- <span data-ttu-id="92712-134">스크립트</span><span class="sxs-lookup"><span data-stu-id="92712-134">Scripts</span></span>
- <span data-ttu-id="92712-135">보기</span><span class="sxs-lookup"><span data-stu-id="92712-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="92712-136">주요 라이브러리</span><span class="sxs-lookup"><span data-stu-id="92712-136">Featured Libraries</span></span>

- <span data-ttu-id="92712-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="92712-137">ASP.NET MVC</span></span>
- <span data-ttu-id="92712-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="92712-138">ASP.NET Web API</span></span>
- <span data-ttu-id="92712-139">ASP.NET 웹 최적화-묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="92712-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="92712-140">[Breeze.js](http://Breezejs.com) -다양 한 데이터 관리</span><span class="sxs-lookup"><span data-stu-id="92712-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="92712-141">[Durandal.js](http://Durandaljs.com) -탐색 및 보기 구성</span><span class="sxs-lookup"><span data-stu-id="92712-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="92712-142">[Knockout.js](http://Knockoutjs.com) -데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="92712-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="92712-143">[Require.js](http://requirejs.org) -AMD 및 최적화를 사용 하 여 모듈화</span><span class="sxs-lookup"><span data-stu-id="92712-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="92712-144">[Toastr.js](http://jpapa.me/c7toastr) -팝업 메시지</span><span class="sxs-lookup"><span data-stu-id="92712-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="92712-145">[Twitter Bootstrap](http://twitter.github.com/bootstrap/) -강력한 CSS 스타일 지정</span><span class="sxs-lookup"><span data-stu-id="92712-145">[Twitter Bootstrap](http://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="92712-146">Visual Studio 2012 핫 수건 SPA 템플릿을 통해 설치</span><span class="sxs-lookup"><span data-stu-id="92712-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="92712-147">Visual Studio 2012 템플릿으로 핫 수건을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92712-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="92712-148">클릭 하기만 `File`  |  `New Project` 선택한 `ASP.NET MVC 4 Web Application`합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="92712-149">선택 된 ' 핫 수건 단일 페이지 응용 프로그램 "템플릿과 실행!</span><span class="sxs-lookup"><span data-stu-id="92712-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="92712-150">NuGet 패키지를 통해 설치</span><span class="sxs-lookup"><span data-stu-id="92712-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="92712-151">핫 수건 기존 빈 ASP.NET MVC 프로젝트를 확대 하는 NuGet 패키지를 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="92712-152">Nuget을 사용 하 여 설치 하 고 실행!</span><span class="sxs-lookup"><span data-stu-id="92712-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="92712-153">핫 수건에서 빌드하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="92712-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="92712-154">코드를 추가 하기만 하면!</span><span class="sxs-lookup"><span data-stu-id="92712-154">Simply start adding code!</span></span>

1. <span data-ttu-id="92712-155">사용자 고유의 서버 쪽 코드를 가급적 Entity Framework와 WebAPI (실제로 Breeze.js를 사용 하 여 우수한 성능을 나타내는) 추가</span><span class="sxs-lookup"><span data-stu-id="92712-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="92712-156">뷰를 추가 합니다 `App/views` 폴더</span><span class="sxs-lookup"><span data-stu-id="92712-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="92712-157">Viewmodel에 추가 된 `App/viewmodels` 폴더</span><span class="sxs-lookup"><span data-stu-id="92712-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="92712-158">새 보기에 HTML 및 Knockout 데이터 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="92712-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="92712-159">탐색 경로 업데이트 합니다. `shell.js`</span><span class="sxs-lookup"><span data-stu-id="92712-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="92712-160">HTML/JavaScript의 연습</span><span class="sxs-lookup"><span data-stu-id="92712-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="92712-161">Views/HotTowel/index.cshtml</span><span class="sxs-lookup"><span data-stu-id="92712-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="92712-162">index.cshtml에는 시작 경로 및 MVC 응용 프로그램에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="92712-163">모든 표준 메타 태그, css 링크 및 예상한 JavaScript 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="92712-164">본문은 단일 포함 `<div>` 즉, 모든 콘텐츠 (보기)을 배치할 요청 된 경우.</span><span class="sxs-lookup"><span data-stu-id="92712-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="92712-165">합니다 `@Scripts.Render` Require.js를 사용 하 여에 포함 된 응용 프로그램의 코드에 대 한 진입점을 실행 하는 `main.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="92712-166">시작 화면 앱을 로드 하는 동안 시작 화면을 만드는 방법을 보여 주기 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92712-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="92712-167">App/main.js</span><span class="sxs-lookup"><span data-stu-id="92712-167">App/main.js</span></span>

<span data-ttu-id="92712-168">`main.js` 파일에 앱이 로드 되는 즉시 실행 될 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="92712-169">탐색 경로 정의 뷰, 시작 설정 및 모든 설치/부트스트래핑 응용 프로그램의 데이터를 초기화 하는 등을 수행 하려는입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="92712-170">`main.js` 파일은 다양 한 시작 응용 프로그램 시작 하는 데 durandal의 모듈을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="92712-171">정의 문을 함수에 대해 사용할 수 있도록 모듈 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92712-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="92712-172">먼저 디버깅 메시지가 사용 됩니다, 콘솔 창에 수행 하는 응용 프로그램 이벤트에 대 한 메시지를 보내는.</span><span class="sxs-lookup"><span data-stu-id="92712-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="92712-173">App.start 코드를 응용 프로그램을 시작 하기 위해 durandal 프레임 워크를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92712-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="92712-174">규칙은 durandal 알고 모든 보기 및 viewmodels 각각 동일한 명명 된 폴더에 포함 된 되도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92712-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="92712-175">마지막으로 `app.setRoot` 로드를 시작 합니다 `shell` 사용 하 여 미리 정의 된 `entrance` 애니메이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="92712-176">보기</span><span class="sxs-lookup"><span data-stu-id="92712-176">Views</span></span>

<span data-ttu-id="92712-177">보기에서 발견 되는 `App/views` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="92712-178">shell.html</span><span class="sxs-lookup"><span data-stu-id="92712-178">shell.html</span></span>

<span data-ttu-id="92712-179">`shell.html` HTML에 대 한 마스터 레이아웃을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="92712-180">다른 보기의 모든 구성 됩니다 위치에 있는 프로그램 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="92712-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="92712-181">핫 수건 제공을 `shell` 이러한 세 가지 영역을 사용 하 여: 머리글, 콘텐츠 영역 및 바닥글을 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="92712-182">사용 하 여 로드 되는 이러한 각 지역 내용을 요청 하는 경우 다른 보기를 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="92712-183">`compose` 머리글 및 바닥글에 대 한 바인딩을 하드 코드 되지를 가리키도록 핫 수건에는 `nav` 및 `footer` 뷰, 각각.</span><span class="sxs-lookup"><span data-stu-id="92712-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="92712-184">섹션에 대 한 작성 바인딩을 `#content` 바인딩되는 `router` 모듈의 활성 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="92712-185">즉, 클릭 하면 해당 뷰이므로 탐색 링크는이 영역에 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92712-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="92712-186">nav.html</span><span class="sxs-lookup"><span data-stu-id="92712-186">nav.html</span></span>

<span data-ttu-id="92712-187">`nav.html` SPA에 대 한 탐색 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="92712-188">메뉴 구조를 배치할 수 있는, 예를 들어입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="92712-189">(Knockout을 사용 하 여) 바인딩된 데이터 인 경우가 많습니다 합니다 `router` 모듈에 정의 된 탐색을 표시 하는 `shell.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="92712-190">Knockout 찾습니다 데이터 바인딩 특성 및이를 바인딩합니다 합니다 `shell` viewmodel 탐색 경로 표시 하 고 (Twitter Bootstrap을 사용 하 여) progressbar를 표시할 경우를 `router` 모듈은 하나의 뷰에서 다른 (참조로 이동 하는 중 `router.isNavigating`).</span><span class="sxs-lookup"><span data-stu-id="92712-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="92712-191">home.html 및 details.html</span><span class="sxs-lookup"><span data-stu-id="92712-191">home.html and details.html</span></span>

<span data-ttu-id="92712-192">이러한 뷰는 사용자 지정 보기에 대 한 HTML을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="92712-193">경우는 `home` 링크를 `nav` 보기의 메뉴를 클릭 하면 합니다 `home` 보기의 콘텐츠 영역에 배치 됩니다는 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="92712-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="92712-194">이러한 뷰를 확대 또는 고유한 사용자 지정 보기를 사용 하 여 대체 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92712-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="92712-195">footer.html</span><span class="sxs-lookup"><span data-stu-id="92712-195">footer.html</span></span>

<span data-ttu-id="92712-196">`footer.html` 아래쪽의 바닥글에 표시 되는 HTML이 포함 된 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="92712-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="92712-197">ViewModels</span><span class="sxs-lookup"><span data-stu-id="92712-197">ViewModels</span></span>

<span data-ttu-id="92712-198">Viewmodel에서 발견 되는 `App/viewmodels` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="92712-199">shell.js</span><span class="sxs-lookup"><span data-stu-id="92712-199">shell.js</span></span>

<span data-ttu-id="92712-200">`shell` viewmodel에 바인딩되어 있는 함수 및 속성이 포함 된 `shell` 보기.</span><span class="sxs-lookup"><span data-stu-id="92712-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="92712-201">메뉴 탐색 바인딩이 있는 인 경우가 많습니다 (참조는 `router.mapNav` 논리).</span><span class="sxs-lookup"><span data-stu-id="92712-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="92712-202">home.js 및 details.js</span><span class="sxs-lookup"><span data-stu-id="92712-202">home.js and details.js</span></span>

<span data-ttu-id="92712-203">이러한 viewmodel 속성 및 함수에 바인딩되는 포함 된 `home` 보기.</span><span class="sxs-lookup"><span data-stu-id="92712-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="92712-204">또한 보기의 경우 프레젠테이션 논리를 포함 하 고 데이터 및 뷰 간의 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92712-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="92712-205">서비스</span><span class="sxs-lookup"><span data-stu-id="92712-205">Services</span></span>

<span data-ttu-id="92712-206">서비스 앱/서비스 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92712-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="92712-207">이상적으로 시작 하 고 원격 데이터를 게시 해야 하는 dataservice 모듈과 같은 향후 서비스를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92712-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="92712-208">logger.js</span><span class="sxs-lookup"><span data-stu-id="92712-208">logger.js</span></span>

<span data-ttu-id="92712-209">핫 수건 제공을 `logger` 서비스 폴더에서는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="92712-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="92712-210">`logger` 모듈 로깅 메시지를 콘솔 및 알림 팝업에서 사용자에 게 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="92712-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
