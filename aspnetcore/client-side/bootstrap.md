---
title: 부트스트랩 및 ASP.NET Core를 사용 하 여 멋진 고 반응이 빠른 사이트 빌드
author: ardalis
description: ASP.NET Core를 사용 하 여 반응 형 웹 앱을 개발 하기 위한 Bootstrap을 사용 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: client-side/bootstrap
ms.openlocfilehash: 1ccf33b299739f5aa963a53feb70b44b290443ca
ms.sourcegitcommit: d53e0cc71542b92de867bcce51575b054886f529
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829502"
---
# <a name="build-beautiful-responsive-sites-with-bootstrap-and-aspnet-core"></a><span data-ttu-id="b3f7c-103">부트스트랩 및 ASP.NET Core를 사용 하 여 멋진 고 반응이 빠른 사이트 빌드</span><span class="sxs-lookup"><span data-stu-id="b3f7c-103">Build beautiful, responsive sites with Bootstrap and ASP.NET Core</span></span>

<a name="bootstrap-index"></a>

<span data-ttu-id="b3f7c-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="b3f7c-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="b3f7c-105">부트스트랩은 현재 응답성이 뛰어난 웹 응용 프로그램을 개발 하기 위한 가장 인기 있는 웹 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-105">Bootstrap is currently the most popular web framework for developing responsive web applications.</span></span> <span data-ttu-id="b3f7c-106">프런트 엔드 디자인 및 개발 전문가 든 초보 든 다양 한 기능 및 웹 사이트를 사용 하 여 사용자 환경을 향상 시킬 수 있는 혜택을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-106">It offers a number of features and benefits that can improve your users' experience with your web site, whether you're a novice at front-end design and development or an expert.</span></span> <span data-ttu-id="b3f7c-107">부트스트랩은 CSS 및 JavaScript 파일 집합으로 배포 되 고 태블릿과 데스크톱을 효율적으로 휴대폰의 웹 사이트 또는 응용 프로그램 확장을 쉽게 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-107">Bootstrap is deployed as a set of CSS and JavaScript files, and is designed to help your website or application scale efficiently from phones to tablets to desktops.</span></span>

## <a name="get-started"></a><span data-ttu-id="b3f7c-108">시작</span><span class="sxs-lookup"><span data-stu-id="b3f7c-108">Get started</span></span>

<span data-ttu-id="b3f7c-109">부트스트랩을 사용 하 여 시작 하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-109">There are several ways to get started with Bootstrap.</span></span> <span data-ttu-id="b3f7c-110">Visual Studio에서 새 웹 응용 프로그램을 시작 하는, 하는 경우에 사례 부트스트랩을 미리 설치 되어 ASP.NET Core 기본 시작 템플릿을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-110">If you're starting a new web application in Visual Studio, you can choose the default starter template for ASP.NET Core, in which case Bootstrap will come pre-installed:</span></span>

![시작 템플릿 솔루션 보기에서 부트스트랩](bootstrap/_static/bootstrap-in-starter-template.png)

<span data-ttu-id="b3f7c-112">ASP.NET Core에 부트스트랩 추가 프로젝트를 추가 하기만 하면 됩니다 *bower.json* 종속성으로:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-112">Adding Bootstrap to an ASP.NET Core project is simply a matter of adding it to *bower.json* as a dependency:</span></span>

[!code-json[](../common/samples/WebApplication1/bower.json?highlight=5)]

<span data-ttu-id="b3f7c-113">이것이 Bootstrap ASP.NET Core 프로젝트에 추가 하는 권장된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-113">This is the recommended way to add Bootstrap to an ASP.NET Core project.</span></span>

<span data-ttu-id="b3f7c-114">또한 NuGet, Bower 및 npm, 등의 여러 패키지 관리자 중 하나를 사용 하 여 부트스트랩을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-114">You can also install bootstrap using one of several package managers, such as Bower, npm, or NuGet.</span></span> <span data-ttu-id="b3f7c-115">각각의 경우에서 프로세스는 거의 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-115">In each case, the process is essentially the same:</span></span>

### <a name="bower"></a><span data-ttu-id="b3f7c-116">Bower</span><span class="sxs-lookup"><span data-stu-id="b3f7c-116">Bower</span></span>

```console
bower install bootstrap
```

### <a name="npm"></a><span data-ttu-id="b3f7c-117">npm</span><span class="sxs-lookup"><span data-stu-id="b3f7c-117">npm</span></span>

```console
npm install bootstrap
```

### <a name="nuget"></a><span data-ttu-id="b3f7c-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="b3f7c-118">NuGet</span></span>

```console
Install-Package bootstrap
```

> [!NOTE]
> <span data-ttu-id="b3f7c-119">ASP.NET Core에서 부트스트랩 Bower 통해 같은 클라이언트 쪽 종속성을 설치 하는 것이 좋습니다 (사용 하 여 *bower.json*위에 표시 된 것 처럼).</span><span class="sxs-lookup"><span data-stu-id="b3f7c-119">The recommended way to install client-side dependencies like Bootstrap in ASP.NET Core is via Bower (using *bower.json*, as shown above).</span></span> <span data-ttu-id="b3f7c-120">Npm/nuget을 사용 하 여 얼마나 쉽게 부트스트랩 추가할 수 있습니다 다른 종류의 이전 버전의 ASP.NET 포함 하 여 웹 응용 프로그램을 보여 주기 위해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-120">The use of npm/NuGet are shown to demonstrate how easily Bootstrap can be added to other kinds of web applications, including earlier versions of ASP.NET.</span></span>

