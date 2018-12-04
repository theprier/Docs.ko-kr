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
# <a name="use-gulp-in-aspnet-core"></a>ASP.NET Core에서 Gulp 사용하기

작성자: [Scott Addie](https://scottaddie.com), [Shayne Boyer](https://twitter.com/spboyer), 및 [David Pine](https://twitter.com/davidpine7)

일반적인 최신 웹 앱에서 빌드 프로세스는 다음과 같은 작업을 수행할 수 있습니다.

* JavaScript 및 CSS 파일을 번들링하고 축소합니다.
* 매번 빌드하기 전에 번들링 및 축소 작업을 호출하는 도구를 실행합니다.
* LESS 또는 SASS 파일을 CSS로 컴파일합니다.
* CoffeeScript 또는 TypeScript 파일을 JavaScript로 컴파일합니다.

*작업 러너*는 이러한 일상적인 개발 작업 등을 자동화하는 도구입니다. Visual Studio는 두 가지 인기 있는 JavaScript 기반의 작업 러너인 [Gulp](https://gulpjs.com/)와 [Grunt](using-grunt.md)에 대한 기본 지원을 제공합니다.

## <a name="gulp"></a>Gulp

Gulp는 클라이언트 쪽 코드에 대한 JavaScript 기반의 스트리밍 빌드 도구 키트입니다. 일반적으로 빌드 환경에서 특정 이벤트가 트리거될 때 클라이언트 쪽 파일을 일련의 프로세스를 통해서 스트리밍하는 데 사용됩니다. 예를 들어 [번들링 및 축소](bundling-and-minification.md) 작업이나 새로운 빌드 전에 개발 환경을 정리하는 작업을 자동화하기 위해 Gulp를 사용할 수 있습니다.

Gulp 작업 집합은 *gulpfile.js*에 정의됩니다. 다음 JavaScript는 Gulp 모듈을 포함하고 이후 작업에서 참조할 파일 경로를 지정합니다.

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

이 코드는 필요한 Node 모듈을 지정합니다. `require` 함수는 종속적인 작업이 해당 모듈의 기능을 활용할 수 있도록 각 모듈을 가져옵니다. 가져온 모듈은 각각 변수에 할당됩니다. 모듈은 이름이나 경로로 찾을 수 있습니다. 이 예제에서는 `gulp`, `rimraf`, `gulp-concat`, `gulp-cssmin`, 및 `gulp-uglify`라는 모듈을 이름으로 검색합니다. 또한 CSS 및 JavaScript 파일의 위치를 작업 내에서 재사용하고 참조할 수 있도록 일련의 경로을 생성합니다. 다음 표는 *gulpfile.js*에 포함된 모듈에 대한 설명입니다.

| 모듈 이름 | 설명 |
| ----------- | ----------- |
| Gulp        | Gulp 스트리밍 빌드 시스템입니다. 자세한 내용은 [gulp](https://www.npmjs.com/package/gulp)를 참고하시기 바랍니다. |
| rimraf      | Node 삭제 모듈입니다. 자세한 내용은 [rimraf](https://www.npmjs.com/package/rimraf)를 참고하시기 바랍니다. |
| gulp concat | 운영 체제의 줄 바꿈 문자를 기반으로 파일을 연결하는 모듈입니다. 자세한 내용은 [gulp concat](https://www.npmjs.com/package/gulp-concat)를 참고하시기 바랍니다. |
| gulp cssmin | CSS 파일을 축소하는 모듈입니다. 자세한 내용은 [gulp cssmin](https://www.npmjs.com/package/gulp-cssmin)을 참고하시기 바랍니다. |
| gulp uglify | *.js* 파일을 축소하는 모듈입니다. 자세한 내용은 [gulp uglify](https://www.npmjs.com/package/gulp-uglify)를 참고하시기 바랍니다. |

필요한 모듈을 가져왔으면 이제 작업을 지정할 수 있습니다. 다음과 같은 코드로 표시되는 등록된 여섯 가지 작업이 존재합니다.

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

다음 표는 위의 코드에서 지정하는 작업을 설명합니다.

|작업 이름|설명|
|--- |--- |
|clean:js|rimraf Node 삭제 모듈을 사용하여 축소된 버전의 site.js 파일을 제거하는 작업입니다.|
|clean:css|rimraf Node 삭제 모듈을 사용하여 축소된 버전의 site.css 파일을 제거하는 작업입니다.|
|clean|`clean:js` 작업을 호출하고 뒤이어 `clean:css` 작업을 호출하는 작업입니다.|
|min:js|js 폴더 내의 모든 .js 파일을 축소 및 연결하는 작업입니다. .min.js 파일들은 제외됩니다.|
|min:css|css 폴더 내의 모든 .css 파일을 축소 및 연결하는 작업입니다. .min.css 파일은 제외됩니다.|
|min|`min:js` 작업을 호출하고 뒤이어 `min:css` 작업을 호출하는 작업입니다.|

## <a name="running-default-tasks"></a>기본 작업 실행하기

아직 새로운 웹 앱을 만들지 않았다면 Visual Studio에서 새로운 ASP.NET Core 웹 응용 프로그램 프로젝트를 만듭니다.

1.  *package.json* 파일을 열고(파일이 없으면 추가) 다음 내용을 추가합니다.

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

2.  새로운 JavaScript 파일을 프로젝트에 추가하고 이름을 *gulpfile.js*로 지정한 다음, 다음 코드를 복사합니다.

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

3.  **솔루션 탐색기**에서 마우스 오른쪽 버튼으로 *gulpfile.js*를 클릭하고 **작업 러너 탐색기**를 선택합니다.
    
    ![솔루션 탐색기에서 작업 러너 탐색기 열기](using-gulp/_static/02-SolutionExplorer-TaskRunnerExplorer.png)
    
    **작업 러너 탐색기**에 Gulp 작업 목록이 표시됩니다. (프로젝트 이름 좌측에 위치한 **새로 고침** 버튼을 클릭해야 할 수도 있습니다.)
    
    ![작업 러너 탐색기](using-gulp/_static/03-TaskRunnerExplorer.png)
    
    > [!IMPORTANT]
    > **작업 러너 탐색기** 컨텍스트 메뉴 항목은 *gulpfile.js*가 루트 프로젝트 디렉토리에 있는 경우에만 나타납니다.

4.  **작업 러너 탐색기**에서 **작업** 하위의 **clean**을 마우스 오른쪽 버튼으로 클릭하고 팝업 메뉴에서 **실행**을 선택합니다.

    ![작업 러너 탐색기 clean 작업](using-gulp/_static/04-TaskRunner-clean.png)

    그러면 **작업 러너 탐색기**가 **clean**이라는 새로운 탭을 열고 *gulpfile.js*에 정의된 대로 정리 작업을 실행합니다.

5.  마우스 오른쪽 버튼으로 **clean** 작업을 클릭한 다음, **바인딩** > **빌드 전**을 선택합니다.

    ![작업 러너 탐색기 빌드 전 바인딩](using-gulp/_static/05-TaskRunner-BeforeBuild.png)

    **빌드 전 바인딩**은 매번 프로젝트를 빌드하기 전에 clean 작업을 자동으로 실행하도록 구성합니다.

**작업 러너 탐색기**로 설정한 바인딩은 *gulpfile.js*의 맨 위에 주석 형태로 저장되며 Visual Studio에서만 적용됩니다. Visual Studio가 필요 없는 다른 방법은 *.csproj* 파일에서 gulp 작업의 자동 실행을 구성하는 것입니다. 예를 들어 *.csproj* 파일에 다음과 같이 입력합니다.

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="gulp clean" />
</Target>
```

이제 Visual Studio에서 프로젝트를 실행하거나 명령 프롬프트에서 [dotnet run](/dotnet/core/tools/dotnet-run) 명령으로(먼저 `npm install`을 실행해야 함) 프로젝트를 실행하면 clean 작업이 실행됩니다.

## <a name="defining-and-running-a-new-task"></a>새로운 작업 정의하고 실행하기

새로운 Gulp 작업을 정의하려면 *gulpfile.js*를 수정합니다.

1.  *gulpfile.js*의 끝 부분에 다음 JavaScript를 추가합니다.

    ```javascript
    gulp.task('first', done => {
      console.log('first task! <-----');
      done(); // signal completion
    });
    ```

    이 작업의 이름은 `first`로, 단순히 문자열만 출력합니다.

2.  *gulpfile.js*를 저장합니다.

3.  **솔루션 탐색기**에서 마우스 오른쪽 버튼으로 *gulpfile.js*를 클릭하고 *작업 러너 탐색기*를 선택합니다.

4.  **작업 러너 탐색기**에서 마우스 오른쪽 버튼으로 **first**를 클릭하고 **실행**을 선택합니다.

    ![first 작업을 실행하는 작업 러너 탐색기](using-gulp/_static/06-TaskRunner-First.png)

    출력 텍스트가 표시됩니다. 일반적인 시나리오를 기반으로 한 예제를 살펴보려면 [Gulp 레시피](#gulp-recipes)를 참고하시기 바랍니다.

## <a name="defining-and-running-tasks-in-a-series"></a>연속 작업 정의하고 실행하기

여러 작업을 실행할 때 작업은 기본적으로 동시에 실행됩니다. 그러나 특정 순서에 따라 작업을 실행해야 하는 경우, 각 작업이 완료되는 시점과 다른 작업의 완료에 따라 영향을 받는 작업을 지정해야 합니다.

1.  순차적으로 실행되는 일련의 작업을 정의하려면 앞에서 *gulpfile.js*에 추가했던 `first` 작업을 다음으로 대체합니다.

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
 
    이제 `series:first`, `series:second`, 및 `series`라는 세 가지 작업이 존재합니다. `series:second` 작업은 `series:second` 작업이 실행되기 전에 실행되어 완료되어야 하는 작업의 배열을 지정하는 두 번째 매개 변수를 포함하고 있습니다. 이 코드에 지정된 것처럼 `series:second` 작업을 실행하려면 `series:first` 작업만 완료되면 됩니다.

2.  *gulpfile.js*를 저장합니다.

3.  **솔루션 탐색기**에서 마우스 오른쪽 버튼으로 *gulpfile.js*를 클릭하고 **작업 러너 탐색기**를 선택합니다.

4.  **작업 러너 탐색기**에서 마우스 오른쪽 버튼으로 **series**를 클릭하고 **실행**을 선택합니다.

    ![series 작업을 실행하는 작업 러너 탐색기](using-gulp/_static/07-TaskRunner-Series.png)

## <a name="intellisense"></a>IntelliSense

IntelliSense는 코드 완성, 매개 변수 설명 및 그 밖의 기능을 제공하여 생산성을 높이고 오류를 줄여줍니다. Gulp 작업은 JavaScript로 작성되며, 따라서 개발하는 동안 IntelliSense가 지원을 제공할 수 있습니다. JavaScript를 사용해서 작업하는 동안 IntelliSense가 현재 문맥을 기반으로 사용할 수 있는 개체, 함수, 속성 및 매개 변수를 나열해줍니다. IntelliSense가 제공하는 팝업 목록에서 코딩 옵션을 선택하여 코드를 완성할 수 있습니다.

![gulp IntelliSense](using-gulp/_static/08-IntelliSense.png)

IntelliSense에 대한 자세한 내용은 [JavaScript IntelliSense](/visualstudio/ide/javascript-intellisense)를 참고하시기 바랍니다.

## <a name="development-staging-and-production-environments"></a>개발, 스테이징 및 프로덕션 환경

Gulp를 스테이징 및 프로덕션에 대한 클라이언트 쪽 파일 최적화에 사용하면 처리된 파일이 로컬 스테이징 및 프로덕션 위치에 저장됩니다. *_Layout.cshtml* 파일은 **environment** 태그 도우미를 활용하여 두 가지 버전의 CSS 파일을 제공합니다. CSS 파일의 한 버전은 개발용이며 다른 버전은 스테이징 및 프로덕션 환경 모두를 위해 최적화되어 있습니다. Visual Studio 2017에서 **ASPNETCORE_ENVIRONMENT** 환경 변수를 `Production`으로 변경하면, Visual Studio가 웹 앱을 빌드하고 최소화된 CSS 파일을 참조합니다. 다음 태그는 `Development` CSS 파일과 축소된 `Staging, Production` CSS 파일에 대한 참조 태그를 포함하고 있는 **environment** 태그 도우미를 보여줍니다.

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

## <a name="switching-between-environments"></a>환경 전환하기

서로 다른 환경에 대한 컴파일로 전환하려면 **ASPNETCORE_ENVIRONMENT** 환경 변수의 값을 수정합니다.

1.  **작업 러너 탐색기**에서 **min** 작업이 **빌드 전**으로 설정되어 있는지 확인합니다.

2.  **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 버튼으로 클릭하고 **속성**을 선택합니다.

    그러면 웹 앱에 대한 속성 시트가 표시됩니다.

3.  **디버그** 탭을 클릭합니다.

4.  **ASPNETCORE_ENVIRONMENT** 환경 변수의 값을 `Production`으로 설정합니다.

5.  **F5** 키를 눌러서 응용 프로그램을 브라우저에서 실행합니다.

6.  브라우저 창에서 마우스 오른쪽 버튼으로 페이지를 클릭하고 **소스 보기**를 선택하여 페이지의 HTML을 살펴봅니다.

    스타일시트가 축소된 CSS 파일을 링크하고 있는지 확인합니다.

7.  브라우저를 닫아서 웹 앱을 중지합니다.

8.  Visual Studio에서 다시 웹 앱에 대한 속성 시트로 되돌아가서 **ASPNETCORE_ENVIRONMENT** 환경 변수의 값을 `Development`으로 재설정합니다.

9.  **F5** 키를 눌러서 다시 응용 프로그램을 브라우저에서 실행합니다.

10. 브라우저 창에서 마우스 오른쪽 버튼으로 페이지를 클릭하고 **소스 보기**를 선택하여 페이지의 HTML을 살펴봅니다.

    스타일시트가 축소되지 않은 버전의 CSS 파일을 링크하고 있는지 확인합니다.

ASP.NET Core의 환경에 관한 자세한 내용은 [여러 환경 사용하기](../fundamentals/environments.md)을 참고하시기 바랍니다.

## <a name="task-and-module-details"></a>작업 및 모듈 세부 정보

Gulp 작업은 함수 이름으로 등록됩니다. 다른 작업을 현재 작업보다 먼저 실행해야 할 경우 종속성을 지정할 수 있습니다. 추가적인 함수를 사용하면 Gulp 작업을 실행하고 모니터링 할 수 있을 뿐만 아니라 수정되는 파일의 원본(*src*)과 대상(*dest*)을 설정할 수도 있습니다. 다음은 기본적인 Gulp API 함수입니다.

|Gulp 함수|구문|설명|
|---   |--- |--- |
|task  |`gulp.task(name[, deps], fn) { }`|`task` 함수는 작업을 만듭니다. `name` 매개 변수는 작업의 이름을 정의합니다. `deps` 매개 변수에는 이 작업을 실행하기 전에 완료해야 할 작업의 배열을 담습니다. `fn` 매개 변수는 이 작업의 실제 작업을 수행하는 콜백 함수를 나타냅니다.|
|watch |`gulp.watch(glob [, opts], tasks) { }`|`watch` 함수는 파일을 모니터링하고 파일이 변경되면 작업을 실행합니다. `glob` 매개 변수는 모니터링 할 파일을 결정하는 `string` 또는 `array`입니다. `opts` 매개 변수는 추가적인 파일 모니터링 옵션을 제공합니다.|
|src   |`gulp.src(globs[, options]) { }`|`src` 함수는 glob 값과 일치하는 파일을 제공합니다. `glob` 매개 변수는 읽을 파일을 결정하는 `string` 또는 `array`입니다. `options` 매개 변수는 추가적인 파일 옵션을 제공합니다.|
|dest  |`gulp.dest(path[, options]) { }`|`dest` 함수는 파일을 쓸 수 있는 위치를 정의합니다. `path` 매개 변수는 대상 폴더를 결정하는 문자열 또는 함수입니다. `options` 매개 변수는 출력 폴더 옵션을 지정하는 개체입니다.|

추가적인 Gulp API 참조 정보는 [Gulp Docs API](https://github.com/gulpjs/gulp/blob/master/docs/API.md)를 참고하시기 바랍니다.

## <a name="gulp-recipes"></a>Gulp 레시피

Gulp 커뮤니티는 Gulp [레시피](https://github.com/gulpjs/gulp/blob/master/docs/recipes/README.md)를 제공합니다. 이러한 레시피는 일반적인 시나리오를 다루는 Gulp 작업으로 구성되어 있습니다.

## <a name="additional-resources"></a>추가 자료

* [Gulp 문서](https://github.com/gulpjs/gulp/blob/master/docs/README.md)
* [ASP.NET Core의 번들링 및 축소](bundling-and-minification.md)
* [ASP.NET Core에서 Grunt 사용하기](using-grunt.md)
