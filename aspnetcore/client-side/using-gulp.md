---
title: ASP.NET Core에서 Gulp 사용하기
author: rick-anderson
description: ASP.NET Core에서 Gulp를 사용하는 방법을 알아봅니다.
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 10/04/2018
uid: client-side/using-gulp
ms.openlocfilehash: e280eabecbd427f3e1418b3d7a60e0ea3df46a5a
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450608"
---
# <a name="use-gulp-in-aspnet-core"></a><span data-ttu-id="a94e3-103">ASP.NET Core에서 Gulp 사용하기</span><span class="sxs-lookup"><span data-stu-id="a94e3-103">Use Gulp in ASP.NET Core</span></span>

<span data-ttu-id="a94e3-104">작성자: [Scott Addie](https://scottaddie.com), [Shayne Boyer](https://twitter.com/spboyer), 및 [David Pine](https://twitter.com/davidpine7)</span><span class="sxs-lookup"><span data-stu-id="a94e3-104">By [Scott Addie](https://scottaddie.com), [Shayne Boyer](https://twitter.com/spboyer), and [David Pine](https://twitter.com/davidpine7)</span></span>

<span data-ttu-id="a94e3-105">일반적인 최신 웹 앱에서 빌드 프로세스는 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-105">In a typical modern web app, the build process might:</span></span>

* <span data-ttu-id="a94e3-106">JavaScript 및 CSS 파일을 번들링하고 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-106">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="a94e3-107">매번 빌드하기 전에 번들링 및 축소 작업을 호출하는 도구를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-107">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="a94e3-108">LESS 또는 SASS 파일을 CSS로 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-108">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="a94e3-109">CoffeeScript 또는 TypeScript 파일을 JavaScript로 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-109">Compile CoffeeScript or TypeScript files to JavaScript.</span></span>

<span data-ttu-id="a94e3-110">A *작업 실행 기* 이러한 일상적인 개발 작업 등을 자동화 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-110">A *task runner* is a tool which automates these routine development tasks and more.</span></span> <span data-ttu-id="a94e3-111">Visual Studio는 두 가지 인기 있는 JavaScript 기반 작업 실행 기에 대 한 기본 제공 지원을 제공 합니다. [Gulp](https://gulpjs.com/) 하 고 [Grunt](using-grunt.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-111">Visual Studio provides built-in support for two popular JavaScript-based task runners: [Gulp](https://gulpjs.com/) and [Grunt](using-grunt.md).</span></span>

## <a name="gulp"></a><span data-ttu-id="a94e3-112">Gulp</span><span class="sxs-lookup"><span data-stu-id="a94e3-112">Gulp</span></span>

<span data-ttu-id="a94e3-113">Gulp는 JavaScript 기반 스트리밍 빌드 도구 키트 클라이언트 쪽 코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-113">Gulp is a JavaScript-based streaming build toolkit for client-side code.</span></span> <span data-ttu-id="a94e3-114">일반적으로 빌드 환경에서 특정 이벤트가 트리거될 때 일련의 프로세스를 통해 클라이언트 쪽 파일을 스트림 하는 것이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-114">It's commonly used to stream client-side files through a series of processes when a specific event is triggered in a build environment.</span></span> <span data-ttu-id="a94e3-115">예를 들어, Gulp 수 자동화 [묶음 및 축소](bundling-and-minification.md) 또는 새 빌드 전에 개발 환경을 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-115">For instance, Gulp can be used to automate [bundling and minification](bundling-and-minification.md) or the cleaning of a development environment before a new build.</span></span>

<span data-ttu-id="a94e3-116">Gulp 작업 집합은 *gulpfile.js*에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-116">A set of Gulp tasks is defined in *gulpfile.js*.</span></span> <span data-ttu-id="a94e3-117">다음 JavaScript는 Gulp 모듈을 포함하고 이후 작업에서 참조할 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-117">The following JavaScript includes Gulp modules and specifies file paths to be referenced within the forthcoming tasks:</span></span>

```javascript
/// <binding Clean='clean' />
"use strict";

var gulp = require("gulp"),
    rimraf = require("rimraf"),
    concat = require("gulp-concat"),
    cssmin = require("gulp-cssmin"),
    uglify = require("gulp-uglify");

var paths = {
  webroot: "./wwwroot/"
};

paths.js = paths.webroot + "js/**/*.js";
paths.minJs = paths.webroot + "js/**/*.min.js";
paths.css = paths.webroot + "css/**/*.css";
paths.minCss = paths.webroot + "css/**/*.min.css";
paths.concatJsDest = paths.webroot + "js/site.min.js";
paths.concatCssDest = paths.webroot + "css/site.min.css";
```

<span data-ttu-id="a94e3-118">이 코드는 필요한 Node 모듈을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-118">The above code specifies which Node modules are required.</span></span> <span data-ttu-id="a94e3-119">`require` 함수는 종속적인 작업이 해당 모듈의 기능을 활용할 수 있도록 각 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-119">The `require` function imports each module so that the dependent tasks can utilize their features.</span></span> <span data-ttu-id="a94e3-120">가져온 모듈은 각각 변수에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-120">Each of the imported modules is assigned to a variable.</span></span> <span data-ttu-id="a94e3-121">모듈은 이름이나 경로로 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-121">The modules can be located either by name or path.</span></span> <span data-ttu-id="a94e3-122">이 예제에서는 `gulp`, `rimraf`, `gulp-concat`, `gulp-cssmin`, 및 `gulp-uglify`라는 모듈을 이름으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-122">In this example, the modules named `gulp`, `rimraf`, `gulp-concat`, `gulp-cssmin`, and `gulp-uglify` are retrieved by name.</span></span> <span data-ttu-id="a94e3-123">또한 CSS 및 JavaScript 파일의 위치를 작업 내에서 재사용하고 참조할 수 있도록 일련의 경로을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-123">Additionally, a series of paths are created so that the locations of CSS and JavaScript files can be reused and referenced within the tasks.</span></span> <span data-ttu-id="a94e3-124">다음 표는 *gulpfile.js*에 포함된 모듈에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-124">The following table provides descriptions of the modules included in *gulpfile.js*.</span></span>

| <span data-ttu-id="a94e3-125">모듈 이름</span><span class="sxs-lookup"><span data-stu-id="a94e3-125">Module Name</span></span> | <span data-ttu-id="a94e3-126">설명</span><span class="sxs-lookup"><span data-stu-id="a94e3-126">Description</span></span> |
| ----------- | ----------- |
| <span data-ttu-id="a94e3-127">Gulp</span><span class="sxs-lookup"><span data-stu-id="a94e3-127">gulp</span></span>        | <span data-ttu-id="a94e3-128">Gulp 스트리밍 빌드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-128">The Gulp streaming build system.</span></span> <span data-ttu-id="a94e3-129">자세한 내용은 [gulp](https://www.npmjs.com/package/gulp)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-129">For more information, see [gulp](https://www.npmjs.com/package/gulp).</span></span> |
| <span data-ttu-id="a94e3-130">rimraf</span><span class="sxs-lookup"><span data-stu-id="a94e3-130">rimraf</span></span>      | <span data-ttu-id="a94e3-131">노드 삭제 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-131">A Node deletion module.</span></span> <span data-ttu-id="a94e3-132">자세한 내용은 [rimraf](https://www.npmjs.com/package/rimraf)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-132">For more information, see [rimraf](https://www.npmjs.com/package/rimraf).</span></span> |
| <span data-ttu-id="a94e3-133">gulp concat</span><span class="sxs-lookup"><span data-stu-id="a94e3-133">gulp-concat</span></span> | <span data-ttu-id="a94e3-134">운영 체제의 줄 바꿈 문자를 기준으로 파일을 연결 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-134">A module that concatenates files based on the operating system's newline character.</span></span> <span data-ttu-id="a94e3-135">자세한 내용은 [gulp concat](https://www.npmjs.com/package/gulp-concat)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-135">For more information, see [gulp-concat](https://www.npmjs.com/package/gulp-concat).</span></span> |
| <span data-ttu-id="a94e3-136">gulp cssmin</span><span class="sxs-lookup"><span data-stu-id="a94e3-136">gulp-cssmin</span></span> | <span data-ttu-id="a94e3-137">CSS 파일을 축소 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-137">A module that minifies CSS files.</span></span> <span data-ttu-id="a94e3-138">자세한 내용은 [gulp cssmin](https://www.npmjs.com/package/gulp-cssmin)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-138">For more information, see [gulp-cssmin](https://www.npmjs.com/package/gulp-cssmin).</span></span> |
| <span data-ttu-id="a94e3-139">gulp uglify</span><span class="sxs-lookup"><span data-stu-id="a94e3-139">gulp-uglify</span></span> | <span data-ttu-id="a94e3-140">축소 하는 모듈 *.js* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-140">A module that minifies *.js* files.</span></span> <span data-ttu-id="a94e3-141">자세한 내용은 [gulp uglify](https://www.npmjs.com/package/gulp-uglify)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-141">For more information, see [gulp-uglify](https://www.npmjs.com/package/gulp-uglify).</span></span> |

<span data-ttu-id="a94e3-142">필요한 모듈을 가져왔으면 이제 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-142">Once the requisite modules are imported, the tasks can be specified.</span></span> <span data-ttu-id="a94e3-143">다음과 같은 코드로 표시되는 등록된 여섯 가지 작업이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-143">Here there are six tasks registered, represented by the following code:</span></span>

```javascript
gulp.task("clean:js", done => rimraf(paths.concatJsDest, done));
gulp.task("clean:css", done => rimraf(paths.concatCssDest, done));
gulp.task("clean", gulp.series(["clean:js", "clean:css"]));

gulp.task("min:js", () => {
  return gulp.src([paths.js, "!" + paths.minJs], { base: "." })
    .pipe(concat(paths.concatJsDest))
    .pipe(uglify())
    .pipe(gulp.dest("."));
});

gulp.task("min:css", () => {
  return gulp.src([paths.css, "!" + paths.minCss])
    .pipe(concat(paths.concatCssDest))
    .pipe(cssmin())
    .pipe(gulp.dest("."));
});

gulp.task("min", gulp.series(["min:js", "min:css"]));
    
// A 'default' task is required by Gulp v4
gulp.task("default", gulp.series(["min"]));
```

---

<span data-ttu-id="a94e3-144">다음 표는 위의 코드에서 지정하는 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-144">The following table provides an explanation of the tasks specified in the code above:</span></span>

|<span data-ttu-id="a94e3-145">작업 이름</span><span class="sxs-lookup"><span data-stu-id="a94e3-145">Task Name</span></span>|<span data-ttu-id="a94e3-146">설명</span><span class="sxs-lookup"><span data-stu-id="a94e3-146">Description</span></span>|
|--- |--- |
|<span data-ttu-id="a94e3-147">정리: js</span><span class="sxs-lookup"><span data-stu-id="a94e3-147">clean:js</span></span>|<span data-ttu-id="a94e3-148">Site.js 파일의 축소 된 버전을 제거 하려면 rimraf 노드 삭제 모듈을 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-148">A task that uses the rimraf Node deletion module to remove the minified version of the site.js file.</span></span>|
|<span data-ttu-id="a94e3-149">정리: css</span><span class="sxs-lookup"><span data-stu-id="a94e3-149">clean:css</span></span>|<span data-ttu-id="a94e3-150">Site.css 파일의 축소 된 버전을 제거 하려면 rimraf 노드 삭제 모듈을 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-150">A task that uses the rimraf Node deletion module to remove the minified version of the site.css file.</span></span>|
|<span data-ttu-id="a94e3-151">정리</span><span class="sxs-lookup"><span data-stu-id="a94e3-151">clean</span></span>|<span data-ttu-id="a94e3-152">호출 하는 태스크를 `clean:js` 태스크인 뒤에 `clean:css` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-152">A task that calls the `clean:js` task, followed by the `clean:css` task.</span></span>|
|<span data-ttu-id="a94e3-153">min:js</span><span class="sxs-lookup"><span data-stu-id="a94e3-153">min:js</span></span>|<span data-ttu-id="a94e3-154">축소 및 js 폴더 내의 모든.js 파일을 연결 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-154">A task that minifies and concatenates all .js files within the js folder.</span></span> <span data-ttu-id="a94e3-155">. min.js 파일은 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-155">The .min.js files are excluded.</span></span>|
|<span data-ttu-id="a94e3-156">min:css</span><span class="sxs-lookup"><span data-stu-id="a94e3-156">min:css</span></span>|<span data-ttu-id="a94e3-157">축소 및 css 폴더 내의 모든.css 파일을 연결 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-157">A task that minifies and concatenates all .css files within the css folder.</span></span> <span data-ttu-id="a94e3-158">. min.css 파일은 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-158">The .min.css files are excluded.</span></span>|
|<span data-ttu-id="a94e3-159">분</span><span class="sxs-lookup"><span data-stu-id="a94e3-159">min</span></span>|<span data-ttu-id="a94e3-160">호출 하는 태스크를 `min:js` 태스크인 뒤에 `min:css` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-160">A task that calls the `min:js` task, followed by the `min:css` task.</span></span>|

## <a name="running-default-tasks"></a><span data-ttu-id="a94e3-161">기본 작업 실행하기</span><span class="sxs-lookup"><span data-stu-id="a94e3-161">Running default tasks</span></span>

<span data-ttu-id="a94e3-162">아직 새로운 웹 앱을 만들지 않았다면 Visual Studio에서 새로운 ASP.NET Core 웹 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-162">If you haven't already created a new Web app, create a new ASP.NET Web Application project in Visual Studio.</span></span>

1.  <span data-ttu-id="a94e3-163">*package.json* 파일을 열고(파일이 없으면 추가) 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-163">Open the *package.json* file (add if not there) and add the following.</span></span>

    ```json
    {
      "devDependencies": {
        "gulp": "^4.0.0",
        "gulp-concat": "2.6.1",
        "gulp-cssmin": "0.2.0",
        "gulp-uglify": "3.0.0",
        "rimraf": "2.6.1"
      }
    }
    ```

2.  <span data-ttu-id="a94e3-164">새로운 JavaScript 파일을 프로젝트에 추가하고 이름을 *gulpfile.js*로 지정한 다음, 다음 코드를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-164">Add a new JavaScript file to your project and name it *gulpfile.js*, then copy the following code.</span></span>

    ```javascript
    /// <binding Clean='clean' />
    "use strict";
    
    const gulp = require("gulp"),
          rimraf = require("rimraf"),
          concat = require("gulp-concat"),
          cssmin = require("gulp-cssmin"),
          uglify = require("gulp-uglify");
    
    const paths = {
      webroot: "./wwwroot/"
    };
    
    paths.js = paths.webroot + "js/**/*.js";
    paths.minJs = paths.webroot + "js/**/*.min.js";
    paths.css = paths.webroot + "css/**/*.css";
    paths.minCss = paths.webroot + "css/**/*.min.css";
    paths.concatJsDest = paths.webroot + "js/site.min.js";
    paths.concatCssDest = paths.webroot + "css/site.min.css";
    
    gulp.task("clean:js", done => rimraf(paths.concatJsDest, done));
    gulp.task("clean:css", done => rimraf(paths.concatCssDest, done));
    gulp.task("clean", gulp.series(["clean:js", "clean:css"]));

    gulp.task("min:js", () => {
      return gulp.src([paths.js, "!" + paths.minJs], { base: "." })
        .pipe(concat(paths.concatJsDest))
        .pipe(uglify())
        .pipe(gulp.dest("."));
    });

    gulp.task("min:css", () => {
      return gulp.src([paths.css, "!" + paths.minCss])
        .pipe(concat(paths.concatCssDest))
        .pipe(cssmin())
        .pipe(gulp.dest("."));
    });

    gulp.task("min", gulp.series(["min:js", "min:css"]));
    
    // A 'default' task is required by Gulp v4
    gulp.task("default", gulp.series(["min"]));
    ```

3.  <span data-ttu-id="a94e3-165">**솔루션 탐색기**에서 마우스 오른쪽 버튼으로 *gulpfile.js*를 클릭하고 **작업 러너 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-165">In **Solution Explorer**, right-click *gulpfile.js*, and select **Task Runner Explorer**.</span></span>
    
    ![솔루션 탐색기에서 작업 러너 탐색기 열기](using-gulp/_static/02-SolutionExplorer-TaskRunnerExplorer.png)
    
    <span data-ttu-id="a94e3-167">**작업 러너 탐색기**에 Gulp 작업 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-167">**Task Runner Explorer** shows the list of Gulp tasks.</span></span> <span data-ttu-id="a94e3-168">(프로젝트 이름 좌측에 위치한 **새로 고침** 버튼을 클릭해야 할 수도 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="a94e3-168">(You might have to click the **Refresh** button that appears to the left of the project name.)</span></span>
    
    ![작업 러너 탐색기](using-gulp/_static/03-TaskRunnerExplorer.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="a94e3-170">**작업 러너 탐색기** 컨텍스트 메뉴 항목은 *gulpfile.js*가 루트 프로젝트 디렉토리에 있는 경우에만 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-170">The **Task Runner Explorer** context menu item appears only if *gulpfile.js* is in the root project directory.</span></span>

4.  <span data-ttu-id="a94e3-171">**작업 러너 탐색기**에서 **작업** 하위의 **clean**을 마우스 오른쪽 버튼으로 클릭하고 팝업 메뉴에서 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-171">Underneath **Tasks** in **Task Runner Explorer**, right-click **clean**, and select **Run** from the pop-up menu.</span></span>

    ![작업 러너 탐색기 clean 작업](using-gulp/_static/04-TaskRunner-clean.png)

    <span data-ttu-id="a94e3-173">그러면 **작업 러너 탐색기**가 **clean**이라는 새로운 탭을 열고 *gulpfile.js*에 정의된 대로 정리 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-173">**Task Runner Explorer** will create a new tab named **clean** and execute the clean task as it's defined in *gulpfile.js*.</span></span>

5.  <span data-ttu-id="a94e3-174">마우스 오른쪽 버튼으로 **clean** 작업을 클릭한 다음, **바인딩** > **빌드 전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-174">Right-click the **clean** task, then select **Bindings** > **Before Build**.</span></span>

    ![작업 러너 탐색기 빌드 전 바인딩](using-gulp/_static/05-TaskRunner-BeforeBuild.png)

    <span data-ttu-id="a94e3-176">**빌드 전 바인딩**은 매번 프로젝트를 빌드하기 전에 clean 작업을 자동으로 실행하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-176">The **Before Build** binding configures the clean task to run automatically before each build of the project.</span></span>

<span data-ttu-id="a94e3-177">**작업 러너 탐색기**로 설정한 바인딩은 *gulpfile.js*의 맨 위에 주석 형태로 저장되며 Visual Studio에서만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-177">The bindings you set up with **Task Runner Explorer** are stored in the form of a comment at the top of your *gulpfile.js* and are effective only in Visual Studio.</span></span> <span data-ttu-id="a94e3-178">Visual Studio가 필요 없는 다른 방법은 *.csproj* 파일에서 gulp 작업의 자동 실행을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-178">An alternative that doesn't require Visual Studio is to configure automatic execution of gulp tasks in your *.csproj* file.</span></span> <span data-ttu-id="a94e3-179">예를 들어 *.csproj* 파일에 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-179">For example, put this in your *.csproj* file:</span></span>

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="gulp clean" />
</Target>
```

<span data-ttu-id="a94e3-180">이제 Visual Studio에서 프로젝트를 실행하거나 명령 프롬프트에서 [dotnet run](/dotnet/core/tools/dotnet-run) 명령으로(먼저 `npm install`을 실행해야 함) 프로젝트를 실행하면 clean 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-180">Now the clean task is executed when you run the project in Visual Studio or from a command prompt using the [dotnet run](/dotnet/core/tools/dotnet-run) command (run `npm install` first).</span></span>

## <a name="defining-and-running-a-new-task"></a><span data-ttu-id="a94e3-181">새로운 작업 정의하고 실행하기</span><span class="sxs-lookup"><span data-stu-id="a94e3-181">Defining and running a new task</span></span>

<span data-ttu-id="a94e3-182">새로운 Gulp 작업을 정의하려면 *gulpfile.js*를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-182">To define a new Gulp task, modify *gulpfile.js*.</span></span>

1.  <span data-ttu-id="a94e3-183">*gulpfile.js*의 끝 부분에 다음 JavaScript를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-183">Add the following JavaScript to the end of *gulpfile.js*:</span></span>

    ```javascript
    gulp.task('first', done => {
      console.log('first task! <-----');
      done(); // signal completion
    });
    ```

    <span data-ttu-id="a94e3-184">이 작업의 이름은 `first`로, 단순히 문자열만 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-184">This task is named `first`, and it simply displays a string.</span></span>

2.  <span data-ttu-id="a94e3-185">*gulpfile.js*를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-185">Save *gulpfile.js*.</span></span>

3.  <span data-ttu-id="a94e3-186">**솔루션 탐색기**에서 마우스 오른쪽 버튼으로 *gulpfile.js*를 클릭하고 *작업 러너 탐색기*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-186">In **Solution Explorer**, right-click *gulpfile.js*, and select *Task Runner Explorer*.</span></span>

4.  <span data-ttu-id="a94e3-187">**작업 러너 탐색기**에서 마우스 오른쪽 버튼으로 **first**를 클릭하고 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-187">In **Task Runner Explorer**, right-click **first**, and select **Run**.</span></span>

    ![first 작업을 실행하는 작업 러너 탐색기](using-gulp/_static/06-TaskRunner-First.png)

    <span data-ttu-id="a94e3-189">출력 텍스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-189">The output text is displayed.</span></span> <span data-ttu-id="a94e3-190">일반적인 시나리오를 기반으로 한 예제를 살펴보려면 [Gulp 레시피](#gulp-recipes)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-190">To see examples based on common scenarios, see [Gulp Recipes](#gulp-recipes).</span></span>

## <a name="defining-and-running-tasks-in-a-series"></a><span data-ttu-id="a94e3-191">연속 작업 정의하고 실행하기</span><span class="sxs-lookup"><span data-stu-id="a94e3-191">Defining and running tasks in a series</span></span>

<span data-ttu-id="a94e3-192">여러 작업을 실행할 때 작업은 기본적으로 동시에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-192">When you run multiple tasks, the tasks run concurrently by default.</span></span> <span data-ttu-id="a94e3-193">그러나 특정 순서에 따라 작업을 실행해야 하는 경우, 각 작업이 완료되는 시점과 다른 작업의 완료에 따라 영향을 받는 작업을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-193">However, if you need to run tasks in a specific order, you must specify when each task is complete, as well as which tasks depend on the completion of another task.</span></span>

1.  <span data-ttu-id="a94e3-194">순차적으로 실행되는 일련의 작업을 정의하려면 앞에서 *gulpfile.js*에 추가했던 `first` 작업을 다음으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-194">To define a series of tasks to run in order, replace the `first` task that you added above in *gulpfile.js* with the following:</span></span>

    ```javascript
    gulp.task('series:first', done => {
      console.log('first task! <-----');
      done(); // signal completion
    });
    gulp.task('series:second', done => {
      console.log('second task! <-----');
      done(); // signal completion
    });

    gulp.task('series', gulp.series(['series:first', 'series:second']), () => { });

    // A 'default' task is required by Gulp v4
    gulp.task('default', gulp.series('series'));
    ```
 
    <span data-ttu-id="a94e3-195">이제 `series:first`, `series:second`, 및 `series`라는 세 가지 작업이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-195">You now have three tasks: `series:first`, `series:second`, and `series`.</span></span> <span data-ttu-id="a94e3-196">`series:second` 작업은 `series:second` 작업이 실행되기 전에 실행되어 완료되어야 하는 작업의 배열을 지정하는 두 번째 매개 변수를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-196">The `series:second` task includes a second parameter which specifies an array of tasks to be run and completed before the `series:second` task will run.</span></span> <span data-ttu-id="a94e3-197">이 코드에 지정된 것처럼 `series:second` 작업을 실행하려면 `series:first` 작업만 완료되면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-197">As specified in the code above, only the `series:first` task must be completed before the `series:second` task will run.</span></span>

2.  <span data-ttu-id="a94e3-198">*gulpfile.js*를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-198">Save *gulpfile.js*.</span></span>

3.  <span data-ttu-id="a94e3-199">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *gulpfile.js* 선택한 **Task Runner 탐색기** 아직 열려 있지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="a94e3-199">In **Solution Explorer**, right-click *gulpfile.js* and select **Task Runner Explorer** if it isn't already open.</span></span>

4.  <span data-ttu-id="a94e3-200">**작업 러너 탐색기**에서 마우스 오른쪽 버튼으로 **series**를 클릭하고 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-200">In **Task Runner Explorer**, right-click **series** and select **Run**.</span></span>

    ![series 작업을 실행하는 작업 러너 탐색기](using-gulp/_static/07-TaskRunner-Series.png)

## <a name="intellisense"></a><span data-ttu-id="a94e3-202">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="a94e3-202">IntelliSense</span></span>

<span data-ttu-id="a94e3-203">IntelliSense는 코드 완성, 매개 변수 설명 및 그 밖의 기능을 제공하여 생산성을 높이고 오류를 줄여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-203">IntelliSense provides code completion, parameter descriptions, and other features to boost productivity and to decrease errors.</span></span> <span data-ttu-id="a94e3-204">Gulp 작업은 JavaScript로 작성되며, 따라서 개발하는 동안 IntelliSense가 지원을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-204">Gulp tasks are written in JavaScript; therefore, IntelliSense can provide assistance while developing.</span></span> <span data-ttu-id="a94e3-205">JavaScript를 사용해서 작업하는 동안 IntelliSense가 현재 문맥을 기반으로 사용할 수 있는 개체, 함수, 속성 및 매개 변수를 나열해줍니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-205">As you work with JavaScript, IntelliSense lists the objects, functions, properties, and parameters that are available based on your current context.</span></span> <span data-ttu-id="a94e3-206">IntelliSense가 제공하는 팝업 목록에서 코딩 옵션을 선택하여 코드를 완성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-206">Select a coding option from the pop-up list provided by IntelliSense to complete the code.</span></span>

![gulp IntelliSense](using-gulp/_static/08-IntelliSense.png)

<span data-ttu-id="a94e3-208">IntelliSense에 대 한 자세한 내용은 참조 하세요. [JavaScript IntelliSense](/visualstudio/ide/javascript-intellisense)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-208">For more information about IntelliSense, see [JavaScript IntelliSense](/visualstudio/ide/javascript-intellisense).</span></span>

## <a name="development-staging-and-production-environments"></a><span data-ttu-id="a94e3-209">개발, 스테이징 및 프로덕션 환경</span><span class="sxs-lookup"><span data-stu-id="a94e3-209">Development, staging, and production environments</span></span>

<span data-ttu-id="a94e3-210">Gulp를 스테이징 및 프로덕션에 대한 클라이언트 쪽 파일 최적화에 사용하면 처리된 파일이 로컬 스테이징 및 프로덕션 위치에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-210">When Gulp is used to optimize client-side files for staging and production, the processed files are saved to a local staging and production location.</span></span> <span data-ttu-id="a94e3-211">*_Layout.cshtml* 파일은 **environment** 태그 도우미를 활용하여 두 가지 버전의 CSS 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-211">The *_Layout.cshtml* file uses the **environment** tag helper to provide two different versions of CSS files.</span></span> <span data-ttu-id="a94e3-212">CSS 파일의 한 버전은 개발용이며 다른 버전은 스테이징 및 프로덕션 환경 모두를 위해 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-212">One version of CSS files is for development and the other version is optimized for both staging and production.</span></span> <span data-ttu-id="a94e3-213">Visual Studio 2017에서 **ASPNETCORE_ENVIRONMENT** 환경 변수를 `Production`으로 변경하면, Visual Studio가 웹 앱을 빌드하고 최소화된 CSS 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-213">In Visual Studio 2017, when you change the **ASPNETCORE_ENVIRONMENT** environment variable to `Production`, Visual Studio will build the Web app and link to the minimized CSS files.</span></span> <span data-ttu-id="a94e3-214">다음 태그는 `Development` CSS 파일과 축소된 `Staging, Production` CSS 파일에 대한 참조 태그를 포함하고 있는 **environment** 태그 도우미를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-214">The following markup shows the **environment** tag helpers containing link tags to the `Development` CSS files and the minified `Staging, Production` CSS files.</span></span>

```html
<environment names="Development">
    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/js/site.js" asp-append-version="true"></script>
</environment>
<environment names="Staging,Production">
    <script src="https://ajax.aspnetcdn.com/ajax/jquery/jquery-2.2.0.min.js"
            asp-fallback-src="~/lib/jquery/dist/jquery.min.js"
            asp-fallback-test="window.jQuery"
            crossorigin="anonymous"
            integrity="sha384-K+ctZQ+LL8q6tP7I94W+qzQsfRV2a+AfHIi9k8z8l9ggpc8X+Ytst4yBo/hH+8Fk">
    </script>
    <script src="https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js"
            asp-fallback-src="~/lib/bootstrap/dist/js/bootstrap.min.js"
            asp-fallback-test="window.jQuery && window.jQuery.fn && window.jQuery.fn.modal"
            crossorigin="anonymous"
            integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa">
    </script>
    <script src="~/js/site.min.js" asp-append-version="true"></script>
</environment>
```

## <a name="switching-between-environments"></a><span data-ttu-id="a94e3-215">환경 전환하기</span><span class="sxs-lookup"><span data-stu-id="a94e3-215">Switching between environments</span></span>

<span data-ttu-id="a94e3-216">서로 다른 환경에 대한 컴파일로 전환하려면 **ASPNETCORE_ENVIRONMENT** 환경 변수의 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-216">To switch between compiling for different environments, modify the **ASPNETCORE_ENVIRONMENT** environment variable's value.</span></span>

1.  <span data-ttu-id="a94e3-217">**작업 러너 탐색기**에서 **min** 작업이 **빌드 전**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-217">In **Task Runner Explorer**, verify that the **min** task has been set to run **Before Build**.</span></span>

2.  <span data-ttu-id="a94e3-218">**솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 버튼으로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-218">In **Solution Explorer**, right-click the project name and select **Properties**.</span></span>

    <span data-ttu-id="a94e3-219">그러면 웹 앱에 대한 속성 시트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-219">The property sheet for the Web app is displayed.</span></span>

3.  <span data-ttu-id="a94e3-220">**디버그** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-220">Click the **Debug** tab.</span></span>

4.  <span data-ttu-id="a94e3-221">**ASPNETCORE_ENVIRONMENT** 환경 변수의 값을 `Production`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-221">Set the value of the **Hosting:Environment** environment variable to `Production`.</span></span>

5.  <span data-ttu-id="a94e3-222">**F5** 키를 눌러서 응용 프로그램을 브라우저에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-222">Press **F5** to run the application in a browser.</span></span>

6.  <span data-ttu-id="a94e3-223">브라우저 창에서 마우스 오른쪽 버튼으로 페이지를 클릭하고 **소스 보기**를 선택하여 페이지의 HTML을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-223">In the browser window, right-click the page and select **View Source** to view the HTML for the page.</span></span>

    <span data-ttu-id="a94e3-224">스타일시트가 축소된 CSS 파일을 링크하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-224">Notice that the stylesheet links point to the minified CSS files.</span></span>

7.  <span data-ttu-id="a94e3-225">브라우저를 닫아서 웹 앱을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-225">Close the browser to stop the Web app.</span></span>

8.  <span data-ttu-id="a94e3-226">Visual Studio에서 다시 웹 앱에 대한 속성 시트로 되돌아가서 **ASPNETCORE_ENVIRONMENT** 환경 변수의 값을 `Development`으로 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-226">In Visual Studio, return to the property sheet for the Web app and change the **Hosting:Environment** environment variable back to `Development`.</span></span>

9.  <span data-ttu-id="a94e3-227">**F5** 키를 눌러서 다시 응용 프로그램을 브라우저에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-227">Press **F5** to run the application in a browser again.</span></span>

10. <span data-ttu-id="a94e3-228">브라우저 창에서 마우스 오른쪽 버튼으로 페이지를 클릭하고 **소스 보기**를 선택하여 페이지의 HTML을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-228">In the browser window, right-click the page and select **View Source** to see the HTML for the page.</span></span>

    <span data-ttu-id="a94e3-229">스타일시트가 축소되지 않은 버전의 CSS 파일을 링크하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-229">Notice that the stylesheet links point to the unminified versions of the CSS files.</span></span>

<span data-ttu-id="a94e3-230">ASP.NET Core의 환경에 관한 자세한 내용은 [여러 환경 사용하기](../fundamentals/environments.md)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-230">For more information related to environments in ASP.NET Core, see [Use multiple environments](../fundamentals/environments.md).</span></span>

## <a name="task-and-module-details"></a><span data-ttu-id="a94e3-231">작업 및 모듈 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a94e3-231">Task and module details</span></span>

<span data-ttu-id="a94e3-232">Gulp 작업은 함수 이름으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-232">A Gulp task is registered with a function name.</span></span> <span data-ttu-id="a94e3-233">다른 작업을 현재 작업보다 먼저 실행해야 할 경우 종속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-233">You can specify dependencies if other tasks must run before the current task.</span></span> <span data-ttu-id="a94e3-234">추가적인 함수를 사용하면 Gulp 작업을 실행하고 모니터링 할 수 있을 뿐만 아니라 수정되는 파일의 원본(*src*)과 대상(*dest*)을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-234">Additional functions allow you to run and watch the Gulp tasks, as well as set the source (*src*) and destination (*dest*) of the files being modified.</span></span> <span data-ttu-id="a94e3-235">다음은 기본적인 Gulp API 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-235">The following are the primary Gulp API functions:</span></span>

|<span data-ttu-id="a94e3-236">Gulp 함수</span><span class="sxs-lookup"><span data-stu-id="a94e3-236">Gulp Function</span></span>|<span data-ttu-id="a94e3-237">구문</span><span class="sxs-lookup"><span data-stu-id="a94e3-237">Syntax</span></span>|<span data-ttu-id="a94e3-238">설명</span><span class="sxs-lookup"><span data-stu-id="a94e3-238">Description</span></span>|
|---   |--- |--- |
|<span data-ttu-id="a94e3-239">task</span><span class="sxs-lookup"><span data-stu-id="a94e3-239">task</span></span>  |`gulp.task(name[, deps], fn) { }`|<span data-ttu-id="a94e3-240">`task` 함수는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-240">The `task` function creates a task.</span></span> <span data-ttu-id="a94e3-241">`name` 매개 변수는 작업의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-241">The `name` parameter defines the name of the task.</span></span> <span data-ttu-id="a94e3-242">`deps` 매개 변수에는 이 작업을 실행하기 전에 완료해야 할 작업의 배열을 담습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-242">The `deps` parameter contains an array of tasks to be completed before this task runs.</span></span> <span data-ttu-id="a94e3-243">`fn` 매개 변수는 이 작업의 실제 작업을 수행하는 콜백 함수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-243">The `fn` parameter represents a callback function which performs the operations of the task.</span></span>|
|<span data-ttu-id="a94e3-244">watch</span><span class="sxs-lookup"><span data-stu-id="a94e3-244">watch</span></span> |`gulp.watch(glob [, opts], tasks) { }`|<span data-ttu-id="a94e3-245">`watch` 함수는 파일을 모니터링하고 파일이 변경되면 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-245">The `watch` function monitors files and runs tasks when a file change occurs.</span></span> <span data-ttu-id="a94e3-246">`glob` 매개 변수는 모니터링 할 파일을 결정하는 `string` 또는 `array`입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-246">The `glob` parameter is a `string` or `array` that determines which files to watch.</span></span> <span data-ttu-id="a94e3-247">`opts` 매개 변수는 추가적인 파일 모니터링 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-247">The `opts` parameter provides additional file watching options.</span></span>|
|<span data-ttu-id="a94e3-248">src</span><span class="sxs-lookup"><span data-stu-id="a94e3-248">src</span></span>   |`gulp.src(globs[, options]) { }`|<span data-ttu-id="a94e3-249">`src` 함수는 glob 값과 일치하는 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-249">The `src` function provides files that match the glob value(s).</span></span> <span data-ttu-id="a94e3-250">`glob` 매개 변수는 읽을 파일을 결정하는 `string` 또는 `array`입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-250">The `glob` parameter is a `string` or `array` that determines which files to read.</span></span> <span data-ttu-id="a94e3-251">`options` 매개 변수는 추가적인 파일 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-251">The `options` parameter provides additional file options.</span></span>|
|<span data-ttu-id="a94e3-252">dest</span><span class="sxs-lookup"><span data-stu-id="a94e3-252">dest</span></span>  |`gulp.dest(path[, options]) { }`|<span data-ttu-id="a94e3-253">`dest` 함수는 파일을 쓸 수 있는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-253">The `dest` function defines a location to which files can be written.</span></span> <span data-ttu-id="a94e3-254">`path` 매개 변수는 대상 폴더를 결정하는 문자열 또는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-254">The `path` parameter is a string or function that determines the destination folder.</span></span> <span data-ttu-id="a94e3-255">`options` 매개 변수는 출력 폴더 옵션을 지정하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-255">The `options` parameter is an object that specifies output folder options.</span></span>|

<span data-ttu-id="a94e3-256">추가적인 Gulp API 참조 정보는 [Gulp Docs API](https://github.com/gulpjs/gulp/blob/master/docs/API.md)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-256">For additional Gulp API reference information, see [Gulp Docs API](https://github.com/gulpjs/gulp/blob/master/docs/API.md).</span></span>

## <a name="gulp-recipes"></a><span data-ttu-id="a94e3-257">Gulp 레시피</span><span class="sxs-lookup"><span data-stu-id="a94e3-257">Gulp recipes</span></span>

<span data-ttu-id="a94e3-258">Gulp 커뮤니티는 Gulp [레시피](https://github.com/gulpjs/gulp/blob/master/docs/recipes/README.md)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-258">The Gulp community provides Gulp [Recipes](https://github.com/gulpjs/gulp/blob/master/docs/recipes/README.md).</span></span> <span data-ttu-id="a94e3-259">이러한 레시피는 일반적인 시나리오를 다루는 Gulp 작업으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94e3-259">These recipes consist of Gulp tasks to address common scenarios.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a94e3-260">추가 자료</span><span class="sxs-lookup"><span data-stu-id="a94e3-260">Additional resources</span></span>

* [<span data-ttu-id="a94e3-261">Gulp 문서</span><span class="sxs-lookup"><span data-stu-id="a94e3-261">Gulp documentation</span></span>](https://github.com/gulpjs/gulp/blob/master/docs/README.md)
* [<span data-ttu-id="a94e3-262">ASP.NET Core의 번들링 및 축소</span><span class="sxs-lookup"><span data-stu-id="a94e3-262">Bundling and minification in ASP.NET Core</span></span>](bundling-and-minification.md)
* [<span data-ttu-id="a94e3-263">ASP.NET Core에서 Grunt 사용하기</span><span class="sxs-lookup"><span data-stu-id="a94e3-263">Use Grunt in ASP.NET Core</span></span>](using-grunt.md)
