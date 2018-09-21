---
title: JavaScriptServices를 사용 하 여 ASP.NET Core의 단일 페이지 응용 프로그램을 만들려면
author: scottaddie
description: JavaScriptServices를 사용 하 여 단일 페이지 응용 프로그램 (SPA) ASP.NET Core에서 지 원하는 만들려면의 이점에 대해 알아봅니다.
ms.author: scaddie
ms.custom: H1Hack27Feb2017
ms.date: 08/02/2017
uid: client-side/spa-services
ms.openlocfilehash: 6d6a92427d5d4b853248e60a12625573c4375515
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523300"
---
# <a name="use-javascriptservices-to-create-single-page-applications-in-aspnet-core"></a><span data-ttu-id="e5ed5-103">JavaScriptServices를 사용 하 여 ASP.NET Core의 단일 페이지 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="e5ed5-103">Use JavaScriptServices to Create Single Page Applications in ASP.NET Core</span></span>

<span data-ttu-id="e5ed5-104">하 여 [Scott Addie](https://github.com/scottaddie) 고 [Fiyaz Hasan](http://fiyazhasan.me/)</span><span class="sxs-lookup"><span data-stu-id="e5ed5-104">By [Scott Addie](https://github.com/scottaddie) and [Fiyaz Hasan](http://fiyazhasan.me/)</span></span>

<span data-ttu-id="e5ed5-105">단일 페이지 응용 프로그램 (SPA)에 내재 된 풍부한 사용자 경험으로 인해 웹 응용 프로그램의 인기 있는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-105">A Single Page Application (SPA) is a popular type of web application due to its inherent rich user experience.</span></span> <span data-ttu-id="e5ed5-106">클라이언트 쪽 SPA 프레임 워크 또는 라이브러리와 같은 통합 [Angular](https://angular.io/) 또는 [반응](https://facebook.github.io/react/), ASP.NET Core 어려울 수와 같은 서버 쪽 프레임 워크를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-106">Integrating client-side SPA frameworks or libraries, such as [Angular](https://angular.io/) or [React](https://facebook.github.io/react/), with server-side frameworks like ASP.NET Core can be difficult.</span></span> <span data-ttu-id="e5ed5-107">[JavaScriptServices](https://github.com/aspnet/JavaScriptServices) 통합 프로세스의 마찰을 줄이기 위해 개발 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-107">[JavaScriptServices](https://github.com/aspnet/JavaScriptServices) was developed to reduce friction in the integration process.</span></span> <span data-ttu-id="e5ed5-108">클라이언트 및 서버 기술 스택 간의 원활한 작업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-108">It enables seamless operation between the different client and server technology stacks.</span></span>

<a name="what-is-js-services"></a>

## <a name="what-is-javascriptservices"></a><span data-ttu-id="e5ed5-109">JavaScriptServices 란</span><span class="sxs-lookup"><span data-stu-id="e5ed5-109">What is JavaScriptServices</span></span>

<span data-ttu-id="e5ed5-110">JavaScriptServices는 ASP.NET Core에 대 한 클라이언트 쪽 기술 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-110">JavaScriptServices is a collection of client-side technologies for ASP.NET Core.</span></span> <span data-ttu-id="e5ed5-111">ASP.NET Core Spa를 구축 하기 위한 개발자의 기본 서버 쪽 플랫폼으로 배치 하려면 해당 목표가입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-111">Its goal is to position ASP.NET Core as developers' preferred server-side platform for building SPAs.</span></span>

<span data-ttu-id="e5ed5-112">JavaScriptServices 세 가지 고유 NuGet 패키지 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-112">JavaScriptServices consists of three distinct NuGet packages:</span></span>

* <span data-ttu-id="e5ed5-113">[Microsoft.AspNetCore.NodeServices](https://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/) (NodeServices)</span><span class="sxs-lookup"><span data-stu-id="e5ed5-113">[Microsoft.AspNetCore.NodeServices](https://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/) (NodeServices)</span></span>
* <span data-ttu-id="e5ed5-114">[Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) (SpaServices)</span><span class="sxs-lookup"><span data-stu-id="e5ed5-114">[Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) (SpaServices)</span></span>
* <span data-ttu-id="e5ed5-115">[Microsoft.AspNetCore.SpaTemplates](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaTemplates/) (SpaTemplates)</span><span class="sxs-lookup"><span data-stu-id="e5ed5-115">[Microsoft.AspNetCore.SpaTemplates](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaTemplates/) (SpaTemplates)</span></span>

<span data-ttu-id="e5ed5-116">이러한 패키지는 유용한 경우 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-116">These packages are useful if you:</span></span>

* <span data-ttu-id="e5ed5-117">서버에서 JavaScript를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-117">Run JavaScript on the server</span></span>
* <span data-ttu-id="e5ed5-118">SPA 프레임 워크 나 라이브러리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e5ed5-118">Use a SPA framework or library</span></span>
* <span data-ttu-id="e5ed5-119">Webpack 사용 하 여 클라이언트 쪽 자산 빌드</span><span class="sxs-lookup"><span data-stu-id="e5ed5-119">Build client-side assets with Webpack</span></span>

<span data-ttu-id="e5ed5-120">이 문서에 포커스를 많은 SpaServices 패키지를 사용 하 여 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-120">Much of the focus in this article is placed on using the SpaServices package.</span></span>

<a name="what-is-spa-services"></a>

## <a name="what-is-spaservices"></a><span data-ttu-id="e5ed5-121">SpaServices 란</span><span class="sxs-lookup"><span data-stu-id="e5ed5-121">What is SpaServices</span></span>

<span data-ttu-id="e5ed5-122">ASP.NET Core Spa를 구축 하기 위한 개발자의 기본 서버 쪽 플랫폼으로 배치 하려면 SpaServices 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-122">SpaServices was created to position ASP.NET Core as developers' preferred server-side platform for building SPAs.</span></span> <span data-ttu-id="e5ed5-123">SpaServices 개발 ASP.NET Core를 사용 하 여 Spa를 필요 하지 않습니다 하 고 특정 클라이언트 프레임 워크에 사용자를 잠글 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-123">SpaServices isn't required to develop SPAs with ASP.NET Core, and it doesn't lock you into a particular client framework.</span></span>

<span data-ttu-id="e5ed5-124">SpaServices 같은 유용한 인프라를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-124">SpaServices provides useful infrastructure such as:</span></span>

* [<span data-ttu-id="e5ed5-125">서버 쪽 사전 렌더링이</span><span class="sxs-lookup"><span data-stu-id="e5ed5-125">Server-side prerendering</span></span>](#server-prerendering)
* [<span data-ttu-id="e5ed5-126">Webpack 개발 미들웨어</span><span class="sxs-lookup"><span data-stu-id="e5ed5-126">Webpack Dev Middleware</span></span>](#webpack-dev-middleware)
* [<span data-ttu-id="e5ed5-127">핫 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="e5ed5-127">Hot Module Replacement</span></span>](#hot-module-replacement)
* [<span data-ttu-id="e5ed5-128">라우팅 도우미</span><span class="sxs-lookup"><span data-stu-id="e5ed5-128">Routing helpers</span></span>](#routing-helpers)

<span data-ttu-id="e5ed5-129">종합적으로 이러한 인프라 구성 요소 개발 워크플로 및 런타임 환경을 모두 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-129">Collectively, these infrastructure components enhance both the development workflow and the runtime experience.</span></span> <span data-ttu-id="e5ed5-130">구성 요소를 개별적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-130">The components can be adopted individually.</span></span>

<a name="spa-services-prereqs"></a>

## <a name="prerequisites-for-using-spaservices"></a><span data-ttu-id="e5ed5-131">SpaServices 사용 하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="e5ed5-131">Prerequisites for using SpaServices</span></span>

<span data-ttu-id="e5ed5-132">SpaServices를 사용 하려면 다음을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-132">To work with SpaServices, install the following:</span></span>

* <span data-ttu-id="e5ed5-133">[Node.js](https://nodejs.org/) (버전 6 이상) npm을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e5ed5-133">[Node.js](https://nodejs.org/) (version 6 or later) with npm</span></span>
  * <span data-ttu-id="e5ed5-134">이러한 구성 요소 설치 되 고 있을 수를 확인 하려면 명령줄에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-134">To verify these components are installed and can be found, run the following from the command line:</span></span>

    ```console
    node -v && npm -v
    ```

<span data-ttu-id="e5ed5-135">참고: Azure 웹 사이트에 배포 하는 경우 필요가 여기에서 모든 작업을 수행할 &mdash; Node.js 설치 되어 서버 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-135">Note: If you're deploying to an Azure web site, you don't need to do anything here &mdash; Node.js is installed and available in the server environments.</span></span>

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]

  * <span data-ttu-id="e5ed5-136">Visual Studio 2017을 사용 하 여 Windows를 사용 하는 경우 SDK가 선택 하 여 설치 합니다 **.NET Core 플랫폼 간 개발** 워크 로드.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-136">If you're on Windows using Visual Studio 2017, the SDK is installed by selecting the **.NET Core cross-platform development** workload.</span></span>

* <span data-ttu-id="e5ed5-137">[Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="e5ed5-137">[Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) NuGet package</span></span>

<a name="server-prerendering"></a>

## <a name="server-side-prerendering"></a><span data-ttu-id="e5ed5-138">서버 쪽 사전 렌더링이</span><span class="sxs-lookup"><span data-stu-id="e5ed5-138">Server-side prerendering</span></span>

<span data-ttu-id="e5ed5-139">유니버설 (라고도 해) 응용 프로그램을는 JavaScript 응용 프로그램 서버와 클라이언트 둘 다 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-139">A universal (also known as isomorphic) application is a JavaScript application capable of running both on the server and the client.</span></span> <span data-ttu-id="e5ed5-140">Angular, React 및 기타 인기 있는 프레임 워크에는이 응용 프로그램 개발 스타일에 대 한 유니버설 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-140">Angular, React, and other popular frameworks provide a universal platform for this application development style.</span></span> <span data-ttu-id="e5ed5-141">먼저 Node.js 통해 서버에서 프레임 워크 구성 요소를 렌더링 하 고 클라이언트를 실행 한 다음 대리자 추가 하는 개념이입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-141">The idea is to first render the framework components on the server via Node.js, and then delegate further execution to the client.</span></span>

<span data-ttu-id="e5ed5-142">ASP.NET Core [태그 도우미](xref:mvc/views/tag-helpers/intro) 제공한 SpaServices 서버에서 JavaScript 함수를 호출 하 여 서버 쪽 사전 렌더링이 구현을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-142">ASP.NET Core [Tag Helpers](xref:mvc/views/tag-helpers/intro) provided by SpaServices simplify the implementation of server-side prerendering by invoking the JavaScript functions on the server.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e5ed5-143">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e5ed5-143">Prerequisites</span></span>

<span data-ttu-id="e5ed5-144">다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-144">Install the following:</span></span>

* <span data-ttu-id="e5ed5-145">[aspnet 사전 렌더링이](https://www.npmjs.com/package/aspnet-prerendering) npm 패키지:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-145">[aspnet-prerendering](https://www.npmjs.com/package/aspnet-prerendering) npm package:</span></span>

    ```console
    npm i -S aspnet-prerendering
    ```

### <a name="configuration"></a><span data-ttu-id="e5ed5-146">구성</span><span class="sxs-lookup"><span data-stu-id="e5ed5-146">Configuration</span></span>

<span data-ttu-id="e5ed5-147">프로젝트의 태그 도우미는 네임 스페이스 등록을 통해 검색할 내용이 *_ViewImports.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-147">The Tag Helpers are made discoverable via namespace registration in the project's *_ViewImports.cshtml* file:</span></span>

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/_ViewImports.cshtml?highlight=3)]

<span data-ttu-id="e5ed5-148">이러한 태그 도우미는 HTML 형식의 구문을 Razor 뷰 내에서 활용 하 여 하위 수준 Api와 직접 통신의 복잡성을 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-148">These Tag Helpers abstract away the intricacies of communicating directly with low-level APIs by leveraging an HTML-like syntax inside the Razor view:</span></span>

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=5)]

### <a name="the-asp-prerender-module-tag-helper"></a><span data-ttu-id="e5ed5-149">`asp-prerender-module` 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="e5ed5-149">The `asp-prerender-module` Tag Helper</span></span>

<span data-ttu-id="e5ed5-150">합니다 `asp-prerender-module` 앞의 코드 예제에 사용 되는 태그 도우미를 실행 *ClientApp/dist/main-server.js* Node.js 통해 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-150">The `asp-prerender-module` Tag Helper, used in the preceding code example, executes *ClientApp/dist/main-server.js* on the server via Node.js.</span></span> <span data-ttu-id="e5ed5-151">말씀 드리지만 대 한 *기본 server.js* 파일이 TypeScript-JavaScript 소스 간 컴파일 태스크의 아티팩트를 [Webpack](http://webpack.github.io/) 빌드 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-151">For clarity's sake, *main-server.js* file is an artifact of the TypeScript-to-JavaScript transpilation task in the [Webpack](http://webpack.github.io/) build process.</span></span> <span data-ttu-id="e5ed5-152">항목 지점 별칭을 정의 하는 Webpack `main-server`;이 별칭에 대 한 종속성 그래프 순회를 시작 및 합니다 *ClientApp/부팅-server.ts* 파일:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-152">Webpack defines an entry point alias of `main-server`; and, traversal of the dependency graph for this alias begins at the *ClientApp/boot-server.ts* file:</span></span>

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=53)]

<span data-ttu-id="e5ed5-153">예에서 다음 Angular를 *ClientApp/부팅-server.ts* 파일 활용 합니다 `createServerRenderer` 함수 및 `RenderResult` 유형의 `aspnet-prerendering` Node.js 통해 서버 렌더링을 구성 하려면 npm 패키지.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-153">In the following Angular example, the *ClientApp/boot-server.ts* file utilizes the `createServerRenderer` function and `RenderResult` type of the `aspnet-prerendering` npm package to configure server rendering via Node.js.</span></span> <span data-ttu-id="e5ed5-154">보내는 서버 쪽 렌더링은 강력한 JavaScript에 래핑되는 해결 함수 호출에 전달 되는 HTML 태그 `Promise` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-154">The HTML markup destined for server-side rendering is passed to a resolve function call, which is wrapped in a strongly-typed JavaScript `Promise` object.</span></span> <span data-ttu-id="e5ed5-155">`Promise` 개체의 중요 한 이유는 DOM의 자리 표시자 요소에 주입을 위한 페이지에 HTML 태그를 비동기적으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-155">The `Promise` object's significance is that it asynchronously supplies the HTML markup to the page for injection in the DOM's placeholder element.</span></span>

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-34,79-)]

### <a name="the-asp-prerender-data-tag-helper"></a><span data-ttu-id="e5ed5-156">`asp-prerender-data` 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="e5ed5-156">The `asp-prerender-data` Tag Helper</span></span>

<span data-ttu-id="e5ed5-157">와 결합 하면 합니다 `asp-prerender-module` 태그 도우미는 `asp-prerender-data` 태그 도우미는 Razor 보기에서 컨텍스트 정보를 서버 쪽 JavaScript 전달할 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-157">When coupled with the `asp-prerender-module` Tag Helper, the `asp-prerender-data` Tag Helper can be used to pass contextual information from the Razor view to the server-side JavaScript.</span></span> <span data-ttu-id="e5ed5-158">다음 태그는 사용자 데이터를 전달 하는 예를 들어를 `main-server` 모듈:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-158">For example, the following markup passes user data to the `main-server` module:</span></span>

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=9-12)]