<span data-ttu-id="b3f7c-121">부트스트랩의 고유한 로컬 버전을 참조 하는 경우에 사용할 모든 페이지에서를 참조 하는 것이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-121">If you're referencing your own local versions of Bootstrap, you'll need to reference them in any pages that will use it.</span></span> <span data-ttu-id="b3f7c-122">프로덕션 환경에서 CDN을 사용 하 여 부트스트랩을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-122">In production you should reference bootstrap using a CDN.</span></span> <span data-ttu-id="b3f7c-123">기본 ASP.NET Core 사이트 템플릿의 합니다 *_Layout.cshtml* 파일은 다음과 같은 하므로:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-123">In the default ASP.NET Core site template, the *_Layout.cshtml* file does so like this:</span></span>

[!code-html[](../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=9,13,51,59)]

> [!NOTE]
> <span data-ttu-id="b3f7c-124">부트스트랩 jQuery 플러그 사용 하려는 경우에 jQuery 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-124">If you're going to be using any of Bootstrap's jQuery plugins, you will also need to reference jQuery.</span></span>

## <a name="basic-templates-and-features"></a><span data-ttu-id="b3f7c-125">기본 템플릿 및 기능</span><span class="sxs-lookup"><span data-stu-id="b3f7c-125">Basic templates and features</span></span>

<span data-ttu-id="b3f7c-126">가장 기본적인 부트스트랩 템플릿와 매우 비슷하며 합니다 *_Layout.cshtml* 파일 위의 고 탐색 하 고 페이지의 나머지 부분을 렌더링 하는 위치에 대 한 기본 메뉴가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-126">The most basic Bootstrap template looks very much like the *_Layout.cshtml* file shown above, and simply includes a basic menu for navigation and a place to render the rest of the page.</span></span>

### <a name="basic-navigation"></a><span data-ttu-id="b3f7c-127">기본 탐색</span><span class="sxs-lookup"><span data-stu-id="b3f7c-127">Basic navigation</span></span>

<span data-ttu-id="b3f7c-128">기본 템플릿 집합을 사용 하 여 `<div>` 맨 위 탐색 모음 및 페이지의 본문을 렌더링 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-128">The default template uses a set of `<div>` elements to render a top navbar and the main body of the page.</span></span> <span data-ttu-id="b3f7c-129">HTML5를 사용 하는 경우에 첫 번째를 바꿀 수 있습니다 `<div>` 사용 하 여 태그를 `<nav>` 동일한 효과를 얻을 때 태그 하지만 정확한 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-129">If you're using HTML5, you can replace the first `<div>` tag with a `<nav>` tag to get the same effect, but with more precise semantics.</span></span> <span data-ttu-id="b3f7c-130">이 첫 번째 내 `<div>` 다른 몇 가지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-130">Within this first `<div>` you can see there are several others.</span></span> <span data-ttu-id="b3f7c-131">첫 번째는 `<div>` "container" 한 다음에 두 개 이상의 클래스를 사용 하 여 `<div>` 요소: "탐색 모음 헤더" 및 "탐색 모음 축소"입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-131">First, a `<div>` with a class of "container", and then within that, two more `<div>` elements: "navbar-header" and "navbar-collapse".</span></span> <span data-ttu-id="b3f7c-132">탐색 모음 헤더 div 특정 최소 너비를 3 개 가로 줄을 보여 주는 아래 화면 때 표시 되는 단추가 포함 됩니다 (소위는 "햄버거 아이콘").</span><span class="sxs-lookup"><span data-stu-id="b3f7c-132">The navbar-header div includes a button that will appear when the screen is below a certain minimum width, showing 3 horizontal lines (a so-called "hamburger icon").</span></span> <span data-ttu-id="b3f7c-133">아이콘 순수 HTML 및 CSS;를 사용 하 여 렌더링 이미지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-133">The icon is rendered using pure HTML and CSS; no image is required.</span></span> <span data-ttu-id="b3f7c-134">이 각 아이콘을 표시 하는 코드는 <span> 흰색 막대 중 하나를 렌더링 하는 태그:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-134">This is the code that displays the icon, with each of the <span> tags rendering one of the white bars:</span></span>

```html
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>
```

