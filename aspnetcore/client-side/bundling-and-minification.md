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
# <a name="bundle-and-minify-static-assets-in-aspnet-core"></a><span data-ttu-id="88fc4-103">번들 및 ASP.NET Core에서 정적 자산을 축소</span><span class="sxs-lookup"><span data-stu-id="88fc4-103">Bundle and minify static assets in ASP.NET Core</span></span>

<span data-ttu-id="88fc4-104">하 여 [Scott Addie](https://twitter.com/Scott_Addie) 고 [David 소나무](https://twitter.com/davidpine7)</span><span class="sxs-lookup"><span data-stu-id="88fc4-104">By [Scott Addie](https://twitter.com/Scott_Addie) and [David Pine](https://twitter.com/davidpine7)</span></span>

<span data-ttu-id="88fc4-105">이 문서에서는 묶음 및 축소, ASP.NET Core 웹 앱을 사용 하 여 이러한 기능을 사용할 수 있는 방법을 포함 하 여 적용 하는 이점에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-105">This article explains the benefits of applying bundling and minification, including how these features can be used with ASP.NET Core web apps.</span></span>

## <a name="what-is-bundling-and-minification"></a><span data-ttu-id="88fc4-106">묶음 및 축소는 것이 무엇입니까</span><span class="sxs-lookup"><span data-stu-id="88fc4-106">What is bundling and minification</span></span>

<span data-ttu-id="88fc4-107">묶음 및 축소는 두 가지 고유한 성능 최적화가 웹 앱에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-107">Bundling and minification are two distinct performance optimizations you can apply in a web app.</span></span> <span data-ttu-id="88fc4-108">함께 사용 하는 묶음 및 축소 성능을 향상 시킬 요청된 된 정적 자산의 크기를 줄이고 서버 요청의 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-108">Used together, bundling and minification improve performance by reducing the number of server requests and reducing the size of the requested static assets.</span></span>

<span data-ttu-id="88fc4-109">묶음 및 축소 주로 첫 번째 페이지 요청 로드 시간을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-109">Bundling and minification primarily improve the first page request load time.</span></span> <span data-ttu-id="88fc4-110">웹 페이지를 요청한 후 브라우저 (예: JavaScript, CSS 및 이미지) 정적 자산을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-110">Once a web page has been requested, the browser caches the static assets (JavaScript, CSS, and images).</span></span> <span data-ttu-id="88fc4-111">따라서 묶음 및 축소 하지 때 성능을 향상 시킬 동일한 페이지 또는 동일한 자산을 요청 하는 동일한 사이트에서 페이지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-111">Consequently, bundling and minification don't improve performance when requesting the same page, or pages, on the same site requesting the same assets.</span></span> <span data-ttu-id="88fc4-112">경우는 만료 헤더 자산에서 올바르게 설정 되지 않습니다 및 묶음 및 축소를 사용 하지 않는 경우 브라우저의 새로 고침 추론 표시 자산 부실 몇 일 후입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-112">If the expires header isn't set correctly on the assets and if bundling and minification isn't used, the browser's freshness heuristics mark the assets stale after a few days.</span></span> <span data-ttu-id="88fc4-113">또한 브라우저 각 자산에 대 한 유효성 검사는 요청이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-113">Additionally, the browser requires a validation request for each asset.</span></span> <span data-ttu-id="88fc4-114">이 경우 묶음 및 축소 첫 번째 페이지 요청 후에 성능 향상을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-114">In this case, bundling and minification provide a performance improvement even after the first page request.</span></span>

### <a name="bundling"></a><span data-ttu-id="88fc4-115">번들</span><span class="sxs-lookup"><span data-stu-id="88fc4-115">Bundling</span></span>

<span data-ttu-id="88fc4-116">번들로 단일 파일에 여러 파일을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-116">Bundling combines multiple files into a single file.</span></span> <span data-ttu-id="88fc4-117">번들로 웹 페이지와 같은 웹 자산을 렌더링 하는 데 필요한 서버 요청의 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-117">Bundling reduces the number of server requests that are necessary to render a web asset, such as a web page.</span></span> <span data-ttu-id="88fc4-118">CSS, JavaScript 등을 위해 특별히 개수에 관계 없이 개별 번들을 만들 수 있습니다. 더 적은 파일 서버로 브라우저 또는 응용 프로그램을 제공 하는 서비스에서 더 적은 수의 HTTP 요청을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-118">You can create any number of individual bundles specifically for CSS, JavaScript, etc. Fewer files means fewer HTTP requests from the browser to the server or from the service providing your application.</span></span> <span data-ttu-id="88fc4-119">이 결과에서 첫 번째 페이지 로드 성능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-119">This results in improved first page load performance.</span></span>

### <a name="minification"></a><span data-ttu-id="88fc4-120">축소</span><span class="sxs-lookup"><span data-stu-id="88fc4-120">Minification</span></span>

<span data-ttu-id="88fc4-121">축소 기능을 변경 하지 않고 코드에서 불필요 한 문자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-121">Minification removes unnecessary characters from code without altering functionality.</span></span> <span data-ttu-id="88fc4-122">결과 요청 된 자산 (예: CSS, 이미지 및 JavaScript 파일)의 크기가 크게 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-122">The result is a significant size reduction in requested assets (such as CSS, images, and JavaScript files).</span></span> <span data-ttu-id="88fc4-123">축소의 일반적인 부작용 변수 이름의 문자 하나를 줄이는 등 주석 및 불필요 한 공백을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-123">Common side effects of minification include shortening variable names to one character and removing comments and unnecessary whitespace.</span></span>

<span data-ttu-id="88fc4-124">다음 JavaScript 함수를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="88fc4-124">Consider the following JavaScript function:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.js)]