<span data-ttu-id="e5ed5-159">받은 `UserName` 인수는 기본 제공 JSON 직렬 변환기를 사용 하 여 직렬화 되 고에 저장 됩니다는 `params.data` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-159">The received `UserName` argument is serialized using the built-in JSON serializer and is stored in the `params.data` object.</span></span> <span data-ttu-id="e5ed5-160">다음 예제의 Angular, 데이터 내에서 개인 설정 된 인사말을 생성 하는 데 사용 된 `h1` 요소:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-160">In the following Angular example, the data is used to construct a personalized greeting within an `h1` element:</span></span>

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,38-52,79-)]

<span data-ttu-id="e5ed5-161">참고: 태그 도우미에 전달 된 속성 이름으로 표시 됩니다 **PascalCase** 표기법입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-161">Note: Property names passed in Tag Helpers are represented with **PascalCase** notation.</span></span> <span data-ttu-id="e5ed5-162">JavaScript에서 동일한 속성 이름으로 표시 됩니다는 위치와 달리 **camelCase**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-162">Contrast that to JavaScript, where the same property names are represented with **camelCase**.</span></span> <span data-ttu-id="e5ed5-163">기본 JSON serialization 구성이이 차이 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-163">The default JSON serialization configuration is responsible for this difference.</span></span>