<span data-ttu-id="b3f7c-135">또한 왼쪽 상단에 표시 되는 응용 프로그램 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-135">It also includes the application name, which appears in the top left.</span></span> <span data-ttu-id="b3f7c-136">주 탐색 메뉴를 렌더링 하는 `<ul>` 내의 두 번째 div 요소 홈, 정보 및 연락처에 대 한 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-136">The main navigation menu is rendered by the `<ul>` element within the second div, and includes links to Home, About, and Contact.</span></span> <span data-ttu-id="b3f7c-137">탐색을 아래 각 페이지의 본문은 다른 렌더링 됩니다 `<div>`, "container" 및 "본문 콘텐츠" 클래스를 사용 하 여 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-137">Below the navigation, the main body of each page is rendered in another `<div>`, marked with the "container" and "body-content" classes.</span></span> <span data-ttu-id="b3f7c-138">간단한 기본 \_페이지의 내용을 페이지 및 간단한와 관련 된 특정 뷰에서 렌더링 되는 여기에 표시 된 레이아웃 파일 `<footer>` 끝에 추가 되는 `<div>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-138">In the simple default \_Layout file shown here, the contents of the page are rendered by the specific View associated with the page, and then a simple `<footer>` is added to the end of the `<div>` element.</span></span> <span data-ttu-id="b3f7c-139">페이지에 대 한 기본 제공 모양을 사용 하 여 볼 수 있습니다이 템플릿에서:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-139">You can see how the built-in About page appears using this template:</span></span>

![페이지에 대 한](bootstrap/_static/about-page-wide.png)

<span data-ttu-id="b3f7c-141">오른쪽 위의 "햄버거" 단추를 사용 하 여 축소 된 탐색 모음 창의 특정 너비 보다 낮게 떨어질 때 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-141">The collapsed navbar, with "hamburger" button in the top right, appears when the window drops below a certain width:</span></span>

![햄버거 메뉴를 사용 하 여 페이지에 대 한](bootstrap/_static/about-page-hamburger.png)

<span data-ttu-id="b3f7c-143">페이지의 맨 위에서 아래로 슬라이드 하는 세로 서랍에서 메뉴 항목 표시 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-143">Clicking the icon reveals the menu items in a vertical drawer that slides down from the top of the page:</span></span>

![햄버거 메뉴를 사용 하 여 페이지에 대 한 확장](bootstrap/_static/about-page-hamburger-open.png)

### <a name="typography-and-links"></a><span data-ttu-id="b3f7c-145">입력 체계 및 링크</span><span class="sxs-lookup"><span data-stu-id="b3f7c-145">Typography and links</span></span>

<span data-ttu-id="b3f7c-146">사이트의 기본 입력 체계, 색 및 CSS 파일에 서식 지정 하는 링크를 설정 하는 부트스트랩 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-146">Bootstrap sets up the site's basic typography, colors, and link formatting in its CSS file.</span></span> <span data-ttu-id="b3f7c-147">테이블, 단추, 폼 요소, 이미지, 등에 대 한 기본 스타일을 포함 하는이 CSS 파일 ([자세한](http://getbootstrap.com/css/)).</span><span class="sxs-lookup"><span data-stu-id="b3f7c-147">This CSS file includes default styles for tables, buttons, form elements, images, and more ([learn more](http://getbootstrap.com/css/)).</span></span> <span data-ttu-id="b3f7c-148">다음 표 형태 레이아웃 시스템을 기능은 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-148">One particularly useful feature is the grid layout system, covered next.</span></span>

### <a name="grids"></a><span data-ttu-id="b3f7c-149">표</span><span class="sxs-lookup"><span data-stu-id="b3f7c-149">Grids</span></span>

<span data-ttu-id="b3f7c-150">부트스트랩의 가장 인기 있는 기능 중 하나는 그리드 레이아웃 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-150">One of the most popular features of Bootstrap is its grid layout system.</span></span> <span data-ttu-id="b3f7c-151">최신 웹 응용 프로그램은 사용 하지 않아야 합니다 `<table>` 대신 실제 테이블 형식 데이터에이 요소의 사용을 제한 하는 레이아웃에 대 한 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-151">Modern web applications should avoid using the `<table>` tag for layout, instead restricting the use of this element to actual tabular data.</span></span> <span data-ttu-id="b3f7c-152">대신, 열 및 행을 레이아웃할 수를 사용 하 여 `<div>` 요소 및 해당 CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-152">Instead, columns and rows can be laid out using a series of `<div>` elements and the appropriate CSS classes.</span></span> <span data-ttu-id="b3f7c-153">표를 세로로 표시 좁은 화면에서는 같은 휴대폰의 레이아웃을 조정 하는 기능을 포함 하 여이 방법의 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-153">There are several advantages to this approach, including the ability to adjust the layout of grids to display vertically on narrow screens, such as on phones.</span></span>

