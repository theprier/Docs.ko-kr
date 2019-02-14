---
title: TypeScript 및 WebPack과 함께 ASP.NET Core SignalR 사용
author: ssougnez
description: 이 자습서에서는 해당 클라이언트가 TypeScript로 작성된 ASP.NET Core SignalR 웹앱을 번들링 및 빌드하도록 WebPack을 구성합니다.
ms.author: bradyg
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/signalr-typescript-webpack
ms.openlocfilehash: aaf9aa59928ed6b17bc0586d97dbdefc9e30362c
ms.sourcegitcommit: 5e3797a02ff3c48bb8cb9ad4320bfd169ebe8aba
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56102954"
---
# <a name="use-aspnet-core-signalr-with-typescript-and-webpack"></a><span data-ttu-id="364f9-103">TypeScript 및 WebPack과 함께 ASP.NET Core SignalR 사용</span><span class="sxs-lookup"><span data-stu-id="364f9-103">Use ASP.NET Core SignalR with TypeScript and Webpack</span></span>

<span data-ttu-id="364f9-104">작성자: [Sébastien Sougnez](https://twitter.com/ssougnez) 및 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="364f9-104">By [Sébastien Sougnez](https://twitter.com/ssougnez) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="364f9-105">[WebPack](https://webpack.js.org/)을 사용하여 개발자가 웹앱의 클라이언트 쪽 리소스를 번들링 및 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-105">[Webpack](https://webpack.js.org/) enables developers to bundle and build the client-side resources of a web app.</span></span> <span data-ttu-id="364f9-106">본 자습서에서는 클라이언트가 [TypeScript](https://www.typescriptlang.org/)로 작성된 ASP.NET Core SignalR 웹앱에서 WebPack을 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-106">This tutorial demonstrates using Webpack in an ASP.NET Core SignalR web app whose client is written in [TypeScript](https://www.typescriptlang.org/).</span></span>

<span data-ttu-id="364f9-107">이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="364f9-108">ASP.NET Core SignalR 앱 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="364f9-108">Scaffold a starter ASP.NET Core SignalR app</span></span>
> * <span data-ttu-id="364f9-109">SignalR TypeScript 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="364f9-109">Configure the SignalR TypeScript client</span></span>
> * <span data-ttu-id="364f9-110">WebPack을 사용하여 빌드 파이프라인 구성</span><span class="sxs-lookup"><span data-stu-id="364f9-110">Configure a build pipeline using Webpack</span></span>
> * <span data-ttu-id="364f9-111">SignalR 서버 구성</span><span class="sxs-lookup"><span data-stu-id="364f9-111">Configure the SignalR server</span></span>
> * <span data-ttu-id="364f9-112">클라이언트 및 서버 간 통신 활성화</span><span class="sxs-lookup"><span data-stu-id="364f9-112">Enable communication between client and server</span></span>

<span data-ttu-id="364f9-113">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr-typescript-webpack/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="364f9-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr-typescript-webpack/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-vs-vsc-2.2.md)]

## <a name="create-the-aspnet-core-web-app"></a><span data-ttu-id="364f9-114">ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="364f9-114">Create the ASP.NET Core web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="364f9-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="364f9-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="364f9-116">*PATH* 환경 변수에서 npm을 찾도록 Visual Studio를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-116">Configure Visual Studio to look for npm in the *PATH* environment variable.</span></span> <span data-ttu-id="364f9-117">기본적으로 Visual Studio는 설치 디렉터리에 있는 npm의 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-117">By default, Visual Studio uses the version of npm found in its installation directory.</span></span> <span data-ttu-id="364f9-118">Visual Studio에서 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-118">Follow these instructions in Visual Studio:</span></span>

1. <span data-ttu-id="364f9-119">**도구** > **옵션** > **프로젝트 및 솔루션** > **웹 패키지 관리** > **외부 웹 도구**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-119">Navigate to **Tools** > **Options** > **Projects and Solutions** > **Web Package Management** > **External Web Tools**.</span></span>
1. <span data-ttu-id="364f9-120">목록에서 *$(PATH)* 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-120">Select the *$(PATH)* entry from the list.</span></span> <span data-ttu-id="364f9-121">위쪽 화살표를 클릭하여 이 항목을 목록의 두 번째 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-121">Click the up arrow to move the entry to the second position in the list.</span></span>

    ![Visual Studio 구성](signalr-typescript-webpack/_static/signalr-configure-path-visual-studio.png)

<span data-ttu-id="364f9-123">Visual Studio 구성이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-123">Visual Studio configuration is completed.</span></span> <span data-ttu-id="364f9-124">이제 프로젝트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-124">It's time to create the project.</span></span>

1. <span data-ttu-id="364f9-125">**파일** > **새로 만들기** > **프로젝트** 메뉴 옵션을 사용하고 **ASP.NET Core 웹 애플리케이션** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-125">Use the **File** > **New** > **Project** menu option and choose the **ASP.NET Core Web Application** template.</span></span>
1. <span data-ttu-id="364f9-126">프로젝트의 이름을 *SignalRWebPack*으로 지정하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-126">Name the project *SignalRWebPack*, and select **OK**.</span></span>
1. <span data-ttu-id="364f9-127">대상 프레임워크 드롭다운에서 *.NET Core*를 선택하고, 프레임워크 선택기 드롭다운에서 *ASP.NET Core 2.2*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-127">Select *.NET Core* from the target framework drop-down, and select *ASP.NET Core 2.2* from the framework selector drop-down.</span></span> <span data-ttu-id="364f9-128">**빈** 템플릿을 선택하고, **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-128">Select the **Empty** template, and select **OK**.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="364f9-129">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="364f9-129">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="364f9-130">**통합 터미널**에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-130">Run the following command in the **Integrated Terminal**:</span></span>

```console
dotnet new web -o SignalRWebPack
```

<span data-ttu-id="364f9-131">.NET Core를 대상으로 하는 빈 ASP.NET Core 웹앱이 *SignalRWebPack* 디렉터리에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-131">An empty ASP.NET Core web app, targeting .NET Core, is created in a *SignalRWebPack* directory.</span></span>

---

## <a name="configure-webpack-and-typescript"></a><span data-ttu-id="364f9-132">WebPack 및 TypeScript 구성</span><span class="sxs-lookup"><span data-stu-id="364f9-132">Configure Webpack and TypeScript</span></span>

<span data-ttu-id="364f9-133">다음 단계에서는 TypeScript에서 JavaScript로 변환 및 클라이언트 쪽 리소스의 번들링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-133">The following steps configure the conversion of TypeScript to JavaScript and the bundling of client-side resources.</span></span>

1. <span data-ttu-id="364f9-134">프로젝트 루트에서 다음 명령을 실행하여 *package.json* 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-134">Execute the following command in the project root to create a *package.json* file:</span></span>

    ```console
    npm init -y
    ```

1. <span data-ttu-id="364f9-135">강조 표시된 속성을 *package.json* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-135">Add the highlighted property to the *package.json* file:</span></span>

    [!code-json[package.json](signalr-typescript-webpack/sample/snippets/package1.json?highlight=4)]

    <span data-ttu-id="364f9-136">`private` 속성을 `true`로 설정하면 다음 단계에서 패키지 설치 경고가 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-136">Setting the `private` property to `true` prevents package installation warnings in the next step.</span></span>

1. <span data-ttu-id="364f9-137">필요한 npm 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-137">Install the required npm packages.</span></span> <span data-ttu-id="364f9-138">프로젝트 루트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-138">Execute the following command from the project root:</span></span>

    ```console
    npm install -D -E clean-webpack-plugin@1.0.1 css-loader@2.1.0 html-webpack-plugin@4.0.0-beta.5 mini-css-extract-plugin@0.5.0 ts-loader@5.3.3 typescript@3.3.3 webpack@4.29.3 webpack-cli@3.2.3
    ```

    <span data-ttu-id="364f9-139">참고할 몇몇 명령 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="364f9-139">Some command details to note:</span></span>

    * <span data-ttu-id="364f9-140">버전 번호는 각 패키지 이름에 대해 `@` 부호 뒤에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-140">A version number follows the `@` sign for each package name.</span></span> <span data-ttu-id="364f9-141">npm은 해당 특정 패키지 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-141">npm installs those specific package versions.</span></span>
    * <span data-ttu-id="364f9-142">`-E` 옵션은 [유의적 버전](https://semver.org/) 범위 연산자를 *package.json*에 쓰는 npm의 기본 동작을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-142">The `-E` option disables npm's default behavior of writing [semantic versioning](https://semver.org/) range operators to *package.json*.</span></span> <span data-ttu-id="364f9-143">예를 들어 `"webpack": "^4.29.3"` 대신 `"webpack": "4.29.3"`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-143">For example, `"webpack": "4.29.3"` is used instead of `"webpack": "^4.29.3"`.</span></span> <span data-ttu-id="364f9-144">이 옵션은 최신 패키지 버전으로 의도하지 않은 업그레이드를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-144">This option prevents unintended upgrades to newer package versions.</span></span>

    <span data-ttu-id="364f9-145">자세한 내용은 [npm-install](https://docs.npmjs.com/cli/install) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364f9-145">See the official [npm-install](https://docs.npmjs.com/cli/install) docs for more detail.</span></span>

1. <span data-ttu-id="364f9-146">*package.json* 파일의 `scripts` 속성을 다음 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-146">Replace the `scripts` property of the *package.json* file with the following snippet:</span></span>

    ```json
    "scripts": {
      "build": "webpack --mode=development --watch",
      "release": "webpack --mode=production",
      "publish": "npm run release && dotnet publish -c Release"
    },
    ```

    <span data-ttu-id="364f9-147">스크립트에 대한 간략한 설명:</span><span class="sxs-lookup"><span data-stu-id="364f9-147">Some explanation of the scripts:</span></span>

    * <span data-ttu-id="364f9-148">`build`: 개발 모드에서 클라이언트 쪽 리소스를 번들링하고 파일 변경을 감시합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-148">`build`: Bundles your client-side resources in development mode and watches for file changes.</span></span> <span data-ttu-id="364f9-149">파일 감시자는 프로젝트 파일이 변경될 때마다 번들이 다시 생성되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-149">The file watcher causes the bundle to regenerate each time a project file changes.</span></span> <span data-ttu-id="364f9-150">`mode` 옵션은 프로덕션 최적화(예: 트리 셰이킹 및 축소)를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-150">The `mode` option disables production optimizations, such as tree shaking and minification.</span></span> <span data-ttu-id="364f9-151">개발 시에는 `build`만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-151">Only use `build` in development.</span></span>
    * <span data-ttu-id="364f9-152">`release`: 프로덕션 모드에서 클라이언트 쪽 리소스를 번들링합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-152">`release`: Bundles your client-side resources in production mode.</span></span>
    * <span data-ttu-id="364f9-153">`publish`: 프로덕션 모드에서 `release` 스크립트를 실행하여 클라이언트 쪽 리소스를 번들링합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-153">`publish`: Runs the `release` script to bundle the client-side resources in production mode.</span></span> <span data-ttu-id="364f9-154">이는 .NET Core CLI의 [publish](/dotnet/core/tools/dotnet-publish) 명령을 호출하여 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-154">It calls the .NET Core CLI's [publish](/dotnet/core/tools/dotnet-publish) command to publish the app.</span></span>

1. <span data-ttu-id="364f9-155">프로젝트 루트에 다음 내용을 포함한 *webpack.config.js*라는 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-155">Create a file named *webpack.config.js*, in the project root, with the following content:</span></span>

    [!code-javascript[webpack.config.js](signalr-typescript-webpack/sample/webpack.config.js)]

    <span data-ttu-id="364f9-156">앞의 파일은 WebPack 컴파일을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-156">The preceding file configures the Webpack compilation.</span></span> <span data-ttu-id="364f9-157">참고할 일부 구성 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="364f9-157">Some configuration details to note:</span></span>

    * <span data-ttu-id="364f9-158">`output` 속성은 *dist*의 기본값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-158">The `output` property overrides the default value of *dist*.</span></span> <span data-ttu-id="364f9-159">번들은 *wwwroot* 디렉터리에 대신 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-159">The bundle is instead emitted in the *wwwroot* directory.</span></span>
    * <span data-ttu-id="364f9-160">`resolve.extensions` 배열은 SignalR 클라이언트 JavaScript를 가져오기 위한 *.js*를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-160">The `resolve.extensions` array includes *.js* to import the SignalR client JavaScript.</span></span>

1. <span data-ttu-id="364f9-161">프로젝트 루트에 새 *src* 디렉터리를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-161">Create a new *src* directory in the project root.</span></span> <span data-ttu-id="364f9-162">그 목적은 프로젝트의 클라이언트 쪽 자산을 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-162">Its purpose is to store the project's client-side assets.</span></span>

1. <span data-ttu-id="364f9-163">다음 내용을 포함한 *src/index.html*을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-163">Create *src/index.html* with the following content.</span></span>

    [!code-html[index.html](signalr-typescript-webpack/sample/src/index.html)]

    <span data-ttu-id="364f9-164">앞의 HTML은 홈 페이지의 상용구 마크업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-164">The preceding HTML defines the homepage's boilerplate markup.</span></span>

1. <span data-ttu-id="364f9-165">새 *src/css* 디렉터리를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-165">Create a new *src/css* directory.</span></span> <span data-ttu-id="364f9-166">그 목적은 프로젝트의 *.css* 파일을 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-166">Its purpose is to store the project's *.css* files.</span></span>

1. <span data-ttu-id="364f9-167">다음 내용을 포함한 *src/css/main.css*를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-167">Create *src/css/main.css* with the following content:</span></span>

    [!code-css[main.css](signalr-typescript-webpack/sample/src/css/main.css)]

    <span data-ttu-id="364f9-168">앞의 *main.css* 파일은 앱의 스타일을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-168">The preceding *main.css* file styles the app.</span></span>

1. <span data-ttu-id="364f9-169">다음 내용을 포함한 *src/tsconfig.json*을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-169">Create *src/tsconfig.json* with the following content:</span></span>

    [!code-json[tsconfig.json](signalr-typescript-webpack/sample/src/tsconfig.json)]

    <span data-ttu-id="364f9-170">앞의 코드는 [ECMAScript](https://wikipedia.org/wiki/ECMAScript) 5 호환 JavaScript를 생성하도록 TypeScript 컴파일러를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-170">The preceding code configures the TypeScript compiler to produce [ECMAScript](https://wikipedia.org/wiki/ECMAScript) 5-compatible JavaScript.</span></span>

1. <span data-ttu-id="364f9-171">다음 내용을 포함한 *src/index.ts*를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-171">Create *src/index.ts* with the following content:</span></span>

    [!code-typescript[index.ts](signalr-typescript-webpack/sample/snippets/index1.ts?name=snippet_IndexTsPhase1File)]

    <span data-ttu-id="364f9-172">이 TypeScript는 DOM 요소 참조를 조회하여 두 가지 이벤트 핸들러를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-172">The preceding TypeScript retrieves references to DOM elements and attaches two event handlers:</span></span>

    * <span data-ttu-id="364f9-173">`keyup`: 이 이벤트는 사용자가 `tbMessage`로 식별되는 텍스트 상자에 내용을 입력할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-173">`keyup`: This event fires when the user types something in the textbox identified as `tbMessage`.</span></span> <span data-ttu-id="364f9-174">`send` 함수는 사용자가 **Enter** 키를 누를 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-174">The `send` function is called when the user presses the **Enter** key.</span></span>
    * <span data-ttu-id="364f9-175">`click`: 이 이벤트는 사용자가 **보내기** 단추를 클릭할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-175">`click`: This event fires when the user clicks the **Send** button.</span></span> <span data-ttu-id="364f9-176">`send` 함수가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-176">The `send` function is called.</span></span>

## <a name="configure-the-aspnet-core-app"></a><span data-ttu-id="364f9-177">ASP.NET Core 앱 구성</span><span class="sxs-lookup"><span data-stu-id="364f9-177">Configure the ASP.NET Core app</span></span>

1. <span data-ttu-id="364f9-178">`Startup.Configure` 메서드에 제공된 코드는 *Hello World!* 를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-178">The code provided in the `Startup.Configure` method displays *Hello World!*.</span></span> <span data-ttu-id="364f9-179">`app.Run` 메서드를 [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_)에 대한 호출로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-179">Replace the `app.Run` method call with calls to [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_).</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_UseStaticDefaultFiles)]

    <span data-ttu-id="364f9-180">이 코드는 사용자가 전체 URL을 입력하는지 아니면 웹앱의 루트 URL만 입력하는지 관계없이 서버가 *index.html* 파일을 찾아서 제공할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-180">The preceding code allows the server to locate and serve the *index.html* file, whether the user enters its full URL or the root URL of the web app.</span></span>

1. <span data-ttu-id="364f9-181">`Startup.ConfigureServices` 메서드에서 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr#Microsoft_Extensions_DependencyInjection_SignalRDependencyInjectionExtensions_AddSignalR_Microsoft_Extensions_DependencyInjection_IServiceCollection_)을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-181">Call [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr#Microsoft_Extensions_DependencyInjection_SignalRDependencyInjectionExtensions_AddSignalR_Microsoft_Extensions_DependencyInjection_IServiceCollection_) in the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="364f9-182">이는 SignalR 서비스를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-182">It adds the SignalR services to your project.</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_AddSignalR)]

1. <span data-ttu-id="364f9-183">*/hub* 경로를 `ChatHub` 허브에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-183">Map a */hub* route to the `ChatHub` hub.</span></span> <span data-ttu-id="364f9-184">`Startup.Configure` 메서드의 끝에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-184">Add the following lines at the end of the `Startup.Configure` method:</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_UseSignalR)]

