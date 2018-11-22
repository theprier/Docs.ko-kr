---
title: 번들 및 ASP.NET Core에서 정적 자산을 축소
author: scottaddie
description: 묶음 및 축소 기술을 적용 하 여 ASP.NET Core 웹 응용 프로그램에서 정적 리소스를 최적화 하는 방법에 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 11/20/2018
uid: client-side/bundling-and-minification
ms.openlocfilehash: 5d5f0aadb7740c9b2b959d12a585cd8c91758ce8
ms.sourcegitcommit: 4225e2c49a0081e6ac15acff673587201f54b4aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52282145"
---
# <a name="bundle-and-minify-static-assets-in-aspnet-core"></a>번들 및 ASP.NET Core에서 정적 자산을 축소

하 여 [Scott Addie](https://twitter.com/Scott_Addie) 고 [David 소나무](https://twitter.com/davidpine7)

이 문서에서는 묶음 및 축소, ASP.NET Core 웹 앱을 사용 하 여 이러한 기능을 사용할 수 있는 방법을 포함 하 여 적용 하는 이점에 설명 합니다.

## <a name="what-is-bundling-and-minification"></a>묶음 및 축소는 것이 무엇입니까

묶음 및 축소는 두 가지 고유한 성능 최적화가 웹 앱에 적용할 수 있습니다. 함께 사용 하는 묶음 및 축소 성능을 향상 시킬 요청된 된 정적 자산의 크기를 줄이고 서버 요청의 수를 줄입니다.

묶음 및 축소 주로 첫 번째 페이지 요청 로드 시간을 개선 합니다. 웹 페이지를 요청한 후 브라우저 (예: JavaScript, CSS 및 이미지) 정적 자산을 캐시 합니다. 따라서 묶음 및 축소 하지 때 성능을 향상 시킬 동일한 페이지 또는 동일한 자산을 요청 하는 동일한 사이트에서 페이지를 요청 합니다. 경우는 만료 헤더 자산에서 올바르게 설정 되지 않습니다 및 묶음 및 축소를 사용 하지 않는 경우 브라우저의 새로 고침 추론 표시 자산 부실 몇 일 후입니다. 또한 브라우저 각 자산에 대 한 유효성 검사는 요청이 필요 합니다. 이 경우 묶음 및 축소 첫 번째 페이지 요청 후에 성능 향상을 제공합니다.

### <a name="bundling"></a>번들

번들로 단일 파일에 여러 파일을 결합합니다. 번들로 웹 페이지와 같은 웹 자산을 렌더링 하는 데 필요한 서버 요청의 수를 줄입니다. CSS, JavaScript 등을 위해 특별히 개수에 관계 없이 개별 번들을 만들 수 있습니다. 더 적은 파일 서버로 브라우저 또는 응용 프로그램을 제공 하는 서비스에서 더 적은 수의 HTTP 요청을 의미 합니다. 이 결과에서 첫 번째 페이지 로드 성능이 향상 되었습니다.

### <a name="minification"></a>축소

축소 기능을 변경 하지 않고 코드에서 불필요 한 문자를 제거 합니다. 결과 요청 된 자산 (예: CSS, 이미지 및 JavaScript 파일)의 크기가 크게 감소 합니다. 축소의 일반적인 부작용 변수 이름의 문자 하나를 줄이는 등 주석 및 불필요 한 공백을 제거 합니다.

다음 JavaScript 함수를 살펴보세요.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.js)]

다음으로 함수를 축소 하는 축소:

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.min.js)]

주석 및 불필요 한 공백을 제거 하는 것 외에도 다음 매개 변수 및 변수 이름은 다음과 같이 바뀌었습니다.

원래 색 | 이름이 바뀜
--- | :---:
`imageTagAndImageID` | `t`
`imageContext` | `a`
`imageElement` | `r`

## <a name="impact-of-bundling-and-minification"></a>묶음 및 축소의 영향

다음 표에서 개별적으로 자산을 로드 하 고 묶음 및 축소를 사용 하 여 차이점을 설명 합니다.