<span data-ttu-id="e5ed5-164">시 앞의 코드 예제를 확장 하려면 데이터로 전달할 수는 서버에서 보기로 hydrating 합니다 `globals` 속성에 제공 되는 `resolve` 함수:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-164">To expand upon the preceding code example, data can be passed from the server to the view by hydrating the `globals` property provided to the `resolve` function:</span></span>

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,57-77,79-)]

<span data-ttu-id="e5ed5-165">`postList` 배열 내에 정의 된 `globals` 개체는 전역 브라우저의 연결 된 `window` 개체.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-165">The `postList` array defined inside the `globals` object is attached to the browser's global `window` object.</span></span> <span data-ttu-id="e5ed5-166">전역 범위에이 변수 호이스팅 제거 일일이, 특히 서버에서 한 번 및 클라이언트에서 다시 동일한 데이터를 로드 하는 관련 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-166">This variable hoisting to global scope eliminates duplication of effort, particularly as it pertains to loading the same data once on the server and again on the client.</span></span>

![창 개체에 연결 된 전역 postList 변수](spa-services/_static/global_variable.png)

<a name="webpack-dev-middleware"></a>

## <a name="webpack-dev-middleware"></a><span data-ttu-id="e5ed5-168">Webpack 개발 미들웨어</span><span class="sxs-lookup"><span data-stu-id="e5ed5-168">Webpack Dev Middleware</span></span>