<span data-ttu-id="88fc4-125">다음으로 함수를 축소 하는 축소:</span><span class="sxs-lookup"><span data-stu-id="88fc4-125">Minification reduces the function to the following:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.min.js)]

<span data-ttu-id="88fc4-126">주석 및 불필요 한 공백을 제거 하는 것 외에도 다음 매개 변수 및 변수 이름은 다음과 같이 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-126">In addition to removing the comments and unnecessary whitespace, the following parameter and variable names were renamed as follows:</span></span>

<span data-ttu-id="88fc4-127">원래 색</span><span class="sxs-lookup"><span data-stu-id="88fc4-127">Original</span></span> | <span data-ttu-id="88fc4-128">이름이 바뀜</span><span class="sxs-lookup"><span data-stu-id="88fc4-128">Renamed</span></span>
--- | :---:
`imageTagAndImageID` | `t`
`imageContext` | `a`
`imageElement` | `r`

## <a name="impact-of-bundling-and-minification"></a><span data-ttu-id="88fc4-129">묶음 및 축소의 영향</span><span class="sxs-lookup"><span data-stu-id="88fc4-129">Impact of bundling and minification</span></span>

<span data-ttu-id="88fc4-130">다음 표에서 개별적으로 자산을 로드 하 고 묶음 및 축소를 사용 하 여 차이점을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-130">The following table outlines differences between individually loading assets and using bundling and minification:</span></span>

<span data-ttu-id="88fc4-131">작업</span><span class="sxs-lookup"><span data-stu-id="88fc4-131">Action</span></span> | <span data-ttu-id="88fc4-132">B/M을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="88fc4-132">With B/M</span></span> | <span data-ttu-id="88fc4-133">B/M 없이</span><span class="sxs-lookup"><span data-stu-id="88fc4-133">Without B/M</span></span> | <span data-ttu-id="88fc4-134">변경</span><span class="sxs-lookup"><span data-stu-id="88fc4-134">Change</span></span>
--- | :---: | :---: | :---:
<span data-ttu-id="88fc4-135">파일 요청</span><span class="sxs-lookup"><span data-stu-id="88fc4-135">File Requests</span></span>  | <span data-ttu-id="88fc4-136">7</span><span class="sxs-lookup"><span data-stu-id="88fc4-136">7</span></span>   | <span data-ttu-id="88fc4-137">18</span><span class="sxs-lookup"><span data-stu-id="88fc4-137">18</span></span>     | <span data-ttu-id="88fc4-138">157%</span><span class="sxs-lookup"><span data-stu-id="88fc4-138">157%</span></span>
<span data-ttu-id="88fc4-139">전송 (kb)</span><span class="sxs-lookup"><span data-stu-id="88fc4-139">KB Transferred</span></span> | <span data-ttu-id="88fc4-140">156</span><span class="sxs-lookup"><span data-stu-id="88fc4-140">156</span></span> | <span data-ttu-id="88fc4-141">264.68</span><span class="sxs-lookup"><span data-stu-id="88fc4-141">264.68</span></span> | <span data-ttu-id="88fc4-142">70%</span><span class="sxs-lookup"><span data-stu-id="88fc4-142">70%</span></span>
<span data-ttu-id="88fc4-143">로드 시간 (ms)</span><span class="sxs-lookup"><span data-stu-id="88fc4-143">Load Time (ms)</span></span> | <span data-ttu-id="88fc4-144">885</span><span class="sxs-lookup"><span data-stu-id="88fc4-144">885</span></span> | <span data-ttu-id="88fc4-145">2360</span><span class="sxs-lookup"><span data-stu-id="88fc4-145">2360</span></span>   | <span data-ttu-id="88fc4-146">167%</span><span class="sxs-lookup"><span data-stu-id="88fc4-146">167%</span></span>

