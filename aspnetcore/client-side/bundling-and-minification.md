---
title: ASP.NET Core에서 번들 및 minifiy 정적 자산
author: scottaddie
description: 묶음 및 축소 기술을 적용 하 여 ASP.NET Core 웹 응용 프로그램에서 정적 리소스를 최적화 하는 방법에 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 01/10/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: client-side/bundling-and-minification
ms.openlocfilehash: a155422c0fd638f46fe4a9d8a77faebc0b2a5681
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="bundle-and-minifiy-static-assets-in-aspnet-core"></a>ASP.NET Core에서 번들 및 minifiy 정적 자산

작성자: [Scott Addie](https://twitter.com/Scott_Addie)

이 문서는 이점과 묶음 및 축소, ASP.NET Core 웹 앱과 이러한 기능은 사용할 수 있는 방법을 포함 하 여 설명 합니다.

## <a name="what-is-bundling-and-minification"></a>묶음 및 축소는 무엇입니까?

묶음 및 축소는 두 가지 고유한 성능 최적화가 웹 응용 프로그램에 적용할 수 있습니다. 함께 사용할 묶음 및 축소 성능을 향상 시킬 서버 요청 수를 줄이면 및 정적 요청 된 자산의 크기를 줄이십시오.

묶음 및 축소는 주로 첫 번째 페이지 요청 부하 시간을 개선 합니다. 웹 페이지를 요청 되 면 브라우저 정적 자산 (JavaScript, CSS 및 이미지)를 캐시 합니다. 따라서 묶음 및 축소 하지 때 성능을 향상 시킬 동일한 페이지 또는 같은 자산을 요청 하는 동일한 사이트에서 페이지를 요청 합니다. 경우는 만료 된 헤더는 자산에 올바르게 설정 되지 않았습니다 고 묶음 및 축소 사용 하지 않을 경우 브라우저의 새로 고침 추론 표시 자산 부실 몇 일 후 합니다. 또한 브라우저 각 자산에 대 한 유효성 검사 요청을 해야 합니다. 이 경우 묶음 및 축소 첫 번째 페이지 요청 후에 뛰어난 성능을 제공합니다.

### <a name="bundling"></a>번들

번들로 단일 파일에 여러 파일을 결합합니다. 번들 웹 페이지 등의 웹 자산을 렌더링 하는 데 필요한 서버 요청의 수를 줄입니다. CSS, JavaScript 등을 위해 특별히 개수에 관계 없이 개별 번들을 만들 수 있습니다. 적은 파일 서버에 대 한 브라우저 또는 응용 프로그램을 제공 하는 서비스에서 더 적은 수의 HTTP 요청을 의미 합니다. 이 결과에서 첫 번째 페이지 부하 성능이 향상 되었습니다.

### <a name="minification"></a>축소

축소 기능을 변경 하지 않고 코드에서 불필요 한 문자를 제거 합니다. 결과 요청 된 자산 (예: CSS, 이미지 및 JavaScript 파일)의 크기가 크게 감소 합니다. 축소의 일반적인 부작용에는 한 문자를 변수 이름을 단축 및 주석과 불필요 한 공백이 제거 포함 됩니다.

다음 JavaScript 함수가 있다고 합시다.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.js)]

다음으로 함수를 축소 하는 축소:

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.min.js)]

주석 및 불필요 한 공백을 제거 하는 것 외에도 다음 매개 변수 및 변수 이름 열의 이름을 다음과 같습니다.

원래 색 | 이름이 바뀜
--- | :---:
`imageTagAndImageID` | `t`
`imageContext` | `a`
`imageElement` | `r`

## <a name="impact-of-bundling-and-minification"></a>묶음 및 축소의 영향

다음 표에서 개별적으로 자산을 로드 하 고 묶음 및 축소를 사용 하 여 차이점을 설명 합니다.

작업 | M B/으로 | M B/없이 | 변경
--- | :---: | :---: | :---:
파일 요청  | 7   | 18     | 157%
전송 KB | 156 | 264.68 | 70%
로드 시간 (밀리초) | 885 | 2360   | 167%