<span data-ttu-id="e5ed5-169">[Webpack 개발 미들웨어](https://webpack.github.io/docs/webpack-dev-middleware.html) Webpack 주문형 리소스를 작성 하는 반면 간소화 된 개발 워크플로 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-169">[Webpack Dev Middleware](https://webpack.github.io/docs/webpack-dev-middleware.html) introduces a streamlined development workflow whereby Webpack builds resources on demand.</span></span> <span data-ttu-id="e5ed5-170">미들웨어가 자동으로 컴파일하고 브라우저에서 페이지를 다시 로드 되 면 클라이언트 쪽 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-170">The middleware automatically compiles and serves client-side resources when a page is reloaded in the browser.</span></span> <span data-ttu-id="e5ed5-171">대체 방법은 타사 종속성 또는 사용자 지정 코드를 변경 하는 경우 프로젝트의 npm 빌드 스크립트를 통해 Webpack를 수동으로 호출할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-171">The alternate approach is to manually invoke Webpack via the project's npm build script when a third-party dependency or the custom code changes.</span></span> <span data-ttu-id="e5ed5-172">Npm에서 스크립트를 작성 합니다 *package.json* 파일 다음 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-172">An npm build script in the *package.json* file is shown in the following example:</span></span>

```json
"build": "npm run build:vendor && npm run build:custom",
```

### <a name="prerequisites"></a><span data-ttu-id="e5ed5-173">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e5ed5-173">Prerequisites</span></span>

<span data-ttu-id="e5ed5-174">다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-174">Install the following:</span></span>

* <span data-ttu-id="e5ed5-175">[aspnet webpack](https://www.npmjs.com/package/aspnet-webpack) npm 패키지:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-175">[aspnet-webpack](https://www.npmjs.com/package/aspnet-webpack) npm package:</span></span>

    ```console
    npm i -D aspnet-webpack
    ```

### <a name="configuration"></a><span data-ttu-id="e5ed5-176">구성</span><span class="sxs-lookup"><span data-stu-id="e5ed5-176">Configuration</span></span>

<span data-ttu-id="e5ed5-177">Webpack 개발 미들웨어에서 다음 코드를 통해 HTTP 요청 파이프라인에 등록 합니다 *Startup.cs* 파일의 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-177">Webpack Dev Middleware is registered into the HTTP request pipeline via the following code in the *Startup.cs* file's `Configure` method:</span></span>

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=webpack-middleware-registration&highlight=4)]

<span data-ttu-id="e5ed5-178">합니다 `UseWebpackDevMiddleware` 확장 메서드를 호출 하기 전에 [정적 파일 호스팅 등록](xref:fundamentals/static-files) 를 통해는 `UseStaticFiles` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-178">The `UseWebpackDevMiddleware` extension method must be called before [registering static file hosting](xref:fundamentals/static-files) via the `UseStaticFiles` extension method.</span></span> <span data-ttu-id="e5ed5-179">보안상의 이유로 앱이 개발 모드에서 실행 하는 경우에 미들웨어를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-179">For security reasons, register the middleware only when the app runs in development mode.</span></span>

<span data-ttu-id="e5ed5-180">합니다 *webpack.config.js* 파일의 `output.publicPath` 속성에 시청 하도록 미들웨어에 지시 합니다 `dist` 변경에 대 한 폴더:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-180">The *webpack.config.js* file's `output.publicPath` property tells the middleware to watch the `dist` folder for changes:</span></span>

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,13-16)]

<a name="hot-module-replacement"></a>