<span data-ttu-id="88fc4-147">브라우저는 HTTP 요청 헤더와 관련 하 여 매우 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="88fc4-147">Browsers are fairly verbose with regard to HTTP request headers.</span></span> <span data-ttu-id="88fc4-148">총 바이트 수를 번들로 묶으면 메트릭을 본 상당히 감소 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-148">The total bytes sent metric saw a significant reduction when bundling.</span></span> <span data-ttu-id="88fc4-149">이 예제에서는 로컬로 실행 되지만 로드 시간 향상을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-149">The load time shows a significant improvement, however this example ran locally.</span></span> <span data-ttu-id="88fc4-150">큰 성능 향상은 묶음 및 축소를 사용 하 여 자산을 사용 하 여 네트워크를 통해 전송 될 때 실현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-150">Greater performance gains are realized when using bundling and minification with assets transferred over a network.</span></span>

## <a name="choose-a-bundling-and-minification-strategy"></a><span data-ttu-id="88fc4-151">묶음 및 축소 전략 선택</span><span class="sxs-lookup"><span data-stu-id="88fc4-151">Choose a bundling and minification strategy</span></span>

<span data-ttu-id="88fc4-152">MVC 및 Razor 페이지 프로젝트 템플릿을 묶음 및 축소 JSON 구성 파일의 구성에 대 한 기본 제공 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-152">The MVC and Razor Pages project templates provide an out-of-the-box solution for bundling and minification consisting of a JSON configuration file.</span></span> <span data-ttu-id="88fc4-153">와 같은 타사 도구를 [Gulp](xref:client-side/using-gulp) 하 고 [Grunt](xref:client-side/using-grunt) 실행 기 작업을 좀 더 많은 복잡성을 사용 하 여 동일한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-153">Third-party tools, such as the [Gulp](xref:client-side/using-gulp) and [Grunt](xref:client-side/using-grunt) task runners, accomplish the same tasks with a bit more complexity.</span></span> <span data-ttu-id="88fc4-154">개발 워크플로에서 처리 묶음 및 축소 초과 해야 하는 경우 타사 도구는 최적의 선택&mdash;lint 및 이미지 최적화와 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-154">A third-party tool is a great fit when your development workflow requires processing beyond bundling and minification&mdash;such as linting and image optimization.</span></span> <span data-ttu-id="88fc4-155">디자인 타임 묶음 및 축소를 사용 하 여 앱의 배포 하기 전에 축소 된 파일이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-155">By using design-time bundling and minification, the minified files are created prior to the app's deployment.</span></span> <span data-ttu-id="88fc4-156">묶음 및 축소를 배포 하기 전에 서버 부하 감소의 이점이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-156">Bundling and minifying before deployment provides the advantage of reduced server load.</span></span> <span data-ttu-id="88fc4-157">그러나 해당 디자인 타임 묶음을 인식 해야 하 고 축소 빌드 복잡성 증가 정적 파일 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-157">However, it's important to recognize that design-time bundling and minification increases build complexity and only works with static files.</span></span>