브라우저는 HTTP 요청 헤더와 관련 하 여 매우 자세한 정보를 표시 합니다. 총 바이트 메트릭을 보여 준다는 사실을 알았습니다을 크게 절감 번들로 묶으면 전송 합니다. 이 예에서는 로컬로 실행 되지만 로드 시간이 크게 향상을 보여 줍니다. 큰 성능 향상은 자산 묶음 및 축소를 사용 하 여 네트워크를 통해 전송 될 때 실현 됩니다.

## <a name="choose-a-bundling-and-minification-strategy"></a>묶음 및 축소 전략 선택

MVC 및 Razor 페이지 프로젝트 템플릿은 묶음 및 축소는 JSON 구성 파일의 구성에 대 한 기본적으로 솔루션을 제공 합니다. 와 같은 타사 도구는 [Gulp](xref:client-side/using-gulp) 및 [Grunt](xref:client-side/using-grunt) runner 작업을 좀 더 복잡 한와 동일한 작업을 수행 합니다. 개발 워크플로에 묶음 및 축소 이외의 처리가 필요한 경우에 타사 도구는 갖추고&mdash;linting 및 이미지 최적화 합니다. 디자인 타임 묶음 및 축소를 사용 하 여 응용 프로그램의 배포 하기 전에 축소 된 파일이 생성 됩니다. 묶음 및 축소 배포 하기 전에 서버 부하 감소의 이점이 있습니다. 그러나 해당 디자인 타임 번들로 인식 해야 하 고 축소 빌드 복잡성을 증가 하 고 정적 파일 에서만 작동 합니다.

## <a name="configure-bundling-and-minification"></a>묶음 및 축소 구성

MVC 및 Razor 페이지 프로젝트 템플릿에 *bundleconfig.json* 구성 파일을 각 번들에 대 한 옵션을 정의 합니다. 기본적으로 단일 번들 구성 사용자 지정 JavaScript에 대 한 정의 (*wwwroot/js/site.js*) 및 스타일 시트 (*wwwroot/css/site.css*) 파일:

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig.json)]

구성 옵션은 다음과 같습니다.