## <a name="hot-module-replacement"></a><span data-ttu-id="e5ed5-181">핫 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="e5ed5-181">Hot Module Replacement</span></span>

<span data-ttu-id="e5ed5-182">Webpack의 생각할 [핫 모듈 교체](https://webpack.js.org/concepts/hot-module-replacement/) 진화 한 것으로 (HMR) 기능 [Webpack 개발 미들웨어](#webpack-dev-middleware)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-182">Think of Webpack's [Hot Module Replacement](https://webpack.js.org/concepts/hot-module-replacement/) (HMR) feature as an evolution of [Webpack Dev Middleware](#webpack-dev-middleware).</span></span> <span data-ttu-id="e5ed5-183">HMR 혜택을 모두 동일한을 소개 하지만 추가 변경 내용을 컴파일한 후 페이지 콘텐츠를 자동으로 업데이트 하 여 개발 워크플로 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-183">HMR introduces all the same benefits, but it further streamlines the development workflow by automatically updating page content after compiling the changes.</span></span> <span data-ttu-id="e5ed5-184">현재 메모리 상태 및 SPA의 디버깅 세션을 사용 하 여 방해 하 게 브라우저의 새로 고침을 사용 하 여이 혼동 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-184">Don't confuse this with a refresh of the browser, which would interfere with the current in-memory state and debugging session of the SPA.</span></span> <span data-ttu-id="e5ed5-185">Webpack 개발 미들웨어 서비스 및 브라우저에 변경 내용이 푸시 즉 브라우저 간에 실시간 연결 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-185">There's a live link between the Webpack Dev Middleware service and the browser, which means changes are pushed to the browser.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e5ed5-186">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e5ed5-186">Prerequisites</span></span>

<span data-ttu-id="e5ed5-187">다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-187">Install the following:</span></span>

* <span data-ttu-id="e5ed5-188">[webpack 실행 부하 과다 미들웨어](https://www.npmjs.com/package/webpack-hot-middleware) npm 패키지:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-188">[webpack-hot-middleware](https://www.npmjs.com/package/webpack-hot-middleware) npm package:</span></span>

    ```console
    npm i -D webpack-hot-middleware
    ```

### <a name="configuration"></a><span data-ttu-id="e5ed5-189">구성</span><span class="sxs-lookup"><span data-stu-id="e5ed5-189">Configuration</span></span>

<span data-ttu-id="e5ed5-190">HMR 구성 요소에서 MVC의 HTTP 요청 파이프라인에 등록 해야 합니다는 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-190">The HMR component must be registered into MVC's HTTP request pipeline in the `Configure` method:</span></span>

```csharp
app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions {
    HotModuleReplacement = true
});
```

<span data-ttu-id="e5ed5-191">가 사용 하 여 true로 [Webpack 개발 미들웨어](#webpack-dev-middleware)의 `UseWebpackDevMiddleware` 확장 메서드를 호출 하기 전에 `UseStaticFiles` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-191">As was true with [Webpack Dev Middleware](#webpack-dev-middleware), the `UseWebpackDevMiddleware` extension method must be called before the `UseStaticFiles` extension method.</span></span> <span data-ttu-id="e5ed5-192">보안상의 이유로 앱이 개발 모드에서 실행 하는 경우에 미들웨어를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-192">For security reasons, register the middleware only when the app runs in development mode.</span></span>

<span data-ttu-id="e5ed5-193">합니다 *webpack.config.js* 파일을 정의 해야 합니다는 `plugins` 비워 두면 하는 경우에 배열:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-193">The *webpack.config.js* file must define a `plugins` array, even if it's left empty:</span></span>

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,25)]

<span data-ttu-id="e5ed5-194">브라우저에서 앱을 로드 한 후 개발자 도구 콘솔 탭 HMR 활성화에 대 한 확인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-194">After loading the app in the browser, the developer tools' Console tab provides confirmation of HMR activation:</span></span>

![핫 모듈 교체 연결 된 메시지](spa-services/_static/hmr_connected.png)

<a name="routing-helpers"></a>

## <a name="routing-helpers"></a><span data-ttu-id="e5ed5-196">라우팅 도우미</span><span class="sxs-lookup"><span data-stu-id="e5ed5-196">Routing helpers</span></span>

<span data-ttu-id="e5ed5-197">대부분의 ASP.NET Core 기반 Spa 서버 쪽 라우팅 외에도 클라이언트 쪽 라우팅을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-197">In most ASP.NET Core-based SPAs, you'll want client-side routing in addition to server-side routing.</span></span> <span data-ttu-id="e5ed5-198">SPA 및 MVC 라우팅 시스템 간섭 하지 않고 독립적으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-198">The SPA and MVC routing systems can work independently without interference.</span></span> <span data-ttu-id="e5ed5-199">그러나 방법이, 문제 하나에 지 사례 해답: 404 HTTP 응답을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-199">There's, however, one edge case posing challenges: identifying 404 HTTP responses.</span></span>

<span data-ttu-id="e5ed5-200">있는 경우를 생각해 볼의 확장명 없는 경로 `/some/page` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-200">Consider the scenario in which an extensionless route of `/some/page` is used.</span></span> <span data-ttu-id="e5ed5-201">요청 하지 패턴 일치는 서버 쪽 경로 하지만 해당 패턴에는 클라이언트 쪽 경로 맞지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-201">Assume the request doesn't pattern-match a server-side route, but its pattern does match a client-side route.</span></span> <span data-ttu-id="e5ed5-202">에 대 한 들어오는 요청을 살펴보겠습니다 `/images/user-512.png`, 일반적으로 서버의 이미지 파일을 찾으려고 시도입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-202">Now consider an incoming request for `/images/user-512.png`, which generally expects to find an image file on the server.</span></span> <span data-ttu-id="e5ed5-203">클라이언트 쪽 응용 프로그램에서 처리는 그럴 가능성은 요청 된 리소스 경로는 모든 서버 쪽 경로 또는 정적 파일와 일치 하지 않으면,-일반적으로 404 HTTP 상태 코드를 반환 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-203">If that requested resource path doesn't match any server-side route or static file, it's unlikely that the client-side application would handle it — you generally want to return a 404 HTTP status code.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e5ed5-204">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e5ed5-204">Prerequisites</span></span>

<span data-ttu-id="e5ed5-205">다음을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-205">Install the following:</span></span>

* <span data-ttu-id="e5ed5-206">클라이언트 쪽 라우팅 npm 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-206">The client-side routing npm package.</span></span> <span data-ttu-id="e5ed5-207">예를 들어 Angular를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-207">Using Angular as an example:</span></span>

    ```console
    npm i -S @angular/router
    ```

### <a name="configuration"></a><span data-ttu-id="e5ed5-208">구성</span><span class="sxs-lookup"><span data-stu-id="e5ed5-208">Configuration</span></span>

<span data-ttu-id="e5ed5-209">라는 확장 메서드 `MapSpaFallbackRoute` 에 사용 되는 `Configure` 메서드:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-209">An extension method named `MapSpaFallbackRoute` is used in the `Configure` method:</span></span>

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=mvc-routing-table&highlight=7-9)]