작업 | B/M을 사용 하 여 | B/M 없이 | 변경
--- | :---: | :---: | :---:
파일 요청  | 7   | 18     | 157%
전송 (kb) | 156 | 264.68 | 70%
로드 시간 (ms) | 885 | 2360   | 167%

브라우저는 HTTP 요청 헤더와 관련 하 여 매우 자세한 정보. 총 바이트 수를 번들로 묶으면 메트릭을 본 상당히 감소 전송 합니다. 이 예제에서는 로컬로 실행 되지만 로드 시간 향상을 보여 줍니다. 큰 성능 향상은 묶음 및 축소를 사용 하 여 자산을 사용 하 여 네트워크를 통해 전송 될 때 실현 됩니다.

## <a name="choose-a-bundling-and-minification-strategy"></a>묶음 및 축소 전략 선택

MVC 및 Razor 페이지 프로젝트 템플릿을 묶음 및 축소 JSON 구성 파일의 구성에 대 한 기본 제공 솔루션을 제공 합니다. 와 같은 타사 도구를 [Gulp](xref:client-side/using-gulp) 하 고 [Grunt](xref:client-side/using-grunt) 실행 기 작업을 좀 더 많은 복잡성을 사용 하 여 동일한 작업을 수행 합니다. 개발 워크플로에서 처리 묶음 및 축소 초과 해야 하는 경우 타사 도구는 최적의 선택&mdash;lint 및 이미지 최적화와 같은 합니다. 디자인 타임 묶음 및 축소를 사용 하 여 앱의 배포 하기 전에 축소 된 파일이 생성 됩니다. 묶음 및 축소를 배포 하기 전에 서버 부하 감소의 이점이 제공 합니다. 그러나 해당 디자인 타임 묶음을 인식 해야 하 고 축소 빌드 복잡성 증가 정적 파일 에서만 작동 합니다.

## <a name="configure-bundling-and-minification"></a>묶음 및 축소 구성

::: moniker range="<= aspnetcore-2.0"

MVC 및 Razor 페이지 프로젝트 템플릿을 제공 하는 ASP.NET Core 2.0 또는 이전에 *bundleconfig.json* 각 번들에 대 한 옵션을 정의 하는 구성 파일:

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

ASP.NET Core 2.1 이상 버전에서는 명명 된 새 JSON 파일을 추가 *bundleconfig.json*, MVC 또는 Razor 페이지 프로젝트 루트에 있습니다. 시작 지점으로 해당 파일에 다음 JSON을 포함:

::: moniker-end

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig.json)]

합니다 *bundleconfig.json* 파일은 각 번들에 대 한 옵션을 정의 합니다. 앞의 예제는 단일 번들 구성 사용자 지정 JavaScript에 대 한 정의 됩니다 (*wwwroot/js/site.js*) 및 스타일 시트 (*wwwroot/css/site.css*) 파일입니다.

구성 옵션은 다음과 같습니다.