* `outputFileName`: 출력 번들 파일의 이름입니다. 상대 경로 포함할 수 있습니다는 *bundleconfig.json* 파일입니다. **required**
* `inputFiles`: 함께 번들로 묶는 파일의 배열입니다. 이들은 구성 파일에 상대 경로입니다. **선택적**, * 빈 출력 파일에 빈 값이 발생 합니다. [와일드 카드 사용](http://www.tldp.org/LDP/abs/html/globbingref.html) 패턴이 지원 됩니다.
* `minify`: 출력 형식에 대 한 축소 옵션입니다. **optional**, *default - `minify: { enabled: true }`*
  * 구성 옵션은 출력 파일 형식을 사용할 수 있습니다.
    * [CSS Minifier입니다.](https://github.com/madskristensen/BundlerMinifier/wiki/cssminifier)
    * [JavaScript Minifier입니다.](https://github.com/madskristensen/BundlerMinifier/wiki/JavaScript-Minifier-settings)
    * [HTML Minifier입니다.](https://github.com/madskristensen/BundlerMinifier/wiki)
* `includeInProject`: 프로젝트 파일을 생성 된 파일을 추가할 것인지를 나타내는 플래그입니다. **optional**, *default - false*
* `sourceMap`: 해당 번들된 파일에 대 한 소스 맵을 생성 여부를 나타내는 플래그입니다. **optional**, *default - false*
* `sourceMapRootPath`생성 된 소스 맵 파일을 저장 하기 위한: 루트 경로입니다.

## <a name="build-time-execution-of-bundling-and-minification"></a>빌드 타임 실행 묶음 및 축소

[BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) 번들로 실행 및 축소 빌드 시 NuGet 패키지에 사용 하도록 설정 합니다. 패키지를 삽입 합니다. [MSBuild 대상](/visualstudio/msbuild/msbuild-targets) 를 빌드 및 정리 시간에 실행 합니다. *bundleconfig.json* 파일 정의 된 구성에 따라 출력 파일을 생성 하는 빌드 프로세스에 의해 분석 됩니다.

> [!NOTE]
> BuildBundlerMinifier는 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속해 있습니다. 문제를 제출 해야 [여기](https://github.com/madskristensen/BundlerMinifier/issues)합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

추가 *BuildBundlerMinifier* 프로젝트에 패키지 합니다.

프로젝트를 빌드합니다. 다음이 출력 창에 나타납니다.

```console
1>------ Build started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Begin processing bundleconfig.json
1>  Minified wwwroot/css/site.min.css
1>  Minified wwwroot/js/site.min.js
1>Bundler: Done processing bundleconfig.json
1>BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

프로젝트를 정리 합니다. 다음이 출력 창에 나타납니다.

```console
1>------ Clean started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Cleaning output from bundleconfig.json
1>Bundler: Done cleaning output file from bundleconfig.json
========== Clean: 1 succeeded, 0 failed, 0 skipped ==========
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli) 

추가 *BuildBundlerMinifier* 패키지를 프로젝트:

```console
dotnet add package BuildBundlerMinifier
```

ASP.NET을 사용 하는 경우 1.x 핵심 새로 추가 된 패키지를 복원 하십시오.

```console
dotnet restore
```

프로젝트를 빌드하십시오.

```console
dotnet build
```

다음이 나타납니다.

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


    Bundler: Begin processing bundleconfig.json
    Bundler: Done processing bundleconfig.json
    BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
```

프로젝트를 정리 합니다.

```console
dotnet clean
```

다음과 같은 출력이 표시 됩니다.

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


  Bundler: Cleaning output from bundleconfig.json
  Bundler: Done cleaning output file from bundleconfig.json
```

---

## <a name="ad-hoc-execution-of-bundling-and-minification"></a>묶음 및 축소의 임시 실행

프로젝트를 작성 하지 않고 임시 트랜잭션이란에 묶음 및 축소 작업을 실행 하려면 것 같습니다. 추가 [BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet 패키지를 프로젝트:

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=10)]

> [!NOTE]
> BundlerMinifier.Core는 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속해 있습니다. 문제를 제출 해야 [여기](https://github.com/madskristensen/BundlerMinifier/issues)합니다.

.NET Core CLI 포함 하도록 확장 하는이 패키지는 *dotnet 번들* 도구입니다. 패키지 관리자 콘솔 (PMC) 창이 나 명령 셸에서 다음 명령을 실행할 수 있습니다.

```console
dotnet bundle
```

> [!IMPORTANT]
> 종속성으로 *.csproj 파일에 추가 하는 NuGet 패키지 관리자 `<PackageReference />` 노드. `dotnet bundle` 명령에 등록 된.NET Core CLI 경우에만 `<DotNetCliToolReference />` 노드를 사용 합니다. *.Csproj 파일을 적절 하 게 수정 합니다.

## <a name="add-files-to-workflow"></a>워크플로에 파일 추가

예제를 고려해 보세요 추가 *custom.css* 다음과 같은 파일이 추가 됩니다.

[!code-css[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/css/custom.css)]

축소할 *custom.css* 하 고 사용 하 여 제공할 *site.css* 에 *site.min.css* 파일, 상대 경로를 추가할 *bundleconfig.json*:

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig2.json?highlight=6)]

> [!NOTE]
> 또는 와일드 카드 사용 패턴을 사용할 수 없습니다.
>
> ```json
> "inputFiles": ["wwwroot/**/*(*.css|!(*.min.css)"]
> ```
>
> 이 와일드 카드 사용 패턴 일치 하는 모든 CSS 파일에 축소 된 파일 패턴을 제외 합니다.

응용 프로그램을 빌드합니다. 열기 *site.min.css* 내외의 내용을 *custom.css* 파일의 끝에 추가 됩니다.

## <a name="environment-based-bundling-and-minification"></a>환경 기반 묶음 및 축소

모범 사례로, 프로덕션 환경에서 앱의 번들로 묶은 및 축소 된 파일을 사용 해야 합니다. 개발 하는 동안 원본 파일 보다 쉽게 디버그 하려면 앱에 대 한 확인 하십시오.

사용 하 여 페이지에 포함할 파일을 지정 된 [환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) 보기에 있습니다. 특정에서 실행 될 때만 해당 콘텐츠를 렌더링 환경 태그 도우미 [환경](xref:fundamentals/environments)합니다.

다음 `environment` 태그에서 실행할 때 처리 되지 않은 CSS 파일을 렌더링 된 `Development` 환경:

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=21-24)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=9-12)]