## <a name="configure-bundling-and-minification"></a><span data-ttu-id="88fc4-158">묶음 및 축소 구성</span><span class="sxs-lookup"><span data-stu-id="88fc4-158">Configure bundling and minification</span></span>

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="88fc4-159">MVC 및 Razor 페이지 프로젝트 템플릿을 제공 하는 ASP.NET Core 2.0 또는 이전에 *bundleconfig.json* 각 번들에 대 한 옵션을 정의 하는 구성 파일:</span><span class="sxs-lookup"><span data-stu-id="88fc4-159">In ASP.NET Core 2.0 or earlier, the MVC and Razor Pages project templates provide a *bundleconfig.json* configuration file that defines the options for each bundle:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="88fc4-160">ASP.NET Core 2.1 이상 버전에서는 명명 된 새 JSON 파일을 추가 *bundleconfig.json*, MVC 또는 Razor 페이지 프로젝트 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-160">In ASP.NET Core 2.1 or later, add a new JSON file, named *bundleconfig.json*, to the MVC or Razor Pages project root.</span></span> <span data-ttu-id="88fc4-161">시작 지점으로 해당 파일에 다음 JSON을 포함:</span><span class="sxs-lookup"><span data-stu-id="88fc4-161">Include the following JSON in that file as a starting point:</span></span>

::: moniker-end

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig.json)]

<span data-ttu-id="88fc4-162">합니다 *bundleconfig.json* 파일은 각 번들에 대 한 옵션을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-162">The *bundleconfig.json* file defines the options for each bundle.</span></span> <span data-ttu-id="88fc4-163">앞의 예제는 단일 번들 구성 사용자 지정 JavaScript에 대 한 정의 됩니다 (*wwwroot/js/site.js*) 및 스타일 시트 (*wwwroot/css/site.css*) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-163">In the preceding example, a single bundle configuration is defined for the custom JavaScript (*wwwroot/js/site.js*) and stylesheet (*wwwroot/css/site.css*) files.</span></span>

<span data-ttu-id="88fc4-164">구성 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-164">Configuration options include:</span></span>