1. <span data-ttu-id="364f9-185">프로젝트 루트에 *Hubs*라는 새 디렉터리를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-185">Create a new directory, called *Hubs*, in the project root.</span></span> <span data-ttu-id="364f9-186">그 목적은 다음 단계에서 생성되는 SignalR 허브를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-186">Its purpose is to store the SignalR hub, which is created in the next step.</span></span>

1. <span data-ttu-id="364f9-187">다음 내용을 포함한 허브 *Hubs/ChatHub.cs*를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-187">Create hub *Hubs/ChatHub.cs* with the following code:</span></span>

    [!code-csharp[ChatHub](signalr-typescript-webpack/sample/snippets/ChatHub.cs?name=snippet_ChatHubStubClass)]

1. <span data-ttu-id="364f9-188">`ChatHub` 참조를 확인하기 위해 *Startup.cs* 파일의 맨 위에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-188">Add the following code at the top of the *Startup.cs* file to resolve the `ChatHub` reference:</span></span>

    [!code-csharp[Startup](signalr-typescript-webpack/sample/Startup.cs?name=snippet_HubsNamespace)]

## <a name="enable-client-and-server-communication"></a><span data-ttu-id="364f9-189">클라이언트 및 서버 통신 활성화</span><span class="sxs-lookup"><span data-stu-id="364f9-189">Enable client and server communication</span></span>