<span data-ttu-id="b3f7c-154">[부트스트랩 그리드 레이아웃 시스템](http://getbootstrap.com/css/#grid) 12 열에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-154">[Bootstrap's grid layout system](http://getbootstrap.com/css/#grid) is based on twelve columns.</span></span> <span data-ttu-id="b3f7c-155">이 번호는 1, 2, 3 또는 4 개의 열으로 균등 하 게 나눌 수 있습니다 및 열 너비는 1 내에 달라질 수 있습니다 때문에 선택 된/세로 화면 너비의 12입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-155">This number was chosen because it can be divided evenly into 1, 2, 3, or 4 columns, and column widths can vary to within 1/12th of the vertical width of the screen.</span></span> <span data-ttu-id="b3f7c-156">컨테이너를 시작 해야를 표 형태 레이아웃 시스템을 사용 하려면 `<div>` 는 행을 추가 하 고 `<div>`다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-156">To start using the grid layout system, you should begin with a container `<div>` and then add a row `<div>`, as shown here:</span></span>

```html
<div class="container">
    <div class="row">
        ...
    </div>
</div>
```

<span data-ttu-id="b3f7c-157">다음으로, 추가할 `<div>` 각 열에 대 한 요소 열 개수를 지정 하는 `<div>` "col-md-"로 시작 하는 CSS 클래스의 일부로 (12)에서 차지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-157">Next, add additional `<div>` elements for each column, and specify the number of columns that `<div>` should occupy (out of 12) as part of a CSS class starting with "col-md-".</span></span> <span data-ttu-id="b3f7c-158">예를 들어 단순히 동일한 크기의 두 열이 포함 하려는 경우 "col-md-6"의 클래스 각각에 대해 사용할 때.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-158">For instance, if you want to simply have two columns of equal size, you would use a class of "col-md-6" for each one.</span></span> <span data-ttu-id="b3f7c-159">이 경우 "md" 약어 "보통"를 참조 하는 데스크톱 컴퓨터 표준 크기의 디스플레이 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-159">In this case "md" is short for "medium" and refers to standard-sized desktop computer display sizes.</span></span> <span data-ttu-id="b3f7c-160">네 가지 다른 옵션을 선택할 수 있습니다 않으며 각각에 사용할 더 높은 너비 (따라서 화면 너비에 관계 없이 수정 될 레이아웃을 하려는 경우에 xs 클래스를 지정할 수 있습니다)를 재정의 하지 않는 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-160">There are four different options you can choose from, and each will be used for higher widths unless overridden (so if you want the layout to be fixed regardless of screen width, you can just specify xs classes).</span></span>

<span data-ttu-id="b3f7c-161">CSS 클래스 접두사</span><span class="sxs-lookup"><span data-stu-id="b3f7c-161">CSS Class Prefix</span></span> | <span data-ttu-id="b3f7c-162">장치 계층</span><span class="sxs-lookup"><span data-stu-id="b3f7c-162">Device Tier</span></span> | <span data-ttu-id="b3f7c-163">너비</span><span class="sxs-lookup"><span data-stu-id="b3f7c-163">Width</span></span>
:---: | :---: | :---:
<span data-ttu-id="b3f7c-164">col-xs-</span><span class="sxs-lookup"><span data-stu-id="b3f7c-164">col-xs-</span></span> | <span data-ttu-id="b3f7c-165">휴대폰</span><span class="sxs-lookup"><span data-stu-id="b3f7c-165">Phones</span></span> | <span data-ttu-id="b3f7c-166">< 768px</span><span class="sxs-lookup"><span data-stu-id="b3f7c-166">< 768px</span></span>
<span data-ttu-id="b3f7c-167">col-sm-</span><span class="sxs-lookup"><span data-stu-id="b3f7c-167">col-sm-</span></span> | <span data-ttu-id="b3f7c-168">태블릿</span><span class="sxs-lookup"><span data-stu-id="b3f7c-168">Tablets</span></span> | <span data-ttu-id="b3f7c-169">> = 768px</span><span class="sxs-lookup"><span data-stu-id="b3f7c-169">>= 768px</span></span>
<span data-ttu-id="b3f7c-170">col-md-</span><span class="sxs-lookup"><span data-stu-id="b3f7c-170">col-md-</span></span> | <span data-ttu-id="b3f7c-171">데스크톱</span><span class="sxs-lookup"><span data-stu-id="b3f7c-171">Desktops</span></span> | <span data-ttu-id="b3f7c-172">> = 992px</span><span class="sxs-lookup"><span data-stu-id="b3f7c-172">>= 992px</span></span>
<span data-ttu-id="b3f7c-173">col-lg-</span><span class="sxs-lookup"><span data-stu-id="b3f7c-173">col-lg-</span></span> | <span data-ttu-id="b3f7c-174">더 큰 데스크톱 디스플레이</span><span class="sxs-lookup"><span data-stu-id="b3f7c-174">Larger Desktop Displays</span></span> | <span data-ttu-id="b3f7c-175">> = 1200px</span><span class="sxs-lookup"><span data-stu-id="b3f7c-175">>= 1200px</span></span>

<span data-ttu-id="b3f7c-176">두 열 모두 "col-md-6" 결과 레이아웃을 사용 하 여 데스크톱 해상도에서 두 개의 열 수 있지만 소형 장치 (또는 더 좁은 브라우저 창을 바탕 화면)에서 사용자를 쉽게 볼 수 있도록 렌더링 될 때 이러한 두 열 세로로 쌓입니다를 지정 하는 경우 가로로 스크롤할 필요 없이 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-176">When specifying two columns both with "col-md-6" the resulting layout will be two columns at desktop resolutions, but these two columns will stack vertically when rendered on smaller devices (or a narrower browser window on a desktop), allowing users to easily view content without the need to scroll horizontally.</span></span>

<span data-ttu-id="b3f7c-177">부트스트랩은 기본적으로 항상 단일 열 레이아웃을 둘 이상의 열을 사용 하려는 경우 열을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-177">Bootstrap will always default to a single-column layout, so you only need to specify columns when you want more than one column.</span></span> <span data-ttu-id="b3f7c-178">에 명시적으로 지정 하려는 `<div>` 모든 12 열을 사용 하는 큰 장치 계층의 동작을 재정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-178">The only time you would want to explicitly specify that a `<div>` take up all 12 columns would be to override the behavior of a larger device tier.</span></span> <span data-ttu-id="b3f7c-179">여러 장치 계층 클래스를 지정할 때 특정 지점에서 열 렌더링을 다시 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-179">When specifying multiple device tier classes, you may need to reset the column rendering at certain points.</span></span> <span data-ttu-id="b3f7c-180">만 특정 뷰포트 내에서 표시 되는 clearfix div를 추가 합니다. 이렇게 할를 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-180">Adding a clearfix div that's only visible within a certain viewport can achieve this, as shown here:</span></span>

![좁은 문자열과 와이드 뷰포트 표](bootstrap/_static/narrow-and-wide-viewport-grid.png)

<span data-ttu-id="b3f7c-182">위의 예제에서는 1과 2 공유 "md" 레이아웃에 행 2와 3 "xs" 레이아웃에 행을 공유 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-182">In the above example, One and Two share a row in the "md" layout, while Two and Three share a row in the "xs" layout.</span></span> <span data-ttu-id="b3f7c-183">clearfix 없이 `<div>`, 2 및 3 제대로 표시 되지 않는 "xs" 보기 (하나만, 4 및 5 나와 있는 참고)에서:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-183">Without the clearfix `<div>`, Two and Three are not shown correctly in the "xs" view (note that only One, Four, and Five are shown):</span></span>

![clearfix 사용 하지 않고 표](bootstrap/_static/grid-without-clearfix.png)

<span data-ttu-id="b3f7c-185">이 예제에서는 단일 행만 `<div>` 를 사용한 부트스트랩 여전히는 대부분 레이아웃 및 열의 스택 알아서 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-185">In this example, only a single row `<div>` was used, and Bootstrap still mostly did the right thing with regard to the layout and stacking of the columns.</span></span> <span data-ttu-id="b3f7c-186">행을 지정 해야 하는 일반적으로 `<div>` 각 가로 행에 대 한 레이아웃을 차지 하며 물론 내부에 다른 부트스트랩 그리드를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-186">Typically, you should specify a row `<div>` for each horizontal row your layout requires, and of course you can nest Bootstrap grids within one another.</span></span> <span data-ttu-id="b3f7c-187">작업을 수행 하면 각 중첩 된 표 형태 열 클래스를 사용 하 여 다음 세분화할 수 있는 요소 배치는 너비의 100%를 차지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-187">When you do, each nested grid will occupy 100% of the width of the element in which it's placed, which can then be subdivided using column classes.</span></span>

### <a name="jumbotron"></a><span data-ttu-id="b3f7c-188">Jumbotron</span><span class="sxs-lookup"><span data-stu-id="b3f7c-188">Jumbotron</span></span>

<span data-ttu-id="b3f7c-189">Visual Studio 2012 또는 2013에서 기본 ASP.NET Core MVC 템플릿을 사용한 경우 아마도 실행 중인 Jumbotron을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-189">If you've used the default ASP.NET Core MVC templates in Visual Studio 2012 or 2013, you've probably seen the Jumbotron in action.</span></span> <span data-ttu-id="b3f7c-190">동작, rotator, 또는 유사한 요소에 대 한 호출 큰 배경 이미지를 표시 하려면 사용할 수 있는 페이지의 큰 전자 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-190">It refers to a large full-width section of a page that can be used to display a large background image, a call to action, a rotator, or similar elements.</span></span> <span data-ttu-id="b3f7c-191">jumbotron에 페이지를 추가 하려면 추가 `<div>` "jumbotron" 클래스를 제공 하 고 컨테이너를 배치 `<div>` 내부 콘텐츠 추가 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-191">To add a jumbotron to a page, simply add a `<div>` and give it a class of "jumbotron", then place a container `<div>` inside and add your content.</span></span> <span data-ttu-id="b3f7c-192">기본 머리글 표시를 jumbotron를 사용 하는 페이지에 대 한 표준 쉽게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-192">We can easily adjust the standard About page to use a jumbotron for the main headings it displays:</span></span>

![jumbotron 예제](bootstrap/_static/jumbotron.png)

### <a name="buttons"></a><span data-ttu-id="b3f7c-194">단추</span><span class="sxs-lookup"><span data-stu-id="b3f7c-194">Buttons</span></span>

<span data-ttu-id="b3f7c-195">기본 단추 클래스 및 해당 색은 아래 그림에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-195">The default button classes and their colors are shown in the figure below.</span></span>

![테마가 지정 된 단추](bootstrap/_static/theme-buttons.png)

### <a name="badges"></a><span data-ttu-id="b3f7c-197">배지</span><span class="sxs-lookup"><span data-stu-id="b3f7c-197">Badges</span></span>

<span data-ttu-id="b3f7c-198">배지 탐색 항목 옆에 있는 작은, 일반적으로 숫자 설명선을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-198">Badges refer to small, usually numeric callouts next to a navigation item.</span></span> <span data-ttu-id="b3f7c-199">업데이트의 존재 여부 메시지 또는 알림을 대기의 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-199">They can indicate a number of messages or notifications waiting, or the presence of updates.</span></span> <span data-ttu-id="b3f7c-200">이러한 배지를 지정 하는 것은 추가 하기만 `<span>` "배지"의 클래스를 사용 하 여 텍스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-200">Specifying such badges is as simple as adding a `<span>` containing the text, with a class of "badge":</span></span>

![테마가 지정 된 배지](bootstrap/_static/theme-badges.png)

### <a name="alerts"></a><span data-ttu-id="b3f7c-202">경고</span><span class="sxs-lookup"><span data-stu-id="b3f7c-202">Alerts</span></span>

<span data-ttu-id="b3f7c-203">응용 프로그램의 사용자에 게 일종의 알림, 경고 또는 오류 메시지를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-203">You may need to display some kind of notification, alert, or error message to your application's users.</span></span> <span data-ttu-id="b3f7c-204">표준 경고 클래스를 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-204">That's where the standard alert classes are useful.</span></span> <span data-ttu-id="b3f7c-205">연결 된 색 구성표를 사용 하 여 4 개의 서로 다른 심각도 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-205">There are four different severity levels with associated color schemes:</span></span>

![테마가 지정 된 경고](bootstrap/_static/theme-alerts.png)

### <a name="navbars-and-menus"></a><span data-ttu-id="b3f7c-207">탐색 모음 및 메뉴</span><span class="sxs-lookup"><span data-stu-id="b3f7c-207">Navbars and menus</span></span>

<span data-ttu-id="b3f7c-208">이 레이아웃을 표준 탐색 모음에 이미 포함 되어 있습니다 하지만 부트스트랩 테마 추가 스타일 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-208">Our layout already includes a standard navbar, but the Bootstrap theme supports additional styling options.</span></span> <span data-ttu-id="b3f7c-209">에서는 보다 가로로 기본 설정에 같은 추가 하위 탐색 항목을 플라이 아웃 메뉴에는 navbar를 세로로 표시 되도록 쉽게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-209">We can also easily opt to display the navbar vertically rather than horizontally if that's preferred, as well as adding sub-navigation items in flyout menus.</span></span> <span data-ttu-id="b3f7c-210">탭 스트립 같은 간단한 탐색 메뉴의 맨 위에 빌드됩니다 `<ul>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-210">Simple navigation menus, like tab strips, are built on top of `<ul>` elements.</span></span> <span data-ttu-id="b3f7c-211">이러한 바로 CSS 클래스 "탐색" 및 "탐색 탭"을 사용 하 여 제공 하 여 매우 간단 하 게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-211">These can be created very simply by just providing them with the CSS classes "nav" and "nav-tabs":</span></span>

![테마가 지정 된 탭 스트립](bootstrap/_static/theme-tabstrips.png)

<span data-ttu-id="b3f7c-213">시각화에는 마찬가지로 빌드됩니다 되지만 좀 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-213">Navbars are built similarly, but are a bit more complex.</span></span> <span data-ttu-id="b3f7c-214">사용 하 여 시작을 `<nav>` 또는 `<div>` 컨테이너 div는 나머지 요소를 보유 "탐색"의 클래스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-214">They start with a `<nav>` or `<div>` with a class of "navbar", within which a container div holds the rest of the elements.</span></span> <span data-ttu-id="b3f7c-215">페이지 헤더에 있는 이미 navbar을 포함-다음 중 하 나와 간단히 확장이 드롭다운 메뉴에 대 한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-215">Our page includes a navbar in its header already – the one shown below simply expands on this, adding support for a dropdown menu:</span></span>

![테마가 지정 된 탐색 모음](bootstrap/_static/theme-navbars.png)

### <a name="additional-elements"></a><span data-ttu-id="b3f7c-217">추가 요소</span><span class="sxs-lookup"><span data-stu-id="b3f7c-217">Additional elements</span></span>

<span data-ttu-id="b3f7c-218">기본 테마 스트라이프 보기에 대 한 지원을 비롯 하 여 보기 좋게 서식이 지정 된 스타일에서 HTML 테이블을 주도록도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-218">The default theme can also be used to present HTML tables in a nicely formatted style, including support for striped views.</span></span> <span data-ttu-id="b3f7c-219">비슷하게 단추의 스타일을 사용 하 여 레이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-219">There are labels with styles that are similar to those of the buttons.</span></span> <span data-ttu-id="b3f7c-220">표준 HTML 외 추가 스타일 옵션을 지 원하는 사용자 지정 드롭다운 메뉴를 만들 수 있습니다 `<select>` 같은 기본 시작 사이트에서 이미 사용 하는 시각화와 함께 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-220">You can create custom Dropdown menus that support additional styling options beyond the standard HTML `<select>` element, along with Navbars like the one our default starter site is already using.</span></span> <span data-ttu-id="b3f7c-221">진행률 표시줄을 할 경우 여러 스타일 목록 그룹 제목 및 콘텐츠를 포함 하는 패널 및 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-221">If you need a progress bar, there are several styles to choose from, as well as List Groups and panels that include a title and content.</span></span> <span data-ttu-id="b3f7c-222">여기서는 표준 부트스트랩 테마 내의 추가 옵션 탐색:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-222">Explore additional options within the standard Bootstrap Theme here:</span></span>

[http://getbootstrap.com/examples/theme/](http://getbootstrap.com/examples/theme/)

## <a name="more-themes"></a><span data-ttu-id="b3f7c-223">추가 테마</span><span class="sxs-lookup"><span data-stu-id="b3f7c-223">More themes</span></span>

<span data-ttu-id="b3f7c-224">해당 CSS의 일부나 전부를 재정의 하 여 색 및 스타일을 사용자 고유의 응용 프로그램의 요구 사항에 맞게 조정 표준 부트스트랩 테마를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-224">You can extend the standard Bootstrap theme by overriding some or all of its CSS, adjusting the colors and styles to suit your own application's needs.</span></span> <span data-ttu-id="b3f7c-225">바로 사용할 수 있는 테마에서 시작 하려는 경우 몇 가지 테마 갤러리 온라인 WrapBootstrap.com (있음, 다양 한 상업용 테마) 및 Bootswatch.com (제공 하는 사용 가능한 테마)와 같은 부트스트랩 테마의 특수화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-225">If you'd like to start from a ready-made theme, there are several theme galleries available online that specialize in Bootstrap themes, such as WrapBootstrap.com (which has a variety of commercial themes) and Bootswatch.com (which offers free themes).</span></span> <span data-ttu-id="b3f7c-226">일부 유료 서식 파일 사용 가능한 다양 한 차트 및 계기를 사용 하 여 많은 양의 관리 메뉴 및 대시보드에 대 한 다양 한 지원 같은 기본 부트스트랩 테마를 기반으로 하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-226">Some of the paid templates available provide a great deal of functionality on top of the basic Bootstrap theme, such as rich support for administrative menus, and dashboards with rich charts and gauges.</span></span> <span data-ttu-id="b3f7c-227">인기 유료 템플릿의 예는 다음 스크린샷에 표시 된 Inspinia.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-227">An example of a popular paid template is Inspinia, which is shown in the following screenshot:</span></span>

![예제에서는 테마 inspinia](bootstrap/_static/theme-inspinia.png)

<span data-ttu-id="b3f7c-229">부트스트랩 테마를 변경 하려는 경우 배치 합니다 *bootstrap.css* 에서 원하는 테마에 대 한 파일을 **wwwroot/css** 폴더에서 참조를 변경 하 고 *_Layout.cshtml* 지정 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-229">If you want to change your Bootstrap theme, put the *bootstrap.css* file for the theme you want in the **wwwroot/css** folder and change the references in *_Layout.cshtml* to point it.</span></span> <span data-ttu-id="b3f7c-230">모든 환경에 대 한 링크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-230">Change the links for all environments:</span></span>

```html
<environment names="Development">
    <link rel="stylesheet" href="~/css/bootstrap.css" />
```

```html
<environment names="Staging,Production">
    <link rel="stylesheet" href="~/css/bootstrap.min.css" />
```

<span data-ttu-id="b3f7c-231">사용자 고유의 대시보드를 빌드 하려는 경우 시작할 수 있습니다 사용 가능한 무료 예제의 여기: [ http://getbootstrap.com/examples/dashboard/ ](http://getbootstrap.com/examples/dashboard/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-231">If you want to build your own dashboard, you can start from the free example available here: [http://getbootstrap.com/examples/dashboard/](http://getbootstrap.com/examples/dashboard/).</span></span>

## <a name="components"></a><span data-ttu-id="b3f7c-232">구성 요소</span><span class="sxs-lookup"><span data-stu-id="b3f7c-232">Components</span></span>

<span data-ttu-id="b3f7c-233">앞에서 설명한 해당 요소 외에도 부트스트랩은 다양 한 지원 [기본 제공 UI 구성 요소](http://getbootstrap.com/components/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-233">In addition to those elements already discussed, Bootstrap includes support for a variety of [built-in UI components](http://getbootstrap.com/components/).</span></span>

### <a name="glyphicons"></a><span data-ttu-id="b3f7c-234">문자</span><span class="sxs-lookup"><span data-stu-id="b3f7c-234">Glyphicons</span></span>

<span data-ttu-id="b3f7c-235">아이콘 집합에서 문자를 포함 하는 부트스트랩 ([http://glyphicons.com](http://glyphicons.com)), 부트스트랩 사용 웹 응용 프로그램 내에서 사용 하 여 무료로 200 개가 넘는 아이콘을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-235">Bootstrap includes icon sets from Glyphicons ([http://glyphicons.com](http://glyphicons.com)), with over 200 icons freely available for use within your Bootstrap-enabled web application.</span></span> <span data-ttu-id="b3f7c-236">다음은 작은 샘플 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-236">Here's just a small sample:</span></span>

![문자](bootstrap/_static/theme-glyphicons.png)

### <a name="input-groups"></a><span data-ttu-id="b3f7c-238">그룹 입력된</span><span class="sxs-lookup"><span data-stu-id="b3f7c-238">Input groups</span></span>

<span data-ttu-id="b3f7c-239">직관적인 환경 사용 하 여 사용자를 제공 하는 추가 텍스트 input 요소를 사용 하 여 단추 등의 묶음 입력된 그룹을 사용:</span><span class="sxs-lookup"><span data-stu-id="b3f7c-239">Input groups allow bundling of additional text or buttons with an input element, providing the user with a more intuitive experience:</span></span>

![그룹 입력된](bootstrap/_static/input-groups.png)

### <a name="breadcrumbs"></a><span data-ttu-id="b3f7c-241">이동 경로</span><span class="sxs-lookup"><span data-stu-id="b3f7c-241">Breadcrumbs</span></span>

<span data-ttu-id="b3f7c-242">이동 경로 최근 기록을 또는 깊이 사이트의 탐색 계층 구조 내에서 해당 사용자를 표시 하는 데 공통 UI 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-242">Breadcrumbs are a common UI component used to show a user their recent history or depth within a site's navigation hierarchy.</span></span> <span data-ttu-id="b3f7c-243">"이동 경로" 클래스에 적용 하 여 쉽게 추가할 `<ol>` 목록 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-243">Add them easily by applying the "breadcrumb" class to any `<ol>` list element.</span></span> <span data-ttu-id="b3f7c-244">"페이지 매김" 클래스를 사용 하 여 페이지 매김에 대 한 기본 제공 지원을 포함을 `<ul>` 내의 요소는 `<nav>`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-244">Include built-in support for pagination by using the "pagination" class on a `<ul>` element within a `<nav>`.</span></span> <span data-ttu-id="b3f7c-245">사용 하 여 응답성이 포함 된 슬라이드 쇼 및 동영상을 추가할 `<iframe>`, `<embed>`, `<video>`, 또는 `<object>` 부트스트랩은 자동으로 스타일을 지정 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-245">Add responsive embedded slideshows and video by using `<iframe>`, `<embed>`, `<video>`, or `<object>` elements, which Bootstrap will style automatically.</span></span> <span data-ttu-id="b3f7c-246">"포함-응답-16by9"와 같은 특정 클래스를 사용 하 여 특정 가로 세로 비율을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-246">Specify a particular aspect ratio by using specific classes like "embed-responsive-16by9".</span></span>

## <a name="javascript-support"></a><span data-ttu-id="b3f7c-247">JavaScript 지원</span><span class="sxs-lookup"><span data-stu-id="b3f7c-247">JavaScript support</span></span>

<span data-ttu-id="b3f7c-248">부트스트랩의 JavaScript 라이브러리에는 응용 프로그램 내에서 프로그래밍 방식으로 해당 동작을 제어할 수 있도록 포함 된 구성 요소에 대 한 API 지원을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-248">Bootstrap's JavaScript library includes API support for the included components, allowing you to control their behavior programmatically within your application.</span></span> <span data-ttu-id="b3f7c-249">또한 *bootstrap.js* 수십 개의 포함 전환, 모달 대화 상자와 같은 추가 기능을 제공 하는 사용자 지정 jQuery 플러그 인 (사용자 문서의 스크롤 위치에 따라 스타일 업데이트)를 감지, 스크롤 축소 동작, 컨베이어 벨트, 및가 화면에 스크롤하여 없습니다 있도록 창에 메뉴를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-249">In addition, *bootstrap.js* includes over a dozen custom jQuery plugins, providing additional features like transitions, modal dialogs, scroll detection (updating styles based on where the user has scrolled in the document), collapse behavior, carousels, and affixing menus to the window so they don't scroll off the screen.</span></span> <span data-ttu-id="b3f7c-250">모든 방문 하십시오 자세히 알아보려면 부트스트랩 – 내장 JavaScript 추가 기능에 맞게 충분 한 공간이 없을 [ http://getbootstrap.com/javascript/ ](http://getbootstrap.com/javascript/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-250">There's not sufficient room to cover all of the JavaScript add-ons built into Bootstrap – to learn more please visit [http://getbootstrap.com/javascript/](http://getbootstrap.com/javascript/).</span></span>

## <a name="summary"></a><span data-ttu-id="b3f7c-251">요약</span><span class="sxs-lookup"><span data-stu-id="b3f7c-251">Summary</span></span>

<span data-ttu-id="b3f7c-252">부트스트랩 신속 하 고 생산적으로 자동 레이아웃 및 다양 한 웹 사이트 및 응용 프로그램 스타일을 사용할 수 있는 웹 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-252">Bootstrap provides a web framework that can be used to quickly and productively lay out and style a wide variety of websites and applications.</span></span> <span data-ttu-id="b3f7c-253">해당 기본 입력 체계 및 스타일에 수동 또는 상업적으로 구입할 수 있는 사용자 지정 테마 지원을 통해 쉽게 조작할 수 있는 편리한 모양 및 느낌을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-253">Its basic typography and styles provide a pleasant look and feel that can easily be manipulated through custom theme support, which can be hand-crafted or purchased commercially.</span></span> <span data-ttu-id="b3f7c-254">과거에는 비용이 많이 드는 타사 컨트롤 열기 및 최신 웹 표준을 지 원하는 하는 동안 수행 하는 필요한 웹 구성 요소 호스트를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3f7c-254">It supports a host of web components that in the past would've required expensive third-party controls to accomplish, while supporting modern and open web standards.</span></span>