* `outputFileName`: 출력 번들 파일의 이름입니다. 상대 경로 포함할 수는 *bundleconfig.json* 파일입니다. **required**
* `inputFiles`: 배열 함께 번들로 제공할 파일입니다. 이들은 구성 파일에 상대 경로입니다. **선택적**, * 값이 비어 있으면 빈 출력 파일에 발생 합니다. [와일드 카드 사용](http://www.tldp.org/LDP/abs/html/globbingref.html) 패턴이 지원 됩니다.
* `minify`축소 옵션: 출력 형식입니다. **optional**, *default - `minify: { enabled: true }`*
  * 구성 옵션은 출력 파일 형식 당 사용할 수 있습니다.
    * [CSS Minifier입니다.](https://github.com/madskristensen/BundlerMinifier/wiki/cssminifier)
    * [JavaScript Minifier입니다.](https://github.com/madskristensen/BundlerMinifier/wiki/JavaScript-Minifier-settings)
    * [HTML Minifier입니다.](https://github.com/madskristensen/BundlerMinifier/wiki)
* `includeInProject`: 프로젝트 파일에 생성 된 파일을 추가할지 여부를 나타내는 플래그입니다. **optional**, *default - false*
* `sourceMap`: 해당 번들된 파일에 대 한 소스 맵을 생성할지 여부를 나타내는 플래그입니다. **optional**, *default - false*
* `sourceMapRootPath`: 생성 된 소스 맵 파일을 저장 하는 것에 대 한 루트 경로입니다.

## <a name="build-time-execution-of-bundling-and-minification"></a>묶음 및 축소의 빌드 시간 실행

합니다 [BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) 실행 묶음 및 축소 빌드 시 NuGet 패키지에 사용 하도록 설정 합니다. 패키지를 삽입 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets) 는 빌드 및 정리 시간에 실행 합니다. 합니다 *bundleconfig.json* 정의 된 구성에 따라 출력 파일을 생성 하는 빌드 프로세스에서 분석 하는 파일입니다.

> [!NOTE]
> BuildBundlerMinifier는 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다. 문제를 제출 해야 [여기](https://github.com/madskristensen/BundlerMinifier/issues)합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

추가 된 *BuildBundlerMinifier* 패키지를 프로젝트입니다.

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

추가 된 *BuildBundlerMinifier* 패키지를 프로젝트:

```console
dotnet add package BuildBundlerMinifier
```

ASP.NET을 사용 하는 경우 Core 1.x의 경우 새로 추가 된 패키지를 복원 합니다.

```console
dotnet restore
```

프로젝트를 빌드하십시오.

```console
dotnet build
```

다음 메시지가 나타납니다.

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

다음 출력이 표시됩니다.

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


  Bundler: Cleaning output from bundleconfig.json
  Bundler: Done cleaning output file from bundleconfig.json
```

---

## <a name="ad-hoc-execution-of-bundling-and-minification"></a>묶음 및 축소의 임시 실행

프로젝트를 빌드하지 않고 임시 단위로 묶음 및 축소 작업을 실행 하는 것이 가능 합니다. 추가 된 [BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet 패키지를 프로젝트:

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=10)]

> [!NOTE]
> BundlerMinifier.Core는 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다. 문제를 제출 해야 [여기](https://github.com/madskristensen/BundlerMinifier/issues)합니다.

이 패키지에 포함 하도록.NET Core CLI를 확장 합니다 *dotnet 번들* 도구입니다. 다음 명령은 패키지 관리자 콘솔 (PMC) 창 또는 명령 셸에서 실행할 수 있습니다.

```console
dotnet bundle
```

> [!IMPORTANT]
> NuGet 패키지 관리자와 *.csproj 파일에 종속성 추가 `<PackageReference />` 노드. 합니다 `dotnet bundle` 명령은.NET Core CLI와 함께 등록 되어 경우에만 `<DotNetCliToolReference />` 노드를 사용 합니다. *.Csproj 파일을 적절 하 게 수정 합니다.

## <a name="add-files-to-workflow"></a>워크플로 파일을 추가 합니다.

예를 살펴봅니다 추가 *custom.css* 다음과 같은 파일이 추가 됩니다.

[!code-css[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/css/custom.css)]

축소 하려면 *custom.css* 고 사용 하 여 번들 *site.css* 에 *site.min.css* 파일에 상대 경로 추가 합니다 *bundleconfig.json*:

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig2.json?highlight=6)]

> [!NOTE]
> 또는 다음 와일드 카드 사용 패턴을 사용할 수 있습니다.
>
> ```json
> "inputFiles": ["wwwroot/**/*(*.css|!(*.min.css))"]
> ```
>
> 모든 CSS 파일과 일치 하는 축소 된 파일 패턴을 제외 하는이 와일드 카드 사용 패턴입니다.

응용 프로그램을 빌드합니다. 오픈 *site.min.css* 의 내용을 확인 하 고 *custom.css* 파일의 끝에 추가 됩니다.

## <a name="environment-based-bundling-and-minification"></a>환경 기반 묶음 및 축소

모범 사례로, 프로덕션 환경에서 앱의 번들 및 축소 된 파일은을 사용 해야 합니다. 개발 하는 동안 원래 파일은 앱의 쉬운 디버깅에 대 한 확인 합니다.

사용 하 여 페이지에 포함할 파일을 지정 합니다 [환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) 보기에 있습니다. 특정에서 실행할 때만 해당 콘텐츠를 렌더링 환경 태그 도우미 [환경](xref:fundamentals/environments)합니다.

다음 `environment` 태그 실행 하는 경우 처리 되지 않은 CSS 파일을 렌더링 합니다 `Development` 환경:

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=21-24)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=9-12)]

::: moniker-end

다음 `environment` 이외의 환경에서 실행 하는 경우 태그 렌더링 묶이고 CSS 파일 `Development`합니다. 예를 들어에서 실행 중인 `Production` 또는 `Staging` 이러한 스타일 시트의 렌더링을 트리거합니다.

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=5&range=25-30)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=13-18)]

::: moniker-end

## <a name="consume-bundleconfigjson-from-gulp"></a>Gulp에서 bundleconfig.json 사용

앱의 묶음 및 축소 워크플로 추가 처리를 필요로 하는 경우가 있습니다. 이미지 최적화, 캐시 버스팅 및 CDN 자산 처리를 예로 들 수 있습니다. 이러한 요구 사항을 충족 하려면 묶음 및 축소 워크플로의 Gulp를 사용 하 여 변환할 수 있습니다.

### <a name="use-the-bundler--minifier-extension"></a>Bundler & Minifier 확장 사용

Visual Studio [Bundler & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) 확장 처리 Gulp로 변환 합니다.

> [!NOTE]
> Bundler & Minifier 확장 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다. 문제를 제출 해야 [여기](https://github.com/madskristensen/BundlerMinifier/issues)합니다.

마우스 오른쪽 단추로 클릭 합니다 *bundleconfig.json* 솔루션 탐색기에서 파일을 선택 **Bundler & Minifier** > **Gulp를 변환 하는 중...** :

![Gulp를 변환 상황에 맞는 메뉴 항목](../client-side/bundling-and-minification/_static/convert-to-gulp.png)

합니다 *gulpfile.js* 하 고 *package.json* 파일이 프로젝트에 추가 됩니다. 지원 [npm](https://www.npmjs.com/) 에 나열 된 패키지를 *package.json* 파일의 `devDependencies` 섹션 설치 됩니다.

전역 종속성으로 Gulp CLI를 설치 하려면 PMC 창에서 다음 명령을 실행 합니다.

```console
npm i -g gulp-cli
```

합니다 *gulpfile.js* 읽기 파일을 *bundleconfig.json* 입력, 출력 및 설정에 대 한 파일입니다.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-12&highlight=10)]

### <a name="convert-manually"></a>수동으로 변환

Visual Studio 및/또는 Bundler & Minifier 확장을 사용할 수 없는 경우 수동으로 변환 합니다.

추가 된 *package.json* 파일에 다음을 사용 하 여 `devDependencies`, 프로젝트 루트에:

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/package.json?range=5-13)]

동일한 수준에서 다음 명령을 실행 하 여 종속성을 설치 *package.json*:

```console
npm i
```

전역 종속성으로 Gulp CLI를 설치 합니다.

```console
npm i -g gulp-cli
```

복사 합니다 *gulpfile.js* 프로젝트 루트 아래의 파일:

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-11,14-)]

### <a name="run-gulp-tasks"></a>Gulp 작업 실행

Gulp 축소 작업 전에 Visual Studio에서 프로젝트 빌드를 트리거하려면 다음을 추가 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets) *.csproj 파일에:

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=14-16)]

이 예제에서는 모든 작업 내에서 정의 합니다 `MyPreCompileTarget` 대상 전에 미리 정의 된 실행 `Build` 대상입니다. Visual Studio의 출력 창에 다음과 유사한 출력이 표시 됩니다.

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

또는 Visual Studio의 특정 이벤트 Gulp 작업을 바인딩할 Visual Studio의 Task Runner 탐색기를 사용할 수 있습니다. 참조 [실행 중인 기본 작업](xref:client-side/using-gulp#running-default-tasks) 그에 대 한 지침은 합니다.

## <a name="additional-resources"></a>추가 자료

* [Gulp 사용](xref:client-side/using-gulp)
* [Grunt 사용](xref:client-side/using-grunt)
* [여러 환경 사용](xref:fundamentals/environments)
* [태그 도우미](xref:mvc/views/tag-helpers/intro)