* <span data-ttu-id="88fc4-165">`outputFileName`: 출력 번들 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-165">`outputFileName`: The name of the bundle file to output.</span></span> <span data-ttu-id="88fc4-166">상대 경로 포함할 수는 *bundleconfig.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-166">Can contain a relative path from the *bundleconfig.json* file.</span></span> <span data-ttu-id="88fc4-167">**required**</span><span class="sxs-lookup"><span data-stu-id="88fc4-167">**required**</span></span>
* <span data-ttu-id="88fc4-168">`inputFiles`: 배열 함께 번들로 제공할 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-168">`inputFiles`: An array of files to bundle together.</span></span> <span data-ttu-id="88fc4-169">이들은 구성 파일에 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-169">These are relative paths to the configuration file.</span></span> <span data-ttu-id="88fc4-170">**선택적**, \* 값이 비어 있으면 빈 출력 파일에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-170">**optional**, \*an empty value results in an empty output file.</span></span> <span data-ttu-id="88fc4-171">[와일드 카드 사용](http://www.tldp.org/LDP/abs/html/globbingref.html) 패턴이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-171">[globbing](http://www.tldp.org/LDP/abs/html/globbingref.html) patterns are supported.</span></span>
* <span data-ttu-id="88fc4-172">`minify`축소 옵션: 출력 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-172">`minify`: The minification options for the output type.</span></span> <span data-ttu-id="88fc4-173">**optional**, *default - `minify: { enabled: true }`*</span><span class="sxs-lookup"><span data-stu-id="88fc4-173">**optional**, *default - `minify: { enabled: true }`*</span></span>
  * <span data-ttu-id="88fc4-174">구성 옵션은 출력 파일 형식 당 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-174">Configuration options are available per output file type.</span></span>
    * [<span data-ttu-id="88fc4-175">CSS Minifier입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-175">CSS Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki/cssminifier)
    * [<span data-ttu-id="88fc4-176">JavaScript Minifier입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-176">JavaScript Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki/JavaScript-Minifier-settings)
    * [<span data-ttu-id="88fc4-177">HTML Minifier입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-177">HTML Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki)
* <span data-ttu-id="88fc4-178">`includeInProject`: 프로젝트 파일에 생성 된 파일을 추가할지 여부를 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-178">`includeInProject`: Flag indicating whether to add generated files to project file.</span></span> <span data-ttu-id="88fc4-179">**optional**, *default - false*</span><span class="sxs-lookup"><span data-stu-id="88fc4-179">**optional**, *default - false*</span></span>
* <span data-ttu-id="88fc4-180">`sourceMap`: 해당 번들된 파일에 대 한 소스 맵을 생성할지 여부를 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-180">`sourceMap`: Flag indicating whether to generate a source map for the bundled file.</span></span> <span data-ttu-id="88fc4-181">**optional**, *default - false*</span><span class="sxs-lookup"><span data-stu-id="88fc4-181">**optional**, *default - false*</span></span>
* <span data-ttu-id="88fc4-182">`sourceMapRootPath`: 생성 된 소스 맵 파일을 저장 하는 것에 대 한 루트 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-182">`sourceMapRootPath`: The root path for storing the generated source map file.</span></span>

## <a name="build-time-execution-of-bundling-and-minification"></a><span data-ttu-id="88fc4-183">묶음 및 축소의 빌드 시간 실행</span><span class="sxs-lookup"><span data-stu-id="88fc4-183">Build-time execution of bundling and minification</span></span>

<span data-ttu-id="88fc4-184">합니다 [BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) 실행 묶음 및 축소 빌드 시 NuGet 패키지에 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-184">The [BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) NuGet package enables the execution of bundling and minification at build time.</span></span> <span data-ttu-id="88fc4-185">패키지를 삽입 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets) 는 빌드 및 정리 시간에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-185">The package injects [MSBuild Targets](/visualstudio/msbuild/msbuild-targets) which run at build and clean time.</span></span> <span data-ttu-id="88fc4-186">합니다 *bundleconfig.json* 정의 된 구성에 따라 출력 파일을 생성 하는 빌드 프로세스에서 분석 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-186">The *bundleconfig.json* file is analyzed by the build process to produce the output files based on the defined configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="88fc4-187">BuildBundlerMinifier는 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-187">BuildBundlerMinifier belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="88fc4-188">문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-188">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="88fc4-189">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88fc4-189">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="88fc4-190">추가 된 *BuildBundlerMinifier* 패키지를 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-190">Add the *BuildBundlerMinifier* package to your project.</span></span>

<span data-ttu-id="88fc4-191">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-191">Build the project.</span></span> <span data-ttu-id="88fc4-192">다음이 출력 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-192">The following appears in the Output window:</span></span>

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

<span data-ttu-id="88fc4-193">프로젝트를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-193">Clean the project.</span></span> <span data-ttu-id="88fc4-194">다음이 출력 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-194">The following appears in the Output window:</span></span>

```console
1>------ Clean started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Cleaning output from bundleconfig.json
1>Bundler: Done cleaning output file from bundleconfig.json
========== Clean: 1 succeeded, 0 failed, 0 skipped ==========
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="88fc4-195">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="88fc4-195">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="88fc4-196">추가 된 *BuildBundlerMinifier* 패키지를 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="88fc4-196">Add the *BuildBundlerMinifier* package to your project:</span></span>

```console
dotnet add package BuildBundlerMinifier
```

<span data-ttu-id="88fc4-197">ASP.NET을 사용 하는 경우 Core 1.x의 경우 새로 추가 된 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-197">If using ASP.NET Core 1.x, restore the newly added package:</span></span>

```console
dotnet restore
```

<span data-ttu-id="88fc4-198">프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="88fc4-198">Build the project:</span></span>

```console
dotnet build
```

<span data-ttu-id="88fc4-199">다음 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-199">The following appears:</span></span>

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


    Bundler: Begin processing bundleconfig.json
    Bundler: Done processing bundleconfig.json
    BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
```

<span data-ttu-id="88fc4-200">프로젝트를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-200">Clean the project:</span></span>

```console
dotnet clean
```

<span data-ttu-id="88fc4-201">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-201">The following output appears:</span></span>

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


  Bundler: Cleaning output from bundleconfig.json
  Bundler: Done cleaning output file from bundleconfig.json
```

---

## <a name="ad-hoc-execution-of-bundling-and-minification"></a><span data-ttu-id="88fc4-202">묶음 및 축소의 임시 실행</span><span class="sxs-lookup"><span data-stu-id="88fc4-202">Ad hoc execution of bundling and minification</span></span>

<span data-ttu-id="88fc4-203">프로젝트를 빌드하지 않고도 필요할 때마다 번들링 및 축소 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-203">It's possible to run the bundling and minification tasks on an ad hoc basis, without building the project.</span></span> <span data-ttu-id="88fc4-204">[BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-204">Add the [BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet package to your project:</span></span>

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=10)]

> [!NOTE]
> <span data-ttu-id="88fc4-205">BundlerMinifier.Core는 Microsoft에서 지원을 제공하지 않는 GitHub의 커뮤니티 주도 프로젝트에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-205">BundlerMinifier.Core belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="88fc4-206">문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-206">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

<span data-ttu-id="88fc4-207">이 패키지에 포함 하도록.NET Core CLI를 확장 합니다 *dotnet 번들* 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-207">This package extends the .NET Core CLI to include the *dotnet-bundle* tool.</span></span> <span data-ttu-id="88fc4-208">다음 명령은 패키지 관리자 콘솔 (PMC) 창 또는 명령 셸에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-208">The following command can be executed in the Package Manager Console (PMC) window or in a command shell:</span></span>

```console
dotnet bundle
```

> [!IMPORTANT]
> <span data-ttu-id="88fc4-209">NuGet 패키지 관리자는 \*.csproj 파일에 `<PackageReference />` 노드로 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-209">NuGet Package Manager adds dependencies to the \*.csproj file as `<PackageReference />` nodes.</span></span> <span data-ttu-id="88fc4-210">`dotnet bundle` 명령은 `<DotNetCliToolReference />` 노드가 사용되는 경우에만 .NET Core CLI에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-210">The `dotnet bundle` command is registered with the .NET Core CLI only when a `<DotNetCliToolReference />` node is used.</span></span> <span data-ttu-id="88fc4-211">그에 맞춰 \*.Csproj 파일을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-211">Modify the \*.csproj file accordingly.</span></span>

## <a name="add-files-to-workflow"></a><span data-ttu-id="88fc4-212">워크플로에 파일 추가하기</span><span class="sxs-lookup"><span data-stu-id="88fc4-212">Add files to workflow</span></span>

<span data-ttu-id="88fc4-213">예를 살펴봅니다 추가 *custom.css* 다음과 같은 파일이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-213">Consider an example in which an additional *custom.css* file is added resembling the following:</span></span>

[!code-css[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/css/custom.css)]

<span data-ttu-id="88fc4-214">*custom.css*를 축소하고 이를 *site.css*와 함께 *site.min.css* 파일에 번들하려면 다음과 같이 상대 경로를 *bundleconfig.json*에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-214">To minify *custom.css* and bundle it with *site.css* into a *site.min.css* file, add the relative path to *bundleconfig.json*:</span></span>

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig2.json?highlight=6)]

> [!NOTE]
> <span data-ttu-id="88fc4-215">또는 다음과 같은 와일드 카드 사용 패턴을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-215">Alternatively, the following globbing pattern could be used:</span></span>
>
> ```json
> "inputFiles": ["wwwroot/**/*(*.css|!(*.min.css))"]
> ```
>
> <span data-ttu-id="88fc4-216">모든 CSS 파일과 일치 하는 축소 된 파일 패턴을 제외 하는이 와일드 카드 사용 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-216">This globbing pattern matches all CSS files and excludes the minified file pattern.</span></span>

<span data-ttu-id="88fc4-217">응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-217">Build the application.</span></span> <span data-ttu-id="88fc4-218">*site.min.css*를 열고 *custom.css*의 내용이 파일 끝에 추가되었음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-218">Open *site.min.css* and notice the content of *custom.css* is appended to the end of the file.</span></span>

## <a name="environment-based-bundling-and-minification"></a><span data-ttu-id="88fc4-219">환경 기반 묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="88fc4-219">Environment-based bundling and minification</span></span>

<span data-ttu-id="88fc4-220">모범 사례로, 프로덕션 환경에서 앱의 번들 및 축소 된 파일은을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-220">As a best practice, the bundled and minified files of your app should be used in a production environment.</span></span> <span data-ttu-id="88fc4-221">개발 하는 동안 원래 파일은 앱의 쉬운 디버깅에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-221">During development, the original files make for easier debugging of the app.</span></span>

<span data-ttu-id="88fc4-222">뷰에서 [Environment 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)를 사용하여 페이지에 포함할 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-222">Specify which files to include in your pages by using the [Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) in your views.</span></span> <span data-ttu-id="88fc4-223">Environment 태그 도우미는 특정 [환경](xref:fundamentals/environments)에서 실행될 때만 자신의 내용을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-223">The Environment Tag Helper only renders its contents when running in specific [environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="88fc4-224">다음 `environment` 태그 실행 하는 경우 처리 되지 않은 CSS 파일을 렌더링 합니다 `Development` 환경:</span><span class="sxs-lookup"><span data-stu-id="88fc4-224">The following `environment` tag renders the unprocessed CSS files when running in the `Development` environment:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=21-24)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=9-12)]

::: moniker-end

<span data-ttu-id="88fc4-225">다음 `environment` 이외의 환경에서 실행 하는 경우 태그 렌더링 묶이고 CSS 파일 `Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-225">The following `environment` tag renders the bundled and minified CSS files when running in an environment other than `Development`.</span></span> <span data-ttu-id="88fc4-226">예를 들어에서 실행 중인 `Production` 또는 `Staging` 이러한 스타일 시트의 렌더링을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-226">For example, running in `Production` or `Staging` triggers the rendering of these stylesheets:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=5&range=25-30)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=13-18)]

::: moniker-end

## <a name="consume-bundleconfigjson-from-gulp"></a><span data-ttu-id="88fc4-227">Gulp에서 bundleconfig.json 사용</span><span class="sxs-lookup"><span data-stu-id="88fc4-227">Consume bundleconfig.json from Gulp</span></span>

<span data-ttu-id="88fc4-228">앱의 묶음 및 축소 워크플로 추가 처리를 필요로 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-228">There are cases in which an app's bundling and minification workflow requires additional processing.</span></span> <span data-ttu-id="88fc4-229">이미지 최적화, 캐시 버스팅 및 CDN 자산 처리를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-229">Examples include image optimization, cache busting, and CDN asset processing.</span></span> <span data-ttu-id="88fc4-230">이러한 요구 사항을 충족 하려면 묶음 및 축소 워크플로의 Gulp를 사용 하 여 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-230">To satisfy these requirements, you can convert the bundling and minification workflow to use Gulp.</span></span>

### <a name="use-the-bundler--minifier-extension"></a><span data-ttu-id="88fc4-231">Bundler & Minifier 확장 사용</span><span class="sxs-lookup"><span data-stu-id="88fc4-231">Use the Bundler & Minifier extension</span></span>

<span data-ttu-id="88fc4-232">Visual Studio [Bundler & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) 확장 처리 Gulp로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-232">The Visual Studio [Bundler & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) extension handles the conversion to Gulp.</span></span>

> [!NOTE]
> <span data-ttu-id="88fc4-233">Bundler & Minifier 확장 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-233">The Bundler & Minifier extension belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="88fc4-234">문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-234">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

<span data-ttu-id="88fc4-235">마우스 오른쪽 단추로 클릭 합니다 *bundleconfig.json* 솔루션 탐색기에서 파일을 선택 **Bundler & Minifier** > **Gulp를 변환 하는 중...** :</span><span class="sxs-lookup"><span data-stu-id="88fc4-235">Right-click the *bundleconfig.json* file in Solution Explorer and select **Bundler & Minifier** > **Convert To Gulp...**:</span></span>

![Convert To Gulp 컨텍스트 메뉴](../client-side/bundling-and-minification/_static/convert-to-gulp.png)

<span data-ttu-id="88fc4-237">그러면 프로젝트에 *gulpfile.js* 및 *package.json* 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-237">The *gulpfile.js* and *package.json* files are added to the project.</span></span> <span data-ttu-id="88fc4-238">그리고 *package.json* 파일의 `devDependencies` 섹션에 나열된 지원 [npm](https://www.npmjs.com/) 패키지들이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-238">The supporting [npm](https://www.npmjs.com/) packages listed in the *package.json* file's `devDependencies` section are installed.</span></span>

<span data-ttu-id="88fc4-239">PMC 창에서 다음 명령을 실행하여 Gulp CLI를 전역 종속성으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-239">Run the following command in the PMC window to install the Gulp CLI as a global dependency:</span></span>

```console
npm i -g gulp-cli
```

<span data-ttu-id="88fc4-240">입력, 출력 및 설정을 위해 *gulpfile.js* 파일에서 *bundleconfig.json* 파일을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-240">The *gulpfile.js* file reads the *bundleconfig.json* file for the inputs, outputs, and settings.</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-12&highlight=10)]

### <a name="convert-manually"></a><span data-ttu-id="88fc4-241">직접 변환하기</span><span class="sxs-lookup"><span data-stu-id="88fc4-241">Convert manually</span></span>

<span data-ttu-id="88fc4-242">Visual Studio 및/또는 Bundler & Minifier 확장을 사용할 수 없는 경우 수동으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-242">If Visual Studio and/or the Bundler & Minifier extension aren't available, convert manually.</span></span>

<span data-ttu-id="88fc4-243">프로젝트 루트에 다음 `devDependencies`가 지정된 *package.json* 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-243">Add a *package.json* file, with the following `devDependencies`, to the project root:</span></span>

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/package.json?range=5-13)]