<span data-ttu-id="e5ed5-210">팁: 경로 구성 하는 순서 대로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-210">Tip: Routes are evaluated in the order in which they're configured.</span></span> <span data-ttu-id="e5ed5-211">결과적으로 `default` 패턴 일치를 위해 이전 코드 예제의 경로 먼저 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-211">Consequently, the `default` route in the preceding code example is used first for pattern matching.</span></span>

<a name="new-project-creation"></a>

## <a name="creating-a-new-project"></a><span data-ttu-id="e5ed5-212">새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e5ed5-212">Creating a new project</span></span>

<span data-ttu-id="e5ed5-213">JavaScriptServices에 미리 구성 된 응용 프로그램 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-213">JavaScriptServices provides pre-configured application templates.</span></span> <span data-ttu-id="e5ed5-214">SpaServices 다양 한 프레임 워크 및 Angular, React 및 Redux 등의 라이브러리와 함께에서 이러한 템플릿에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-214">SpaServices is used in these templates, in conjunction with different frameworks and libraries such as Angular, React, and Redux.</span></span>

<span data-ttu-id="e5ed5-215">이러한 템플릿은 다음 명령을 실행 하 여.NET Core CLI를 통해 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-215">These templates can be installed via the .NET Core CLI by running the following command:</span></span>

```console
dotnet new --install Microsoft.AspNetCore.SpaTemplates::*
```

<span data-ttu-id="e5ed5-216">사용 가능한 SPA 템플릿 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-216">A list of available SPA templates is displayed:</span></span>