<span data-ttu-id="364f9-190">앱은 현재 메시지를 보낼 간단한 양식을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-190">The app currently displays a simple form to send messages.</span></span> <span data-ttu-id="364f9-191">그런 시도를 할 때 아무 일도 일어나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-191">Nothing happens when you try to do so.</span></span> <span data-ttu-id="364f9-192">서버는 특정 경로를 수신 대기하지만 보낸 메시지를 사용하여 아무 일도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-192">The server is listening to a specific route but does nothing with sent messages.</span></span>

1. <span data-ttu-id="364f9-193">프로젝트 루트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-193">Execute the following command at the project root:</span></span>

    ```console
    npm install @aspnet/signalr
    ```

    <span data-ttu-id="364f9-194">앞의 명령은 클라이언트가 서버에 메시지를 보낼 수 있도록 하는 [SignalR TypeScript 클라이언트](https://www.npmjs.com/package/@aspnet/signalr)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-194">The preceding command installs the [SignalR TypeScript client](https://www.npmjs.com/package/@aspnet/signalr), which allows the client to send messages to the server.</span></span>

1. <span data-ttu-id="364f9-195">강조 표시된 코드를 *src/index.ts* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-195">Add the highlighted code to the *src/index.ts* file:</span></span>

    [!code-typescript[index.ts](signalr-typescript-webpack/sample/snippets/index2.ts?name=snippet_IndexTsPhase2File&highlight=2,9-23)]

    <span data-ttu-id="364f9-196">앞의 코드는 서버에서 오는 메시지의 수신을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-196">The preceding code supports receiving messages from the server.</span></span> <span data-ttu-id="364f9-197">`HubConnectionBuilder` 클래스는 서버 연결을 구성하기 위한 새 빌더를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-197">The `HubConnectionBuilder` class creates a new builder for configuring the server connection.</span></span> <span data-ttu-id="364f9-198">`withUrl` 함수는 허브 URL을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-198">The `withUrl` function configures the hub URL.</span></span>

    <span data-ttu-id="364f9-199">SignalR은 클라이언트 및 서버 간 메시지 교환을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-199">SignalR enables the exchange of messages between a client and a server.</span></span> <span data-ttu-id="364f9-200">각 메시지는 특정 이름을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-200">Each message has a specific name.</span></span> <span data-ttu-id="364f9-201">예를 들어 메시지 영역에 새 메시지를 표시하는 로직을 실행하는 `messageReceived`라는 이름을 가진 메시지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-201">For example, you can have messages with the name `messageReceived` that execute the logic responsible for displaying the new message in the messages zone.</span></span> <span data-ttu-id="364f9-202">특정 메시지 수신 대기는 `on` 함수를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-202">Listening to a specific message can be done via the `on` function.</span></span> <span data-ttu-id="364f9-203">임의 개수의 메시지 이름을 수신 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-203">You can listen to any number of message names.</span></span> <span data-ttu-id="364f9-204">또한 수신 메시지의 작성자 이름 및 내용 등을 메시지에 파라미터로 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-204">It's also possible to pass parameters to the message, such as the author's name and the content of the message received.</span></span> <span data-ttu-id="364f9-205">클라이언트가 메시지를 수신한 후 `innerHTML` 특성의 작성자 이름 및 메시지 내용을 사용하여 새 `div` 요소가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-205">Once the client receives a message, a new `div` element is created with the author's name and the message content in its `innerHTML` attribute.</span></span> <span data-ttu-id="364f9-206">이 요소가 주 `div` 요소에 추가되어 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-206">It's added to the main `div` element displaying the messages.</span></span>

1. <span data-ttu-id="364f9-207">이제 클라이언트가 메시지를 수신할 수 있으므로, 메시지를 보내도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-207">Now that the client can receive a message, configure it to send messages.</span></span> <span data-ttu-id="364f9-208">강조 표시된 코드를 *src/index.ts* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-208">Add the highlighted code to the *src/index.ts* file:</span></span>

    [!code-typescript[index.ts](signalr-typescript-webpack/sample/src/index.ts?highlight=34-35)]

    <span data-ttu-id="364f9-209">WebSockets 연결을 통해 메시지를 보내면 `send` 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-209">Sending a message through the WebSockets connection requires calling the `send` method.</span></span> <span data-ttu-id="364f9-210">이 메서드의 첫 번째 매개 변수는 메시지의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-210">The method's first parameter is the message name.</span></span> <span data-ttu-id="364f9-211">메시지의 데이터는 다른 매개 변수를 통해 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-211">The message data inhabits the other parameters.</span></span> <span data-ttu-id="364f9-212">이 예제에서는 `newMessage`로 식별되는 메시지가 서버로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-212">In this example, a message identified as `newMessage` is sent to the server.</span></span> <span data-ttu-id="364f9-213">메시지는 사용자 이름 및 텍스트 상자에 입력된 사용자 입력으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-213">The message consists of the username and the user input from a text box.</span></span> <span data-ttu-id="364f9-214">보내기가 작동하면 텍스트 상자 값이 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-214">If the send works, the text box value is cleared.</span></span>

1. <span data-ttu-id="364f9-215">강조 표시된 메서드를 `ChatHub` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-215">Add the highlighted method to the `ChatHub` class:</span></span>

    [!code-csharp[ChatHub](signalr-typescript-webpack/sample/Hubs/ChatHub.cs?highlight=8-11)]

    <span data-ttu-id="364f9-216">앞의 코드는 서버가 메시지를 수신한 후 수신된 메시지를 모든 연결된 사용자에게 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-216">The preceding code broadcasts received messages to all connected users once the server receives them.</span></span> <span data-ttu-id="364f9-217">모든 메시지를 수신하기 위해 일반 `on` 메서드를 포함할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-217">It's unnecessary to have a generic `on` method to receive all the messages.</span></span> <span data-ttu-id="364f9-218">메시지 이름 뒤에 명명한 메서드로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-218">A method named after the message name suffices.</span></span>

    <span data-ttu-id="364f9-219">이 예에서 TypeScript 클라이언트는 `newMessage`로 식별된 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-219">In this example, the TypeScript client sends a message identified as `newMessage`.</span></span> <span data-ttu-id="364f9-220">C# `NewMessage` 메서드에는 클라이언트가 보낸 데이터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-220">The C# `NewMessage` method expects the data sent by the client.</span></span> <span data-ttu-id="364f9-221">[Clients.All](/dotnet/api/microsoft.aspnetcore.signalr.ihubclients-1.all)에 대한 [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-221">A call is made to the [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) method on [Clients.All](/dotnet/api/microsoft.aspnetcore.signalr.ihubclients-1.all).</span></span> <span data-ttu-id="364f9-222">수신된 메시지를 허브에 연결된 모든 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-222">The received messages are sent to all clients connected to the hub.</span></span>

## <a name="test-the-app"></a><span data-ttu-id="364f9-223">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="364f9-223">Test the app</span></span>

<span data-ttu-id="364f9-224">다음 단계를 사용하여 앱이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-224">Confirm that the app works with the following steps.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="364f9-225">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="364f9-225">Visual Studio</span></span>](#tab/visual-studio)

1. <span data-ttu-id="364f9-226">WebPack을 *release* 모드로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-226">Run Webpack in *release* mode.</span></span> <span data-ttu-id="364f9-227">**패키지 관리자 콘솔** 창을 사용하여 프로젝트 루트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-227">Using the **Package Manager Console** window, execute the following command in the project root.</span></span> <span data-ttu-id="364f9-228">프로젝트 루트가 아닌 경우 명령을 입력하기 전에 `cd SignalRWebPack`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-228">If you are not in the project root, enter `cd SignalRWebPack` before entering the command.</span></span>

    [!INCLUDE [npm-run-release](../includes/signalr-typescript-webpack/npm-run-release.md)]

1. <span data-ttu-id="364f9-229">**디버그** > **디버그하지 않고 시작**을 선택하여 디버거를 연결하지 않고 브라우저에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-229">Select **Debug** > **Start without debugging** to launch the app in a browser without attaching the debugger.</span></span> <span data-ttu-id="364f9-230">*wwwroot/index.html* 파일은 `http://localhost:<port_number>`에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-230">The *wwwroot/index.html* file is served at `http://localhost:<port_number>`.</span></span>

1. <span data-ttu-id="364f9-231">다른 브라우저 인스턴스(임의 브라우저)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-231">Open another browser instance (any browser).</span></span> <span data-ttu-id="364f9-232">URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-232">Paste the URL in the address bar.</span></span>

1. <span data-ttu-id="364f9-233">브라우저를 선택하고 **메시지** 텍스트 상자에 내용을 입력하고 **보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-233">Choose either browser, type something in the **Message** text box, and click the **Send** button.</span></span> <span data-ttu-id="364f9-234">고유한 사용자 이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-234">The unique user name and message are displayed on both pages instantly.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="364f9-235">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="364f9-235">Visual Studio Code</span></span>](#tab/visual-studio-code)

1. <span data-ttu-id="364f9-236">프로젝트 루트에서 다음 명령을 실행하여 WebPack을 *release* 모드로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-236">Run Webpack in *release* mode by executing the following command in the project root:</span></span>

    [!INCLUDE [npm-run-release](../includes/signalr-typescript-webpack/npm-run-release.md)]

1. <span data-ttu-id="364f9-237">프로젝트 루트에서 다음 명령을 실행하여 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-237">Build and run the app by executing the following command in the project root:</span></span>

    ```console
    dotnet run
    ```

    <span data-ttu-id="364f9-238">웹 서버가 앱을 시작하고 로컬 호스트에서 사용할 수 있도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-238">The web server starts the app and makes it available on localhost.</span></span>

1. <span data-ttu-id="364f9-239">`http://localhost:<port_number>`에 대해 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-239">Open a browser to `http://localhost:<port_number>`.</span></span> <span data-ttu-id="364f9-240">그러면 *wwwroot/index.html* 파일이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-240">The *wwwroot/index.html* file is served.</span></span> <span data-ttu-id="364f9-241">주소 표시줄에서 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-241">Copy the URL from the address bar.</span></span>

1. <span data-ttu-id="364f9-242">다른 브라우저 인스턴스(임의 브라우저)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-242">Open another browser instance (any browser).</span></span> <span data-ttu-id="364f9-243">URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-243">Paste the URL in the address bar.</span></span>

1. <span data-ttu-id="364f9-244">브라우저를 선택하고 **메시지** 텍스트 상자에 내용을 입력하고 **보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-244">Choose either browser, type something in the **Message** text box, and click the **Send** button.</span></span> <span data-ttu-id="364f9-245">고유한 사용자 이름과 메시지는 두 페이지 모두에 즉시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="364f9-245">The unique user name and message are displayed on both pages instantly.</span></span>

---

![두 브라우저 창 모두에 표시된 메시지](signalr-typescript-webpack/_static/browsers-message-broadcast.png)

## <a name="additional-resources"></a><span data-ttu-id="364f9-247">추가 자료</span><span class="sxs-lookup"><span data-stu-id="364f9-247">Additional resources</span></span>

* <xref:signalr/javascript-client>
* <xref:signalr/hubs>