<span data-ttu-id="88fc4-244">*package.json*과 동일한 수준에서 다음 명령을 실행하여 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-244">Install the dependencies by running the following command at the same level as *package.json*:</span></span>

```console
npm i
```

<span data-ttu-id="88fc4-245">전역 종속성으로 Gulp CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-245">Install the Gulp CLI as a global dependency:</span></span>

```console
npm i -g gulp-cli
```

<span data-ttu-id="88fc4-246">*gulpfile.js* 파일을 프로젝트 루트 아래에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-246">Copy the *gulpfile.js* file below to the project root:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-11,14-)]

### <a name="run-gulp-tasks"></a><span data-ttu-id="88fc4-247">Gulp 작업 실행하기</span><span class="sxs-lookup"><span data-stu-id="88fc4-247">Run Gulp tasks</span></span>

<span data-ttu-id="88fc4-248">Gulp 축소 작업 전에 Visual Studio에서 프로젝트 빌드를 트리거하려면 다음을 추가 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets) \*.csproj 파일에:</span><span class="sxs-lookup"><span data-stu-id="88fc4-248">To trigger the Gulp minification task before the project builds in Visual Studio, add the following [MSBuild Target](/visualstudio/msbuild/msbuild-targets) to the \*.csproj file:</span></span>

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=14-16)]

