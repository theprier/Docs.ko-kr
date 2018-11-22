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
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a>ASP.NET Core와 Less, Sass 및 Font Awesome

작성자: [Steve Smith](https://ardalis.com/)

웹 응용 프로그램의 사용자는 스타일과 전반적인 경험에 대해 갈수록 더 많은 기대를 갖고 있습니다. 최신 웹 응용 프로그램은 모양 및 느낌을 일관적인 방식으로 정의하고 관리하기 위해 풍부한 도구와 프레임워크를 자주 활용합니다. [부트스트랩](http://getbootstrap.com/) 같은 프레임워크는 웹 사이트에 대한 공통 스타일 모음과 레이아웃 옵션을 정의하는데 매우 효과적입니다. 그러나 대부분의 중요한 사이트들은 스타일과 CSS 스타일시트 파일을 효과적으로 정의하고 관리할 수 있다는 점과 함께 사이트의 인터페이스를 보다 직관적으로 만들어주는 비이미지 아이콘에 쉽게 접근할 수 있는 장점도 얻을 수 있습니다. 바로 이 점이 [Less](http://lesscss.org/) 및 [Sass](http://sass-lang.com/)를 지원하는 언어와 도구, 그리고 [Font Awesome](http://fontawesome.io/) 같은 라이브러리가 필요한 이유입니다.

## <a name="css-preprocessor-languages"></a>CSS 전처리기 언어

기본 언어의 작업 경험을 개선하기 위해서 다른 언어로 컴파일되는 언어를 전처리기라고 합니다. CSS에는 Less와 Sass라는 두 가지 인기 있는 전처리기가 존재합니다. 이 전처리기들은 CSS에 변수 및 중첩된 규칙 같은 기능을 추가하여 크고 복잡한 스타일시트의 유지 관리를 향상시킵니다. 언어로서의 CSS는 매우 단순하기 때문에 변수처럼 간단한 기능조차 지원이 부족하며 이는 CSS 파일을 반복적이고 비대하게 만듭니다. 전처리기를 통해서 실제 프로그래밍 언어의 기능을 추가하면 중복을 줄이고 스타일 규칙을 보다 효과적으로 구성할 수 있습니다. Visual Studio는 Less 및 Sass 둘 모두에 대한 기본 제공을 비롯해서 이런 언어로 작업할 때 개발 환경을 더욱 개선할 수 있는 확장을 제공합니다.

전처리기가 스타일 정보의 가독성과 유지 관리를 향상시키는 방법에 대한 간단한 예제로 다음 CSS를 살펴보시기 바랍니다.

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

Less를 사용하면 *믹스인*(속성을 한 클래스나 규칙 집합에서 다른 클래스나 규칙 집합에 '섞을' 수 있기 때문에 이런 이름이 붙여짐)을 사용해서 모든 중복을 제거하도록 이를 다시 작성할 수 있습니다.

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

## <a name="less"></a>Less

Less CSS 전처리기는 Node.js를 통해서 실행됩니다. Less를 설치하려면 명령 프롬프트에서 노드 패키지 관리자(npm)를 사용합니다 (-g는 '전역'을 의미합니다).

```console
npm install -g less
```

Visual Studio를 사용하는 경우, 프로젝트에 하나 이상의 Less 파일을 추가한 다음, 컴파일 시에 이를 처리하도록 Gulp를 (또는 Grunt를) 구성하여 Less를 시작할 수 있습니다. 프로젝트에 *Styles* 폴더를 추가한 다음, 이 폴더에 *main.less*라는 이름으로 새로운 Less 파일을 추가합니다.

![Less 파일 추가하기](less-sass-fa/_static/add-less-file.png)

파일이 추가된 폴더의 구조는 다음과 같아야 합니다.

![폴더 구조](less-sass-fa/_static/folder-structure.png)

이제 이 파일에 몇 가지 기본 스타일을 추가할 수 있으며, 이는 Gulp에 의해 CSS로 컴파일되어 wwwroot 폴더에 배포됩니다.

다음 내용을 포함하도록 *main.less*를 수정해서 단일 기본 색상으로부터 간단한 색상표를 만듭니다.

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

`@base`와 @가 접두사로 붙은 다른 항목들은 변수입니다. 각각은 색상을 나타냅니다. `@base`를 제외한 변수들은 lighten, darken 및 spin 같은 색상 함수를 이용해서 설정됩니다. lighten 및 darken 함수는 사용자가 예상하는 것처럼 동작하고, spin 함수는 색의 색조를 색상환을 따라 돌면서 각도로 조정합니다. Less 프로세서는 사용하지 않는 변수를 무시할 만큼 똑똑하기 때문에 이 변수들의 동작 방식을 살펴보려면 변수를 어딘가에 사용해야만 합니다. `.baseColor` 클래스 등은 생성된 CSS 파일에서 각 변수들의 계산된 값을 보여줍니다.

### <a name="get-started"></a>시작하기

프로젝트 폴더에 **npm 구성 파일**(*package.json*)을 만들고 이 파일이 `gulp` 및 `gulp-less`를 참조하도록 편집합니다.

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

프로젝트 폴더의 명령 프롬프트나 Visual Studio의 **솔루션 탐색기**에서 종속성을 설치합니다(**종속성 > npm > 패키지 복원**).

```console
npm install
```

![VS 패키지 복원](less-sass-fa/_static/restore-packages.png)

프로젝트 폴더에 **Gulp 구성 파일**(*gulpfile.js*)을 만들고 자동화된 프로세스를 정의합니다. 파일의 맨 위에 Less를 나타내는 변수를 추가하고 Less를 실행하기 위한 작업을 추가합니다.

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

**작업 러너 탐색기**를 엽니다(**보기 > 다른 창 > 작업 러너 탐색기**). 작업 중에 `less`라는 새 작업이 표시되어야 합니다. 창을 새로 고침해야 할 수도 있습니다.

`less` 작업을 실행하면 다음과 비슷한 출력이 표시될 것입니다.

![less 작업 러너](less-sass-fa/_static/less-task-runner.png)

이제 *wwwroot/css* 폴더에 *main.css*라는 새 파일이 들어 있습니다.

![생성된 main css](less-sass-fa/_static/main-css-created.png)

*main.css*를 열어보면 다음과 같은 내용을 확인할 수 있습니다.

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

간단한 HTML 페이지를 *wwwroot* 폴더에 추가하고 *main.css*를 참조하여 실제 색상표를 확인합니다.

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

`@base`를 180도 회전하여 `@background`를 생성한 결과로 색상환에서 `@base`의 반대색이 만들어진 것을 확인할 수 있습니다.

![Less 테스트 예제](less-sass-fa/_static/less-test-screenshot.png)

Less는 중첩된 미디어 쿼리뿐만 아니라 중첩된 규칙에 대한 지원도 제공합니다. 예를 들어 메뉴 같은 중첩된 계층 구조를 정의하다 보면 다음과 같이 장황한 CSS 규칙이 만들어질 수 있습니다.

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

이상적으로 관련된 모든 스타일 규칙이 CSS 파일 내에 함께 존재하지만, 실제로 규약을 제외하고는 이 규칙을 강제하는 것은 아무 것도 없으며 아마도 주석을 작성할 것입니다.

Less를 사용하여 동일한 규칙을 정의하면 다음과 같습니다.

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

이 경우 `nav`의 모든 하위 요소가 해당 범위에 포함된다는 점에 유의하시기 바랍니다. 더 이상 부모 요소(`nav`, `li`, `a`)들이 반복되지 않으며, 전체 줄 수도 감소했습니다(그 중 일부는 두 번째 예제에서 동일한 줄에 값을 넣은 결과이기도 합니다). 명시적으로 지정된 범위내에서 해당 UI 요소에 대한 모든 규칙을 살펴보는 것이 조직적으로 매우 유용할 수 있으며, 이 경우 파일의 나머지 부분에서 중괄호를 사용하여 설정합니다.

`&` 구문은 Less의 선택자 기능으로, &를 지정하면 현재 선택자의 부모를 의미합니다. 따라서 {...} 블록 내에서 `&`는 `a` 태그를 나타내므로 `&:link`는 `a:link`와 같습니다.

반응형 디자인을 만드는데 매우 유용한 미디어 쿼리는 CSS의 반복과 복잡성의 큰 원인이기도 합니다. Less를 사용하면 클래스 내 미디어 쿼리를 중첩시킬 수 있으므로, 전체 클래스 정의를 다른 최상위 `@media` 요소 내에서 반복할 필요가 없습니다. 예를 들어 반응형 메뉴의 CSS는 다음과 같습니다.

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

이를 Less로 다음과 같이 더 잘 정의할 수 있습니다.

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

이미 살펴본 Less의 또 다른 기능은 미리 정의된 변수로 스타일의 속성을 구성할 수 있는 수학적 연산에 대한 지원입니다. 이 기능을 사용하면 기본 변수만 수정해도 모든 종속 값들이 자동으로 변경되므로 관련된 스타일을 훨씬 쉽게 수정할 수 있습니다.

CSS 파일은 특히 대규모 사이트의 경우 (그리고 특히 미디어 쿼리가 사용되는 경우) 시간이 지남에 따라 상당히 커지는 경향이 있어서 작업하기가 어렵습니다. Less 파일을 별도로 정의한 다음 `@import` 지시문을 사용하여 함께 가져올 수 있습니다. 필요한 경우 Less는 개별 CSS 파일을 가져오기 위해서도 사용할 수 있습니다.

*믹스인*은 매개 변수를 전달받을 수 있으며, Less는 특정 믹스인이 언제 효력이 발생하는지를 정의하기 위한 선언적 방법을 제공하는 믹스인 가드의 형태로 조건부 논리를 지원합니다. 믹스인 가드의 일반적인 용도는 원본 색이 얼마나 밝거나 어두운지에 따라 색을 조정하는 것입니다. 색에 대한 매개 변수를 전달받는 믹스인이 주어지면 믹스인 가드를 사용하여 해당 색을 기반으로 믹스인을 수정할 수 있습니다.

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

현재 `@base` 값인 `#663333`을 고려해 볼 때, 이 Less 스크립트는 다음과 같은 CSS를 생성합니다.

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

Less는 다양한 추가적인 기능들을 제공하며, 지금까지 살펴본 예제들은 이 전처리기 언어를 향상하기 위해 일부 아이디어를 제공할 것입니다.

## <a name="sass"></a>Sass

Sass는 Less와 비슷하며 많은 동일한 기능을 지원하지만 구문이 조금 다릅니다. JavaScript 대신 Ruby를 사용해서 만들어졌기 때문에 설치 요구 사항이 다릅니다. 원래의 Sass 언어는 중괄호 또는 세미콜론을 사용하지 않으며, 대신 공백 및 들여쓰기를 사용해서 범위를 정의했습니다. Sass 버전 3에서는 새로운 구문인 **SCSS**("Sassy CSS")가 도입되었습니다. SCSS는 들여쓰기 수준과 공백을 무시하고 대신 세미콜론과 중괄호를 사용한다는 점에서 CSS와 비슷합니다.

일반적으로 Sass를 설치하려면 먼저 Ruby를 설치한 다음(MacOS에는 사전 설치되어 있음), 다음 명령을 실행합니다.

```console
gem install sass
```

그러나 Visual Studio를 실행하고 있다면 Less와 거의 동일한 방식으로 Sass를 시작할 수 있습니다. *package.json*을 열고 "gulp-sass" 패키지를 `devDependencies`에 추가합니다.

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

다음으로 *gulpfile.js*를 수정하여 sass 변수와 작업을 추가해서 Sass 파일을 컴파일하고 결과를 wwwroot 폴더에 저장합니다.

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

이제 *main2.scss*라는 Sass 파일을 프로젝트 루트의 *Styles* 폴더에 추가할 수 있습니다.

![scss 파일 추가하기](less-sass-fa/_static/add-scss-file.png)

*main2.scss*를 열고 다음 내용을 추가합니다.

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

모든 파일을 저장합니다. 이제 **작업 러너 탐색기**를 새로 고쳐보면 `sass` 작업이 나타날 것입니다. 이 작업을 실행하고 */wwwroot/css* 폴더를 살펴보시기 바랍니다. 이제 다음 내용이 포함된 main2.css 파일이 존재할 것입니다.

```css
body {
    background-color: #CC0000;
}
```

Sass는 Less를 사용할 때와 비슷한 방식으로 중첩을 지원하므로 유사한 이점을 제공합니다. 파일은 함수로 나눌 수 있으며 `@import` 지시문을 사용해서 포함시킬 수 있습니다.

```sass
@import 'anotherfile';
```

Sass는 믹스인도 지원하며, 다음 [sass-lang.com](http://sass-lang.com)의 예제처럼 `@mixin` 키워드를 사용하여 정의하고 `@include`를 사용하여 포함시킵니다.

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

믹스인 외에도 Sass는 상속의 개념을 지원하므로 한 클래스가 다른 클래스를 확장할 수 있습니다. 개념적으로는 믹스인과 비슷하지만 CSS 코드가 적습니다. 이 기능은 `@extend` 키워드를 사용하여 수행됩니다. 믹스인을 시험해보려면 *main2.scss* 파일에 다음 내용을 추가합니다.

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

**작업 러너 탐색기**에서 `sass` 작업을 실행한 다음, *main2.css*의 출력을 확인해봅니다.

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

경고 믹스인의 모든 공통 속성들이 각 클래스에서 반복된다는 점에 유의하시기 바랍니다. 믹스인은 개발 시 중복 제거에 많은 도움을 주지만 여전히 많은 중복이 존재하는 CSS를 생성하여 필요한 CSS 파일보다 큰, 잠재적 성능 문제를 갖고 있는 파일이 만들어졌습니다.

이제 alert 믹스인을 `.alert` 클래스로 대체하고 `@include`를 `@extend`로 변경합니다(`alert`이 아니라 `.alert`을 확장해야 한다는 점이 중요).

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

Sass를 다시 실행하고 결과 CSS를 확인해봅니다.

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

이제 필요한 횟수만큼만 속성이 정의되며 더 나은 CSS가 생성됩니다.

Sass는 Less와 유사한 함수 및 조건부 논리 연산도 포함하고 있습니다. 사실 두 언어의 기능은 매우 유사합니다.

## <a name="less-or-sass"></a>Less 또는 Sass?

Less나 Sass를 사용하는 것이 일반적으로 더 나은지 여부에 대해서는 (또는 Sass 내에서 원래의 Sass 또는 최신 SCSS 구문을 선호할지 여부에 대해서도) 여전히 일치된 의견이 없습니다. 아마도 가장 중요한 결정은 CSS 파일을 손으로 코딩하는 대신 **이런 도구 중 하나를 사용하는 것**입니다. 일단 결정을 하고 나면 Less와 Sass 모두 좋은 선택입니다.

## <a name="font-awesome"></a>Font Awesome

CSS 전처리기와 더불어 최신 웹 응용 프로그램의 스타일 지정에 유용한 또 다른 리소스는 Font Awesome입니다. Font Awesome은 웹 응용 프로그램에서 자유롭게 사용할 수 있는 500개 이상의 확대 및 축소 가능한 벡터 아이콘을 제공하는 도구 키트입니다. 본래 부트스트랩과 함께 사용하도록 설계되었지만 해당 프레임워크나 어떠한 JavaScript 라이브러리에도 종속성이 없습니다.

Font Awesome을 시작하는 가장 쉬운 방법은 공용 콘텐츠 배달 네트워크(CDN) 위치를 사용하여 Font Awesome에 대한 참조를 추가하는 것입니다.

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

또는 *bower.json*의 "dependencies"에 이를 추가해서 Visual Studio 프로젝트에 추가할 수도 있습니다.

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

페이지에 Font Awesome에 대한 참조를 추가하고 나면 일반적으로 접두사가 'fa-'인 Font Awesome 클래스를 인라인 HTML 요소(예: `<span>` 또는 `<i>`)dp 적용하여 응용 프로그램에 아이콘을 추가할 수 있습니다. 예를 들어, 다음과 같은 코드를 사용하여 간단한 목록 및 메뉴에 아이콘을 추가할 수 있습니다.

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

이 코드는 브라우저에서 다음과 같은 화면을 만들게 됩니다. 각 항목 옆의 아이콘에 주목하시기 바랍니다.

![목록 아이콘](less-sass-fa/_static/list-icons-screenshot.png)

다음에서 사용 가능한 아이콘의 전체 목록을 볼 수 있습니다.

http://fontawesome.io/icons/

## <a name="summary"></a>요약

최신 웹 응용 프로그램은 다양한 장치에서 점점 더 깔끔하고 직관적이며 사용하기 쉬운 반응형의 유연한 디자인을 요구합니다. 이런 목표를 달성하기 위해 필요한 CSS 스타일시트의 복잡성 관리는 Less 또는 Sass 같은 전처리기를 사용하는 것이 가장 좋습니다. 또한 Font Awesome 같은 도구 키트는 텍스트 기반의 탐색 메뉴 및 버튼에 친숙한 아이콘을 신속하게 제공하여 응용 프로그램의 전반적인 사용자 경험을 향상시킵니다.
