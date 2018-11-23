---
title: ASP.NET Core와 Less, Sass 및 Font Awesome
author: ardalis
description: ASP.NET Core 응용 프로그램에서 Less, Sass 및 Font Awesome을 사용하는 방법을 알아봅니다.
ms.author: tdykstra
ms.date: 10/14/2016
uid: client-side/less-sass-fa
ms.openlocfilehash: 2229c4e3b0238ff17c15e78f657b9acb10495c72
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275567"
---
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a><span data-ttu-id="dbd1f-103">ASP.NET Core와 Less, Sass 및 Font Awesome</span><span class="sxs-lookup"><span data-stu-id="dbd1f-103">Less, Sass, and Font Awesome in ASP.NET Core</span></span>

<span data-ttu-id="dbd1f-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="dbd1f-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="dbd1f-105">웹 응용 프로그램의 사용자는 스타일과 전반적인 경험에 대해 갈수록 더 많은 기대를 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-105">Users of web applications have increasingly high expectations when it comes to style and overall experience.</span></span> <span data-ttu-id="dbd1f-106">최신 웹 응용 프로그램은 모양 및 느낌을 일관적인 방식으로 정의하고 관리하기 위해 풍부한 도구와 프레임워크를 자주 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-106">Modern web applications frequently leverage rich tools and frameworks for defining and managing their look and feel in a consistent manner.</span></span> <span data-ttu-id="dbd1f-107">[부트스트랩](http://getbootstrap.com/) 같은 프레임워크는 웹 사이트에 대한 공통 스타일 모음과 레이아웃 옵션을 정의하는데 매우 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-107">Frameworks like [Bootstrap](http://getbootstrap.com/) can go a long way toward defining a common set of styles and layout options for web sites.</span></span> <span data-ttu-id="dbd1f-108">그러나 대부분의 중요한 사이트들은 스타일과 CSS 스타일시트 파일을 효과적으로 정의하고 관리할 수 있다는 점과 함께 사이트의 인터페이스를 보다 직관적으로 만들어주는 비이미지 아이콘에 쉽게 접근할 수 있는 장점도 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-108">However, most non-trivial sites also benefit from being able to effectively define and maintain styles and cascading style sheet (CSS) files, as well as having easy access to non-image icons that help make the site's interface more intuitive.</span></span> <span data-ttu-id="dbd1f-109">바로 이 점이 [Less](http://lesscss.org/) 및 [Sass](http://sass-lang.com/)를 지원하는 언어와 도구, 그리고 [Font Awesome](http://fontawesome.io/) 같은 라이브러리가 필요한 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-109">That's where languages and tools that support [Less](http://lesscss.org/) and [Sass](http://sass-lang.com/), and libraries like [Font Awesome](http://fontawesome.io/), come in.</span></span>

## <a name="css-preprocessor-languages"></a><span data-ttu-id="dbd1f-110">CSS 전처리기 언어</span><span class="sxs-lookup"><span data-stu-id="dbd1f-110">CSS preprocessor languages</span></span>

<span data-ttu-id="dbd1f-111">기본 언어의 작업 경험을 개선하기 위해서 다른 언어로 컴파일되는 언어를 전처리기라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-111">Languages that are compiled into other languages, in order to improve the experience of working with the underlying language, are referred to as preprocessors.</span></span> <span data-ttu-id="dbd1f-112">CSS에는 Less와 Sass라는 두 가지 인기 있는 전처리기가 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-112">There are two popular preprocessors for CSS: Less and Sass.</span></span>  <span data-ttu-id="dbd1f-113">이 전처리기들은 CSS에 변수 및 중첩된 규칙 같은 기능을 추가하여 크고 복잡한 스타일시트의 유지 관리를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-113">These preprocessors add features to CSS, such as support for variables and nested rules, which improve the maintainability of large, complex stylesheets.</span></span> <span data-ttu-id="dbd1f-114">언어로서의 CSS는 매우 단순하기 때문에 변수처럼 간단한 기능조차 지원이 부족하며 이는 CSS 파일을 반복적이고 비대하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-114">CSS as a language is very basic, lacking support even for something as simple as variables, and this tends to make CSS files repetitive and bloated.</span></span> <span data-ttu-id="dbd1f-115">전처리기를 통해서 실제 프로그래밍 언어의 기능을 추가하면 중복을 줄이고 스타일 규칙을 보다 효과적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-115">Adding real programming language features via preprocessors can help reduce duplication and provide better organization of styling rules.</span></span> <span data-ttu-id="dbd1f-116">Visual Studio는 Less 및 Sass 둘 모두에 대한 기본 제공을 비롯해서 이런 언어로 작업할 때 개발 환경을 더욱 개선할 수 있는 확장을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-116">Visual Studio provides built-in support for both Less and Sass, as well as extensions that can further improve the development experience when working with these languages.</span></span>

<span data-ttu-id="dbd1f-117">전처리기가 스타일 정보의 가독성과 유지 관리를 향상시키는 방법에 대한 간단한 예제로 다음 CSS를 살펴보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-117">As a quick example of how preprocessors can improve readability and maintainability of style information, consider this CSS:</span></span>

```css
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    color: black;
    font-weight: bold;
    font-size: 14px;
    font-family: Helvetica, Arial, sans-serif;
}
```

<span data-ttu-id="dbd1f-118">Less를 사용하면 *믹스인*(속성을 한 클래스나 규칙 집합에서 다른 클래스나 규칙 집합에 '섞을' 수 있기 때문에 이런 이름이 붙여짐)을 사용해서 모든 중복을 제거하도록 이를 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-118">Using Less, this can be rewritten to eliminate all of the duplication, using a *mixin* (so named because it allows you to "mix in" properties from one class or rule-set into another):</span></span>

```less
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    .header;
    font-size: 14px;
}
```

## <a name="less"></a><span data-ttu-id="dbd1f-119">Less</span><span class="sxs-lookup"><span data-stu-id="dbd1f-119">Less</span></span>

<span data-ttu-id="dbd1f-120">Less CSS 전처리기는 Node.js를 통해서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-120">The Less CSS preprocessor runs using Node.js.</span></span> <span data-ttu-id="dbd1f-121">Less를 설치하려면 명령 프롬프트에서 노드 패키지 관리자(npm)를 사용합니다 (-g는 '전역'을 의미합니다).</span><span class="sxs-lookup"><span data-stu-id="dbd1f-121">To install Less, use Node Package Manager (npm) from a command prompt (-g means "global"):</span></span>

```console
npm install -g less
```

<span data-ttu-id="dbd1f-122">Visual Studio를 사용하는 경우, 프로젝트에 하나 이상의 Less 파일을 추가한 다음, 컴파일 시에 이를 처리하도록 Gulp를 (또는 Grunt를) 구성하여 Less를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-122">If you're using Visual Studio, you can get started with Less by adding one or more Less files to your project, and then configuring Gulp (or Grunt) to process them at compile-time.</span></span> <span data-ttu-id="dbd1f-123">프로젝트에 *Styles* 폴더를 추가한 다음, 이 폴더에 *main.less*라는 이름으로 새로운 Less 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-123">Add a *Styles* folder to your project, and then add a new Less file named *main.less* to this folder.</span></span>

![Less 파일 추가하기](less-sass-fa/_static/add-less-file.png)

<span data-ttu-id="dbd1f-125">파일이 추가된 폴더의 구조는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-125">Once added, your folder structure should look something like this:</span></span>

![폴더 구조](less-sass-fa/_static/folder-structure.png)

<span data-ttu-id="dbd1f-127">이제 이 파일에 몇 가지 기본 스타일을 추가할 수 있으며, 이는 Gulp에 의해 CSS로 컴파일되어 wwwroot 폴더에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-127">Now you can add some basic styling to the file, which will be compiled into CSS and deployed to the wwwroot folder by Gulp.</span></span>

<span data-ttu-id="dbd1f-128">다음 내용을 포함하도록 *main.less*를 수정해서 단일 기본 색상으로부터 간단한 색상표를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-128">Modify *main.less* to include the following content, which creates a simple color palette from a single base color.</span></span>

```less
@base: #663333;
@background: spin(@base, 180);
@lighter: lighten(spin(@base, 5), 10%);
@lighter2: lighten(spin(@base, 10), 20%);
@darker: darken(spin(@base, -5), 10%);
@darker2: darken(spin(@base, -10), 20%);

body {
    background-color:@background;
}
.baseColor  {color:@base}
.bgLight    {color:@lighter}
.bgLight2   {color:@lighter2}
.bgDark     {color:@darker}
.bgDark2    {color:@darker2}
```

<span data-ttu-id="dbd1f-129">`@base` 다른 @-prefixed 항목은 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-129">`@base` and the other @-prefixed items are variables.</span></span> <span data-ttu-id="dbd1f-130">각각의 색을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-130">Each of them represents a color.</span></span> <span data-ttu-id="dbd1f-131">제외 하 고 `@base`, 색 함수를 사용 하 여 설정 하는 것: 밝게, 어둡게, 및 회전 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-131">Except for `@base`, they're set using color functions: lighten, darken, and spin.</span></span> <span data-ttu-id="dbd1f-132">밝게 및 어둡게 거의 예상 대로; 수행 스핀 (색상표) 중심으로 다양 한 색의 색상을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-132">Lighten and darken do pretty much what you would expect; spin adjusts the hue of a color by a number of degrees (around the color wheel).</span></span> <span data-ttu-id="dbd1f-133">작은 프로세서는 때문에 이러한 변수 작동 하는 방법을 설명 하기 위해 어딘가에 사용법이 사용 되지 않는 변수를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-133">The Less processor is smart enough to ignore variables that aren't used, so to demonstrate how these variables work, we need to use them somewhere.</span></span> <span data-ttu-id="dbd1f-134">클래스 `.baseColor`, 등에서는 변수가 생성 되는 CSS 파일에 각각의 계산된 된 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-134">The classes `.baseColor`, etc. will demonstrate the calculated values of each of the variables in the CSS file that's produced.</span></span>

### <a name="get-started"></a><span data-ttu-id="dbd1f-135">시작하기</span><span class="sxs-lookup"><span data-stu-id="dbd1f-135">Get started</span></span>

<span data-ttu-id="dbd1f-136">프로젝트 폴더에 **npm 구성 파일**(*package.json*)을 만들고 이 파일이 `gulp` 및 `gulp-less`를 참조하도록 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-136">Create an **npm Configuration File** (*package.json*) in your project folder and edit it to reference `gulp` and `gulp-less`:</span></span>

```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "3.9.1",
    "gulp-less": "3.3.0"
  }
}
```

<span data-ttu-id="dbd1f-137">프로젝트 폴더에서 나 Visual Studio 명령 프롬프트에서 종속성을 설치 **솔루션 탐색기** (**종속성 > npm > 패키지를 복원**).</span><span class="sxs-lookup"><span data-stu-id="dbd1f-137">Install the dependencies either at a command prompt in your project folder, or in Visual Studio **Solution Explorer** (**Dependencies > npm > Restore packages**).</span></span>

```console
npm install
```

![VS 패키지 복원](less-sass-fa/_static/restore-packages.png)

<span data-ttu-id="dbd1f-139">프로젝트 폴더에 **Gulp 구성 파일**(*gulpfile.js*)을 만들고 자동화된 프로세스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-139">In the project folder, create a **Gulp Configuration File** (*gulpfile.js*) to define the automated process.</span></span>  <span data-ttu-id="dbd1f-140">파일의 맨 위에 Less를 나타내는 변수를 추가하고 Less를 실행하기 위한 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-140">Add a variable at the top of the file to represent Less, and a task to run Less:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less");

gulp.task("less", function () {
  return gulp.src('Styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="dbd1f-141">열기는 **작업 Runner 탐색기** (**보기 > 다른 Windows > 작업 Runner 탐색기**).</span><span class="sxs-lookup"><span data-stu-id="dbd1f-141">Open the **Task Runner Explorer** (**View > Other Windows > Task Runner Explorer**).</span></span> <span data-ttu-id="dbd1f-142">작업 간에 라는 새 작업을 표시 되어야 `less`합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-142">Among the tasks, you should see a new task named `less`.</span></span> <span data-ttu-id="dbd1f-143">창을 새로 고쳐야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-143">You might have to refresh the window.</span></span>

<span data-ttu-id="dbd1f-144">`less` 작업을 실행하면 다음과 비슷한 출력이 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-144">Run the `less` task, and you see output similar to what is shown here:</span></span>

![less 작업 러너](less-sass-fa/_static/less-task-runner.png)

<span data-ttu-id="dbd1f-146">이제 *wwwroot/css* 폴더에 *main.css*라는 새 파일이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-146">The *wwwroot/css* folder now contains a new file, *main.css*:</span></span>

![생성된 main css](less-sass-fa/_static/main-css-created.png)

<span data-ttu-id="dbd1f-148">*main.css*를 열어보면 다음과 같은 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-148">Open *main.css* and you see something like the following:</span></span>

```css
body {
    background-color: #336666;
}
.baseColor {
    color: #663333;
}
.bgLight {
    color: #884a44;
}
.bgLight2 {
    color: #aa6355;
}
.bgDark {
    color: #442225;
}
.bgDark2 {
    color: #221114;
}
```

<span data-ttu-id="dbd1f-149">간단한 HTML 페이지를 *wwwroot* 폴더에 추가하고 *main.css*를 참조하여 실제 색상표를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-149">Add a simple HTML page to the *wwwroot* folder, and reference *main.css* to see the color palette in action.</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="css/main.css" rel="stylesheet" />
    <title></title>
</head>
<body>
    <div>
        <div class="baseColor">BaseColor</div>
        <div class="bgLight">Light</div>
        <div class="bgLight2">Light2</div>
        <div class="bgDark">Dark</div>
        <div class="bgDark2">Dark2</div>
    </div>
</body>
</html>
```

<span data-ttu-id="dbd1f-150">`@base`를 180도 회전하여 `@background`를 생성한 결과로 색상환에서 `@base`의 반대색이 만들어진 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-150">You can see that the 180 degree spin on `@base` used to produce `@background` resulted in the color wheel opposing color of `@base`:</span></span>

![Less 테스트 예제](less-sass-fa/_static/less-test-screenshot.png)

<span data-ttu-id="dbd1f-152">Less는 중첩된 미디어 쿼리뿐만 아니라 중첩된 규칙에 대한 지원도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-152">Less also provides support for nested rules, as well as nested media queries.</span></span> <span data-ttu-id="dbd1f-153">예를 들어 메뉴 같은 중첩된 계층 구조를 정의하다 보면 다음과 같이 장황한 CSS 규칙이 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-153">For example, defining nested hierarchies like menus can result in verbose CSS rules like these:</span></span>

```css
nav {
    height: 40px;
    width: 100%;
}
nav li {
    height: 38px;
    width: 100px;
}
nav li a:link {
    color: #000;
    text-decoration: none;
}
nav li a:visited {
    text-decoration: none;
    color: #CC3333;
}
nav li a:hover {
    text-decoration: underline;
    font-weight: bold;
}
nav li a:active {
    text-decoration: underline;
}
```

<span data-ttu-id="dbd1f-154">이상적으로 관련된 모든 스타일 규칙이 CSS 파일 내에 함께 존재하지만, 실제로 규약을 제외하고는 이 규칙을 강제하는 것은 아무 것도 없으며 아마도 주석을 작성할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-154">Ideally all of the related style rules will be placed together within the CSS file, but in practice there's nothing enforcing this rule except convention and perhaps block comments.</span></span>

<span data-ttu-id="dbd1f-155">Less를 사용하여 동일한 규칙을 정의하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-155">Defining these same rules using Less looks like this:</span></span>

```less
nav {
    height: 40px;
    width: 100%;
    li {
        height: 38px;
        width: 100px;
        a {
            color: #000;
            &:link { text-decoration:none}
            &:visited { color: #CC3333; text-decoration:none}
            &:hover { text-decoration:underline; font-weight:bold}
            &:active {text-decoration:underline}
        }
    }
}
```

<span data-ttu-id="dbd1f-156">이 경우 `nav`의 모든 하위 요소가 해당 범위에 포함된다는 점에 유의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-156">Note that in this case, all of the subordinate elements of `nav` are contained within its scope.</span></span> <span data-ttu-id="dbd1f-157">더 이상 부모 요소(`nav`, `li`, `a`)들이 반복되지 않으며, 전체 줄 수도 감소했습니다(그 중 일부는 두 번째 예제에서 동일한 줄에 값을 넣은 결과이기도 합니다).</span><span class="sxs-lookup"><span data-stu-id="dbd1f-157">There's no longer any repetition of parent elements (`nav`, `li`, `a`), and the total line count has dropped as well (though some of that's a result of putting values on the same lines in the second example).</span></span> <span data-ttu-id="dbd1f-158">명시적으로 지정된 범위내에서 해당 UI 요소에 대한 모든 규칙을 살펴보는 것이 조직적으로 매우 유용할 수 있으며, 이 경우 파일의 나머지 부분에서 중괄호를 사용하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-158">It can be very helpful, organizationally, to see all of the rules for a given UI element within an explicitly bounded scope, in this case set off from the rest of the file by curly braces.</span></span>

<span data-ttu-id="dbd1f-159">`&` 구문은 Less의 선택자 기능으로, &amp;를 지정하면 현재 선택자의 부모를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-159">The `&` syntax is a Less selector feature, with & representing the current selector parent.</span></span> <span data-ttu-id="dbd1f-160">따라서 {...}</span><span class="sxs-lookup"><span data-stu-id="dbd1f-160">So, within the a {...}</span></span> <span data-ttu-id="dbd1f-161">블록 내에서 `&`는 `a` 태그를 나타내므로 `&:link`는 `a:link`와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-161">block, `&` represents an `a` tag, and thus `&:link` is equivalent to `a:link`.</span></span>

<span data-ttu-id="dbd1f-162">반응형 디자인을 만드는데 매우 유용한 미디어 쿼리는 CSS의 반복과 복잡성의 큰 원인이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-162">Media queries, extremely useful in creating responsive designs, can also contribute heavily to repetition and complexity in CSS.</span></span> <span data-ttu-id="dbd1f-163">Less를 사용하면 클래스 내 미디어 쿼리를 중첩시킬 수 있으므로, 전체 클래스 정의를 다른 최상위 `@media` 요소 내에서 반복할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-163">Less allows media queries to be nested within classes, so that the entire class definition doesn't need to be repeated within different top-level `@media` elements.</span></span> <span data-ttu-id="dbd1f-164">예를 들어 반응형 메뉴의 CSS는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-164">For example, here is CSS for a responsive menu:</span></span>

```css
.navigation {
    margin-top: 30%;
    width: 100%;
}
@media screen and (min-width: 40em) {
    .navigation {
        margin: 0;
    }
}
@media screen and (min-width: 62em) {
    .navigation {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="dbd1f-165">이를 Less로 다음과 같이 더 잘 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-165">This can be better defined in Less as:</span></span>

```less
.navigation {
    margin-top: 30%;
    width: 100%;
    @media screen and (min-width: 40em) {
        margin: 0;
    }
    @media screen and (min-width: 62em) {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="dbd1f-166">이미 살펴본 Less의 또 다른 기능은 미리 정의된 변수로 스타일의 속성을 구성할 수 있는 수학적 연산에 대한 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-166">Another feature of Less that we have already seen is its support for mathematical operations, allowing style attributes to be constructed from pre-defined variables.</span></span> <span data-ttu-id="dbd1f-167">이 기능을 사용하면 기본 변수만 수정해도 모든 종속 값들이 자동으로 변경되므로 관련된 스타일을 훨씬 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-167">This makes updating related styles much easier, since the base variable can be modified and all dependent values change automatically.</span></span>

<span data-ttu-id="dbd1f-168">CSS 파일은 특히 대규모 사이트의 경우 (그리고 특히 미디어 쿼리가 사용되는 경우) 시간이 지남에 따라 상당히 커지는 경향이 있어서 작업하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-168">CSS files, especially for large sites (and especially if media queries are being used), tend to get quite large over time, making working with them unwieldy.</span></span> <span data-ttu-id="dbd1f-169">Less 파일을 별도로 정의한 다음 `@import` 지시문을 사용하여 함께 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-169">Less files can be defined separately, then pulled together using `@import` directives.</span></span> <span data-ttu-id="dbd1f-170">필요한 경우 Less는 개별 CSS 파일을 가져오기 위해서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-170">Less can also be used to import individual CSS files, as well, if desired.</span></span>

<span data-ttu-id="dbd1f-171">*믹스인*은 매개 변수를 전달받을 수 있으며, Less는 특정 믹스인이 언제 효력이 발생하는지를 정의하기 위한 선언적 방법을 제공하는 믹스인 가드의 형태로 조건부 논리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-171">*Mixins* can accept parameters, and Less supports conditional logic in the form of mixin guards, which provide a declarative way to define when certain mixins take effect.</span></span> <span data-ttu-id="dbd1f-172">믹스인 가드의 일반적인 용도는 원본 색이 얼마나 밝거나 어두운지에 따라 색을 조정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-172">A common use for mixin guards is to adjust colors based on how light or dark the source color is.</span></span> <span data-ttu-id="dbd1f-173">색에 대한 매개 변수를 전달받는 믹스인이 주어지면 믹스인 가드를 사용하여 해당 색을 기반으로 믹스인을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-173">Given a mixin that accepts a parameter for color, a mixin guard can be used to modify the mixin based on that color:</span></span>

```less
.box (@color) when (lightness(@color) >= 50%) {
    background-color: #000;
}
.box (@color) when (lightness(@color) < 50%) {
    background-color: #FFF;
}
.box (@color) {
    color: @color;
}

.feature {
    .box (@base);
}
```

<span data-ttu-id="dbd1f-174">현재 `@base` 값인 `#663333`을 고려해 볼 때, 이 Less 스크립트는 다음과 같은 CSS를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-174">Given our current `@base` value of `#663333`, this Less script will produce the following CSS:</span></span>

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

<span data-ttu-id="dbd1f-175">Less는 다양한 추가적인 기능들을 제공하며, 지금까지 살펴본 예제들은 이 전처리기 언어를 향상하기 위해 일부 아이디어를 제공할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-175">Less provides a number of additional features, but this should give you some idea of the power of this preprocessing language.</span></span>

## <a name="sass"></a><span data-ttu-id="dbd1f-176">Sass</span><span class="sxs-lookup"><span data-stu-id="dbd1f-176">Sass</span></span>

<span data-ttu-id="dbd1f-177">Sass는 Less와 비슷하며 많은 동일한 기능을 지원하지만 구문이 조금 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-177">Sass is similar to Less, providing support for many of the same features, but with slightly different syntax.</span></span> <span data-ttu-id="dbd1f-178">JavaScript 대신 Ruby를 사용해서 만들어졌기 때문에 설치 요구 사항이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-178">It's built using Ruby, rather than JavaScript, and so has different setup requirements.</span></span> <span data-ttu-id="dbd1f-179">원래의 Sass 언어는 중괄호 또는 세미콜론을 사용하지 않으며, 대신 공백 및 들여쓰기를 사용해서 범위를 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-179">The original Sass language didn't use curly braces or semicolons, but instead defined scope using white space and indentation.</span></span> <span data-ttu-id="dbd1f-180">Sass 버전 3에서는 새로운 구문인 **SCSS**("Sassy CSS")가 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-180">In version 3 of Sass, a new syntax was introduced, **SCSS** ("Sassy CSS").</span></span> <span data-ttu-id="dbd1f-181">SCSS는 들여쓰기 수준과 공백을 무시하고 대신 세미콜론과 중괄호를 사용한다는 점에서 CSS와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-181">SCSS is similar to CSS in that it ignores indentation levels and whitespace, and instead uses semicolons and curly braces.</span></span>

<span data-ttu-id="dbd1f-182">일반적으로 Sass를 설치하려면 먼저 Ruby를 설치한 다음(MacOS에는 사전 설치되어 있음), 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-182">To install Sass, typically you would first install Ruby (pre-installed on macOS), and then run:</span></span>

```console
gem install sass
```

<span data-ttu-id="dbd1f-183">그러나 Visual Studio를 실행하고 있다면 Less와 거의 동일한 방식으로 Sass를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-183">However, if you're running Visual Studio, you can get started with Sass in much the same way as you would with Less.</span></span> <span data-ttu-id="dbd1f-184">*package.json*을 열고 "gulp-sass" 패키지를 `devDependencies`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-184">Open *package.json* and add the "gulp-sass" package to `devDependencies`:</span></span>

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

<span data-ttu-id="dbd1f-185">다음으로 *gulpfile.js*를 수정하여 sass 변수와 작업을 추가해서 Sass 파일을 컴파일하고 결과를 wwwroot 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-185">Next, modify *gulpfile.js* to add a sass variable and a task to compile your Sass files and place the results in the wwwroot folder:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less"),
  sass = require("gulp-sass");

// other content removed

gulp.task("sass", function () {
  return gulp.src('Styles/main2.scss')
    .pipe(sass())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="dbd1f-186">이제 *main2.scss*라는 Sass 파일을 프로젝트 루트의 *Styles* 폴더에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-186">Now you can add the Sass file *main2.scss* to the *Styles* folder in the root of the project:</span></span>

![scss 파일 추가하기](less-sass-fa/_static/add-scss-file.png)

<span data-ttu-id="dbd1f-188">*main2.scss*를 열고 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-188">Open *main2.scss* and add the following:</span></span>

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

<span data-ttu-id="dbd1f-189">모든 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-189">Save all of your files.</span></span> <span data-ttu-id="dbd1f-190">이제를 새로 고칠 때 **Task Runner 탐색기**, 표시는 `sass` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-190">Now when you refresh **Task Runner Explorer**, you see a `sass` task.</span></span> <span data-ttu-id="dbd1f-191">찾는 위치 하 고 실행 된 */wwwroot/css* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-191">Run it, and look in the */wwwroot/css* folder.</span></span> <span data-ttu-id="dbd1f-192">이제는 *main2.css* 이러한 내용 인 파일에:</span><span class="sxs-lookup"><span data-stu-id="dbd1f-192">There's now a *main2.css* file, with these contents:</span></span>

```css
body {
    background-color: #CC0000;
}
```

<span data-ttu-id="dbd1f-193">Sass는 Less를 사용할 때와 비슷한 방식으로 중첩을 지원하므로 유사한 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-193">Sass supports nesting in much the same was that Less does, providing similar benefits.</span></span> <span data-ttu-id="dbd1f-194">파일은 함수로 나눌 수 있으며 `@import` 지시문을 사용해서 포함시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-194">Files can be split up by function and included using the `@import` directive:</span></span>

```sass
@import 'anotherfile';
```

<span data-ttu-id="dbd1f-195">Sass는 믹스인도 지원하며, 다음 [sass-lang.com](http://sass-lang.com)의 예제처럼 `@mixin` 키워드를 사용하여 정의하고 `@include`를 사용하여 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-195">Sass supports mixins as well, using the `@mixin` keyword to define them and `@include` to include them, as in this example from [sass-lang.com](http://sass-lang.com):</span></span>

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

<span data-ttu-id="dbd1f-196">믹스인 외에도 Sass는 상속의 개념을 지원하므로 한 클래스가 다른 클래스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-196">In addition to mixins, Sass also supports the concept of inheritance, allowing one class to extend another.</span></span> <span data-ttu-id="dbd1f-197">개념적으로는 믹스인과 비슷하지만 CSS 코드가 적습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-197">It's conceptually similar to a mixin, but results in less CSS code.</span></span> <span data-ttu-id="dbd1f-198">이 기능은 `@extend` 키워드를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-198">It's accomplished using the `@extend` keyword.</span></span> <span data-ttu-id="dbd1f-199">믹스인을 시험해보려면 *main2.scss* 파일에 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-199">To try out mixins, add the following to your *main2.scss* file:</span></span>

```sass
@mixin alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @include alert;
    border-color: green;
}

.error {
    @include alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="dbd1f-200">**작업 러너 탐색기**에서 `sass` 작업을 실행한 다음, *main2.css*의 출력을 확인해봅니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-200">Examine the output in *main2.css* after running the `sass` task in **Task Runner Explorer**:</span></span>

```css
.success {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    border-color: green;
 }

.error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="dbd1f-201">경고 믹스인의 모든 공통 속성들이 각 클래스에서 반복된다는 점에 유의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-201">Notice that all of the common properties of the alert mixin are repeated in each class.</span></span> <span data-ttu-id="dbd1f-202">믹스인은 개발 시 중복 제거에 많은 도움을 주지만 여전히 많은 중복이 존재하는 CSS를 생성하여 필요한 CSS 파일보다 큰, 잠재적 성능 문제를 갖고 있는 파일이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-202">The mixin did a good job of helping eliminate duplication at development time, but it's still creating CSS with a lot of duplication in it, resulting in larger than necessary CSS files - a potential performance issue.</span></span>

<span data-ttu-id="dbd1f-203">이제 alert 믹스인을 `.alert` 클래스로 대체하고 `@include`를 `@extend`로 변경합니다(`alert`이 아니라 `.alert`을 확장해야 한다는 점이 중요).</span><span class="sxs-lookup"><span data-stu-id="dbd1f-203">Now replace the alert mixin with a `.alert` class, and change `@include` to `@extend` (remembering to extend `.alert`, not `alert`):</span></span>

```sass
.alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @extend .alert;
    border-color: green;
}

.error {
    @extend .alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="dbd1f-204">Sass를 다시 실행하고 결과 CSS를 확인해봅니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-204">Run Sass once more, and examine the resulting CSS:</span></span>

```css
.alert, .success, .error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    border-color: green;
}

.error {
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="dbd1f-205">이제 필요한 횟수만큼만 속성이 정의되며 더 나은 CSS가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-205">Now the properties are defined only as many times as needed, and better CSS is generated.</span></span>

<span data-ttu-id="dbd1f-206">Sass는 Less와 유사한 함수 및 조건부 논리 연산도 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-206">Sass also includes functions and conditional logic operations, similar to Less.</span></span> <span data-ttu-id="dbd1f-207">사실 두 언어의 기능은 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-207">In fact, the two languages' capabilities are very similar.</span></span>

## <a name="less-or-sass"></a><span data-ttu-id="dbd1f-208">Less 또는 Sass?</span><span class="sxs-lookup"><span data-stu-id="dbd1f-208">Less or Sass?</span></span>

<span data-ttu-id="dbd1f-209">Less나 Sass를 사용하는 것이 일반적으로 더 나은지 여부에 대해서는 (또는 Sass 내에서 원래의 Sass 또는 최신 SCSS 구문을 선호할지 여부에 대해서도) 여전히 일치된 의견이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-209">There's still no consensus as to whether it's generally better to use Less or Sass (or even whether to prefer the original Sass or the newer SCSS syntax within Sass).</span></span> <span data-ttu-id="dbd1f-210">아마도 가장 중요한 결정은 CSS 파일을 손으로 코딩하는 대신 **이런 도구 중 하나를 사용하는 것**입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-210">Probably the most important decision is to **use one of these tools**, as opposed to just hand-coding your CSS files.</span></span> <span data-ttu-id="dbd1f-211">일단 결정을 하고 나면 Less와 Sass 모두 좋은 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-211">Once you've made that decision, both Less and Sass are good choices.</span></span>

## <a name="font-awesome"></a><span data-ttu-id="dbd1f-212">Font Awesome</span><span class="sxs-lookup"><span data-stu-id="dbd1f-212">Font Awesome</span></span>

<span data-ttu-id="dbd1f-213">CSS 전처리기와 더불어 최신 웹 응용 프로그램의 스타일 지정에 유용한 또 다른 리소스는 Font Awesome입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-213">In addition to CSS preprocessors, another great resource for styling modern web applications is Font Awesome.</span></span> <span data-ttu-id="dbd1f-214">Font Awesome은 웹 응용 프로그램에서 자유롭게 사용할 수 있는 500개 이상의 확대 및 축소 가능한 벡터 아이콘을 제공하는 도구 키트입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-214">Font Awesome is a toolkit that provides over 500 scalable vector icons that can be freely used in your web applications.</span></span> <span data-ttu-id="dbd1f-215">본래 부트스트랩과 함께 사용하도록 설계되었지만 해당 프레임워크나 어떠한 JavaScript 라이브러리에도 종속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-215">It was originally designed to work with Bootstrap, but it has no dependency on that framework or on any JavaScript libraries.</span></span>

<span data-ttu-id="dbd1f-216">Font Awesome을 시작하는 가장 쉬운 방법은 공용 콘텐츠 배달 네트워크(CDN) 위치를 사용하여 Font Awesome에 대한 참조를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-216">The easiest way to get started with Font Awesome is to add a reference to it, using its public content delivery network (CDN) location:</span></span>

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

<span data-ttu-id="dbd1f-217">또는 *bower.json*의 "dependencies"에 이를 추가해서 Visual Studio 프로젝트에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-217">You can also add it to your Visual Studio project by adding it to the "dependencies" in *bower.json*:</span></span>

```json
{
  "name": "ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap": "3.0.0",
    "jquery": "1.10.2",
    "jquery-validation": "1.11.1",
    "jquery-validation-unobtrusive": "3.2.2",
    "hammer.js": "2.0.4",
    "bootstrap-touch-carousel": "0.8.0",
    "Font-Awesome": "4.3.0"
  }
}
```

<span data-ttu-id="dbd1f-218">페이지에 Font Awesome에 대한 참조를 추가하고 나면 일반적으로 접두사가 'fa-'인 Font Awesome 클래스를 인라인 HTML 요소(예: `<span>` 또는 `<i>`)dp 적용하여 응용 프로그램에 아이콘을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-218">Once you have a reference to Font Awesome on a page, you can add icons to your application by applying Font Awesome classes, typically prefixed with "fa-", to your inline HTML elements (such as `<span>` or `<i>`).</span></span>  <span data-ttu-id="dbd1f-219">예를 들어, 다음과 같은 코드를 사용하여 간단한 목록 및 메뉴에 아이콘을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-219">For example, you can add icons to simple lists and menus using code like this:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <link href="lib/font-awesome/css/font-awesome.css" rel="stylesheet" />
</head>
<body>
    <ul class="fa-ul">
        <li><i class="fa fa-li fa-home"></i> Home</li>
        <li><i class="fa fa-li fa-cog"></i> Settings</li>
    </ul>
</body>
</html>
```

<span data-ttu-id="dbd1f-220">이렇게 하면 브라우저에서 다음이 생성-각 항목 옆의 아이콘에 유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-220">This produces the following in the browser - note the icon beside each item:</span></span>

![목록 아이콘](less-sass-fa/_static/list-icons-screenshot.png)

<span data-ttu-id="dbd1f-222">다음에서 사용 가능한 아이콘의 전체 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-222">You can view a complete list of the available icons here:</span></span>

http://fontawesome.io/icons/

## <a name="summary"></a><span data-ttu-id="dbd1f-223">요약</span><span class="sxs-lookup"><span data-stu-id="dbd1f-223">Summary</span></span>

<span data-ttu-id="dbd1f-224">최신 웹 응용 프로그램은 다양한 장치에서 점점 더 깔끔하고 직관적이며 사용하기 쉬운 반응형의 유연한 디자인을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-224">Modern web applications increasingly demand responsive, fluid designs that are clean, intuitive, and easy to use from a variety of devices.</span></span> <span data-ttu-id="dbd1f-225">이런 목표를 달성하기 위해 필요한 CSS 스타일시트의 복잡성 관리는 Less 또는 Sass 같은 전처리기를 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-225">Managing the complexity of the CSS stylesheets required to achieve these goals is best done using a preprocessor like Less or Sass.</span></span> <span data-ttu-id="dbd1f-226">또한 Font Awesome 같은 도구 키트는 텍스트 기반의 탐색 메뉴 및 버튼에 친숙한 아이콘을 신속하게 제공하여 응용 프로그램의 전반적인 사용자 경험을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="dbd1f-226">In addition, toolkits like Font Awesome quickly provide well-known icons to textual navigation menus and buttons, improving the overall user experience of your application.</span></span>