* * *
다음 `environment` 이외의 환경에서 실행 하는 경우 태그 렌더링 번들 및 축소 된 CSS 파일 `Development`합니다. 예를 들어에서 실행 `Production` 또는 `Staging` 이러한 스타일 시트의 렌더링을 트리거합니다.

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=5&range=25-30)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=13-18)]

* * *
## <a name="consume-bundleconfigjson-from-gulp"></a>Bundleconfig.json Gulp에서 사용 합니다.

묶음 및 축소 워크플로 응용 프로그램의 추가 처리를 필요로 하는 경우가 있습니다. 이미지 최적화, 캐시 busting 및 CDN 자산 처리를 예로 들 수 있습니다. 이러한 요구를 충족 하기 위해 묶음 및 축소 워크플로 Gulp를 사용 하도록 변환할 수 있습니다.

### <a name="use-the-bundler--minifier-extension"></a>번들러 & Minifier 확장을 사용 하 여

Visual Studio [번들러 & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) 확장 처리 Gulp로 변환 합니다.

> [!NOTE]
> 번들러 & Minifier 확장을 Microsoft 지원을 제공 하지는 GitHub의 커뮤니티 기반 프로젝트에 속해 있습니다. 문제를 제출 해야 [여기](https://github.com/madskristensen/BundlerMinifier/issues)합니다.

마우스 오른쪽 단추로 클릭는 *bundleconfig.json* 솔루션 탐색기에서 파일을 선택 **번들러 & Minifier** > **Gulp 변환...** :

![상황에 맞는 메뉴 항목 Gulp 변환](../client-side/bundling-and-minification/_static/convert-to-gulp.png)

*gulpfile.js* 및 *package.json* 파일이 프로젝트에 추가 됩니다. 지 원하는 [npm](https://www.npmjs.com/) 에 나열 된 패키지는 *package.json* 파일의 `devDependencies` 섹션 설치 됩니다.

전역 종속성으로 Gulp CLI를 설치 하려면 PMC 창에서 다음 명령을 실행 합니다.

```console
npm i -g gulp-cli
```

*gulpfile.js* 파일 읽기는 *bundleconfig.json* 입력, 출력 및 설정에 대 한 파일입니다.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-12&highlight=10)]

### <a name="convert-manually"></a>수동으로 변환

Visual Studio 및/또는 번들러 & Minifier 확장을 사용할 수 없는 경우 수동으로 변환 합니다.

추가 *package.json* 파일을 다음으로 `devDependencies`, 프로젝트 루트에:

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/package.json?range=5-13)]

와 같은 수준에서 다음 명령을 실행 하 여 종속성을 설치 *package.json*:

```console
npm i
```

전역 종속성으로 Gulp CLI를 설치 합니다.

```console
npm i -g gulp-cli
```

복사는 *gulpfile.js* 프로젝트 루트 아래의 파일:

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-11,14-)]

### <a name="run-gulp-tasks"></a>Gulp 작업 실행된

Gulp 축소 작업을 트리거하는 Visual Studio에서 프로젝트를 구성 하기 전에, 다음 추가 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets) *.csproj 파일에:

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=14-16)]

이 예제에서는 모든 작업 내에서 정의 `MyPreCompileTarget` 전에 미리 정의 된 실행 대상 `Build` 대상입니다. Visual Studio의 출력 창에 다음과 비슷한 출력이 나타납니다.

```console
1>------ Build started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
1>[14:17:49] Using gulpfile C:\BuildBundlerMinifierApp\gulpfile.js
1>[14:17:49] Starting 'min:js'...
1>[14:17:49] Starting 'min:css'...
1>[14:17:49] Starting 'min:html'...
1>[14:17:49] Finished 'min:js' after 83 ms
1>[14:17:49] Finished 'min:css' after 88 ms
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

또는 Visual Studio의 Task Runner 탐색기 Gulp 작업을 특정 Visual Studio 이벤트에 바인딩 데 사용할 수 있습니다. 참조 [기본 작업을 실행](xref:client-side/using-gulp#running-default-tasks) 것에 대 한 지침은 합니다.

## <a name="additional-resources"></a>추가 자료

* [Gulp 사용](xref:client-side/using-gulp)
* [Grunt 사용](xref:client-side/using-grunt)
* [여러 환경 사용](xref:fundamentals/environments)
* [태그 도우미](xref:mvc/views/tag-helpers/intro)