| <span data-ttu-id="e5ed5-217">템플릿</span><span class="sxs-lookup"><span data-stu-id="e5ed5-217">Templates</span></span>                                 | <span data-ttu-id="e5ed5-218">짧은 이름</span><span class="sxs-lookup"><span data-stu-id="e5ed5-218">Short Name</span></span> | <span data-ttu-id="e5ed5-219">언어</span><span class="sxs-lookup"><span data-stu-id="e5ed5-219">Language</span></span> | <span data-ttu-id="e5ed5-220">Tags</span><span class="sxs-lookup"><span data-stu-id="e5ed5-220">Tags</span></span>        |
|:------------------------------------------|:-----------|:---------|:------------|
| <span data-ttu-id="e5ed5-221">Angular를 사용 하 여 ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="e5ed5-221">MVC ASP.NET Core with Angular</span></span>             | <span data-ttu-id="e5ed5-222">angular</span><span class="sxs-lookup"><span data-stu-id="e5ed5-222">angular</span></span>    | <span data-ttu-id="e5ed5-223">[C#]</span><span class="sxs-lookup"><span data-stu-id="e5ed5-223">[C#]</span></span>     | <span data-ttu-id="e5ed5-224">웹/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="e5ed5-224">Web/MVC/SPA</span></span> |
| <span data-ttu-id="e5ed5-225">MVC ASP.NET Core (react.js 사용)</span><span class="sxs-lookup"><span data-stu-id="e5ed5-225">MVC ASP.NET Core with React.js</span></span>            | <span data-ttu-id="e5ed5-226">react</span><span class="sxs-lookup"><span data-stu-id="e5ed5-226">react</span></span>      | <span data-ttu-id="e5ed5-227">[C#]</span><span class="sxs-lookup"><span data-stu-id="e5ed5-227">[C#]</span></span>     | <span data-ttu-id="e5ed5-228">웹/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="e5ed5-228">Web/MVC/SPA</span></span> |
| <span data-ttu-id="e5ed5-229">React.js 및 Redux MVC ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e5ed5-229">MVC ASP.NET Core with React.js and Redux</span></span>  | <span data-ttu-id="e5ed5-230">reactredux</span><span class="sxs-lookup"><span data-stu-id="e5ed5-230">reactredux</span></span> | <span data-ttu-id="e5ed5-231">[C#]</span><span class="sxs-lookup"><span data-stu-id="e5ed5-231">[C#]</span></span>     | <span data-ttu-id="e5ed5-232">웹/MVC/SPA</span><span class="sxs-lookup"><span data-stu-id="e5ed5-232">Web/MVC/SPA</span></span> |

<span data-ttu-id="e5ed5-233">SPA 템플릿 중 하나를 사용 하 여 새 프로젝트를 만들려면 다음을 포함 합니다 **약식 이름** 에서 템플릿의 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-233">To create a new project using one of the SPA templates, include the **Short Name** of the template in the [dotnet new](/dotnet/core/tools/dotnet-new) command.</span></span> <span data-ttu-id="e5ed5-234">다음 명령은 서버 쪽에 대해 구성 된 ASP.NET Core MVC를 사용 하 여 Angular 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-234">The following command creates an Angular application with ASP.NET Core MVC configured for the server side:</span></span>

```console
dotnet new angular
```

<a name="runtime-config-mode"></a>

### <a name="set-the-runtime-configuration-mode"></a><span data-ttu-id="e5ed5-235">런타임 구성 모드 설정</span><span class="sxs-lookup"><span data-stu-id="e5ed5-235">Set the runtime configuration mode</span></span>

<span data-ttu-id="e5ed5-236">다음과 같은 두 가지 기본 런타임 구성 모드</span><span class="sxs-lookup"><span data-stu-id="e5ed5-236">Two primary runtime configuration modes exist:</span></span>

* <span data-ttu-id="e5ed5-237">**개발**:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-237">**Development**:</span></span>
  * <span data-ttu-id="e5ed5-238">디버깅을 쉽게 수행 하려면 소스 맵이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-238">Includes source maps to ease debugging.</span></span>
  * <span data-ttu-id="e5ed5-239">성능에 대 한 클라이언트 쪽 코드를 최적화 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-239">Doesn't optimize the client-side code for performance.</span></span>
* <span data-ttu-id="e5ed5-240">**프로덕션**:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-240">**Production**:</span></span>
  * <span data-ttu-id="e5ed5-241">소스 맵 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-241">Excludes source maps.</span></span>
  * <span data-ttu-id="e5ed5-242">묶음 및 축소를 통해 클라이언트 쪽 코드를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-242">Optimizes the client-side code via bundling & minification.</span></span>

<span data-ttu-id="e5ed5-243">ASP.NET Core 라는 환경 변수를 사용 하 여 `ASPNETCORE_ENVIRONMENT` 구성 모드를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-243">ASP.NET Core uses an environment variable named `ASPNETCORE_ENVIRONMENT` to store the configuration mode.</span></span> <span data-ttu-id="e5ed5-244">참조 **[환경을 설정할](xref:fundamentals/environments#set-the-environment)** 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-244">See **[Set the environment](xref:fundamentals/environments#set-the-environment)** for more information.</span></span>

### <a name="running-with-net-core-cli"></a><span data-ttu-id="e5ed5-245">.NET Core CLI 사용 하 여 실행</span><span class="sxs-lookup"><span data-stu-id="e5ed5-245">Running with .NET Core CLI</span></span>

<span data-ttu-id="e5ed5-246">프로젝트 루트에서 다음 명령을 실행 하 여 필요한 NuGet 및 npm 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-246">Restore the required NuGet and npm packages by running the following command at the project root:</span></span>

```console
dotnet restore && npm i
```

<span data-ttu-id="e5ed5-247">빌드 및 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-247">Build and run the application:</span></span>

```console
dotnet run
```

<span data-ttu-id="e5ed5-248">Localhost에 따라 응용 프로그램을 시작 합니다 [런타임 구성 모드](#runtime-config-mode)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-248">The application starts on localhost according to the [runtime configuration mode](#runtime-config-mode).</span></span> <span data-ttu-id="e5ed5-249">이동할 `http://localhost:5000` 브라우저에서 방문 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-249">Navigating to `http://localhost:5000` in the browser displays the landing page.</span></span>

### <a name="running-with-visual-studio-2017"></a><span data-ttu-id="e5ed5-250">Visual Studio 2017을 사용 하 여 실행</span><span class="sxs-lookup"><span data-stu-id="e5ed5-250">Running with Visual Studio 2017</span></span>

<span data-ttu-id="e5ed5-251">열기는 *.csproj* 에서 생성 된 파일을 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-251">Open the *.csproj* file generated by the [dotnet new](/dotnet/core/tools/dotnet-new) command.</span></span> <span data-ttu-id="e5ed5-252">프로젝트를 열고 시 필요한 NuGet 및 npm 패키지를 자동으로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-252">The required NuGet and npm packages are restored automatically upon project open.</span></span> <span data-ttu-id="e5ed5-253">이 복원 프로세스는 몇 분 정도 걸릴 수 있습니다 하 고 응용 프로그램은 작업이 완료 될 때 실행 하도록 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-253">This restoration process may take up to a few minutes, and the application is ready to run when it completes.</span></span> <span data-ttu-id="e5ed5-254">누르거나 녹색 실행된 단추를 클릭 `Ctrl + F5`, 브라우저 응용 프로그램의 방문 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-254">Click the green run button or press `Ctrl + F5`, and the browser opens to the application's landing page.</span></span> <span data-ttu-id="e5ed5-255">Localhost에 따라 응용 프로그램을 실행 합니다 [런타임 구성 모드](#runtime-config-mode)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-255">The application runs on localhost according to the [runtime configuration mode](#runtime-config-mode).</span></span>

<a name="app-testing"></a>

## <a name="testing-the-app"></a><span data-ttu-id="e5ed5-256">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="e5ed5-256">Testing the app</span></span>

<span data-ttu-id="e5ed5-257">SpaServices 템플릿은 사용 하 여 클라이언트 쪽 테스트를 실행 하도록 미리 구성 [Karma](https://karma-runner.github.io/1.0/index.html) 하 고 [Jasmine](https://jasmine.github.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-257">SpaServices templates are pre-configured to run client-side tests using [Karma](https://karma-runner.github.io/1.0/index.html) and [Jasmine](https://jasmine.github.io/).</span></span> <span data-ttu-id="e5ed5-258">Karma test runner를 해당 테스트는 jasmine는 JavaScript에 대 한 테스트 프레임 워크 인기 있는 단위.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-258">Jasmine is a popular unit testing framework for JavaScript, whereas Karma is a test runner for those tests.</span></span> <span data-ttu-id="e5ed5-259">Karma과 작동 하도록 구성 되는 [Webpack 개발 미들웨어](#webpack-dev-middleware) 는 개발자 중지 될 때마다 변경 내용이 테스트를 실행 하는 데 필요한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-259">Karma is configured to work with the [Webpack Dev Middleware](#webpack-dev-middleware) such that the developer isn't required to stop and run the test every time changes are made.</span></span> <span data-ttu-id="e5ed5-260">테스트 사례 또는 테스트 사례 자체에 대해 실행 되는 코드 인지 자동 테스트 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-260">Whether it's the code running against the test case or the test case itself, the test runs automatically.</span></span>

<span data-ttu-id="e5ed5-261">Angular 응용 프로그램을 사용 하 여 예를 들어, Jasmine 두 개의 테스트 사례는 아직 제공 합니다 `CounterComponent` 에 *counter.component.spec.ts* 파일:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-261">Using the Angular application as an example, two Jasmine test cases are already provided for the `CounterComponent` in the *counter.component.spec.ts* file:</span></span>

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/app/components/counter/counter.component.spec.ts?range=15-28)]

<span data-ttu-id="e5ed5-262">명령 프롬프트를 열고 합니다 *ClientApp* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-262">Open the command prompt in the *ClientApp* directory.</span></span> <span data-ttu-id="e5ed5-263">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-263">Run the following command:</span></span>

```console
npm test
```

<span data-ttu-id="e5ed5-264">스크립트에 정의 된 설정을 읽어 Karma test runner를 시작 합니다 *karma.conf.js* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-264">The script launches the Karma test runner, which reads the settings defined in the *karma.conf.js* file.</span></span> <span data-ttu-id="e5ed5-265">기타 설정 합니다 *karma.conf.js* 식별을 통해 실행할 테스트 파일을 해당 `files` 배열:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-265">Among other settings, the *karma.conf.js* identifies the test files to be executed via its `files` array:</span></span>

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/test/karma.conf.js?range=4-5,8-11)]

<a name="app-publishing"></a>

## <a name="publishing-the-application"></a><span data-ttu-id="e5ed5-266">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="e5ed5-266">Publishing the application</span></span>

<span data-ttu-id="e5ed5-267">배포 준비 패키지로 생성 된 클라이언트 쪽 자산 및 게시 된 ASP.NET Core 아티팩트를 결합 하는 것은 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-267">Combining the generated client-side assets and the published ASP.NET Core artifacts into a ready-to-deploy package can be cumbersome.</span></span> <span data-ttu-id="e5ed5-268">SpaServices 라는 사용자 지정 MSBuild 대상을 사용 하 여 전체 게시 프로세스를 오케스트레이션 하는 다행 스럽게도 `RunWebpack`:</span><span class="sxs-lookup"><span data-stu-id="e5ed5-268">Thankfully, SpaServices orchestrates that entire publication process with a custom MSBuild target named `RunWebpack`:</span></span>

[!code-xml[](../client-side/spa-services/sample/SpaServicesSampleApp/SpaServicesSampleApp.csproj?range=31-45)]

<span data-ttu-id="e5ed5-269">MSBuild 대상에는 다음 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-269">The MSBuild target has the following responsibilities:</span></span>

1. <span data-ttu-id="e5ed5-270">Npm 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-270">Restore the npm packages</span></span>
1. <span data-ttu-id="e5ed5-271">제 3 자, 클라이언트 쪽 자산 프로덕션 급 빌드 만들기</span><span class="sxs-lookup"><span data-stu-id="e5ed5-271">Create a production-grade build of the third-party, client-side assets</span></span>
1. <span data-ttu-id="e5ed5-272">프로덕션 급 빌드 사용자 지정 클라이언트 쪽 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="e5ed5-272">Create a production-grade build of the custom client-side assets</span></span>
1. <span data-ttu-id="e5ed5-273">Webpack에서 생성 된 자산을 게시 폴더에 복사</span><span class="sxs-lookup"><span data-stu-id="e5ed5-273">Copy the Webpack-generated assets to the publish folder</span></span>

<span data-ttu-id="e5ed5-274">MSBuild 대상 실행 하는 경우 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5ed5-274">The MSBuild target is invoked when running:</span></span>

```console
dotnet publish -c Release
```

## <a name="additional-resources"></a><span data-ttu-id="e5ed5-275">추가 자료</span><span class="sxs-lookup"><span data-stu-id="e5ed5-275">Additional resources</span></span>

* [<span data-ttu-id="e5ed5-276">Angular Docs</span><span class="sxs-lookup"><span data-stu-id="e5ed5-276">Angular Docs</span></span>](https://angular.io/docs)