<span data-ttu-id="88fc4-249">이 예제에서는 모든 작업 내에서 정의 합니다 `MyPreCompileTarget` 대상 전에 미리 정의 된 실행 `Build` 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-249">In this example, any tasks defined within the `MyPreCompileTarget` target run before the predefined `Build` target.</span></span> <span data-ttu-id="88fc4-250">Visual Studio의 출력 창에 다음과 유사한 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-250">Output similar to the following appears in Visual Studio's Output window:</span></span>

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

<span data-ttu-id="88fc4-251">또는 Visual Studio의 작업 러너 탐색기를 사용하여 Gulp 작업을 특정 Visual Studio 이벤트에 바인딩 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-251">Alternatively, Visual Studio's Task Runner Explorer may be used to bind Gulp tasks to specific Visual Studio events.</span></span> <span data-ttu-id="88fc4-252">이에 대한 지침은 [기본 작업 실행하기](xref:client-side/using-gulp#running-default-tasks)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="88fc4-252">See [Running default tasks](xref:client-side/using-gulp#running-default-tasks) for instructions on doing that.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88fc4-253">추가 자료</span><span class="sxs-lookup"><span data-stu-id="88fc4-253">Additional resources</span></span>

* [<span data-ttu-id="88fc4-254">Gulp 사용하기</span><span class="sxs-lookup"><span data-stu-id="88fc4-254">Use Gulp</span></span>](xref:client-side/using-gulp)
* [<span data-ttu-id="88fc4-255">Grunt 사용하기</span><span class="sxs-lookup"><span data-stu-id="88fc4-255">Use Grunt</span></span>](xref:client-side/using-grunt)
* [<span data-ttu-id="88fc4-256">여러 환경 사용</span><span class="sxs-lookup"><span data-stu-id="88fc4-256">Use multiple environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="88fc4-257">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="88fc4-257">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
