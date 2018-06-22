---
title: ASP.NET Core에서 Angular 프로젝트 템플릿 사용
author: SteveSandersonMS
description: Angular 및 Angular CLI에 대한 ASP.NET Core SPA(단일 페이지 응용 프로그램) 프로젝트 템플릿을 시작하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/angular
ms.openlocfilehash: 811e28af2b67c356ff038d8d673e2164bb56578e
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36291466"
---
# <a name="use-the-angular-project-template-with-aspnet-core"></a><span data-ttu-id="b879e-103">ASP.NET Core에서 Angular 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="b879e-103">Use the Angular project template with ASP.NET Core</span></span>

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> <span data-ttu-id="b879e-104">이 문서는 ASP.NET Core 2.0에 포함된 Angular 프로젝트 템플릿에 대한 내용이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-104">This documentation isn't about the Angular project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="b879e-105">수동으로 업데이트할 수 있는 최신 Angular 템플릿에 대한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-105">It's about the newer Angular template to which you can update manually.</span></span> <span data-ttu-id="b879e-106">템플릿은 ASP.NET Core 2.1에 기본적으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

::: moniker-end

<span data-ttu-id="b879e-107">업데이트된 Angular 프로젝트 템플릿은 Angular 및 Angular CLI를 사용하여 풍부한 클라이언트 쪽 UI(사용자 인터페이스)를 구현하는 ASP.NET Core 앱에 대한 편리한 시작점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-107">The updated Angular project template provides a convenient starting point for ASP.NET Core apps using Angular and the Angular CLI to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="b879e-108">이 템플릿은 API 백 엔드로 사용되는 ASP.NET Core 프로젝트 및 UI로 사용되는 Angular CLI 프로젝트를 만드는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-108">The template is equivalent to creating an ASP.NET Core project to act as an API backend and an Angular CLI project to act as a UI.</span></span> <span data-ttu-id="b879e-109">템플릿은 단일 앱 프로젝트에서 두 프로젝트 유형을 모두 호스트하는 편리한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-109">The template offers the convenience of hosting both project types in a single app project.</span></span> <span data-ttu-id="b879e-110">따라서 앱 프로젝트를 단일 단위로 빌드하고 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-110">Consequently, the app project can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="b879e-111">새 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="b879e-111">Create a new app</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="b879e-112">ASP.NET Core 2.0을 사용하는 경우 [업데이트된 React 프로젝트 템플릿을 설치](xref:spa/index#installation)했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-112">If using ASP.NET Core 2.0, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span>

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="b879e-113">ASP.NET Core 2.1이 설치 되어 있을 경우 각 프로젝트 템플릿은 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-113">If you have ASP.NET Core 2.1 installed, there's no need to install the Angular project template.</span></span>

::: moniker-end

<span data-ttu-id="b879e-114">빈 디렉터리에 `dotnet new angular` 명령을 사용하여 명령 프롬프트에서 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-114">Create a new project from a command prompt using the command `dotnet new angular` in an empty directory.</span></span> <span data-ttu-id="b879e-115">예를 들어 다음 명령은 *my-new-app* 디렉터리에 앱을 만들고 해당 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-115">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new angular -o my-new-app
cd my-new-app
```

<span data-ttu-id="b879e-116">Visual Studio 또는 .NET Core CLI에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-116">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="b879e-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b879e-117">Visual Studio</span></span>](#tab/visual-studio/)

<span data-ttu-id="b879e-118">생성된 *.csproj* 파일을 열고 여기에서 정상적으로 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-118">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="b879e-119">빌드 프로세스는 첫 번째 실행에서 npm 종속성을 복원하고 이 작업에는 몇 분 정도 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-119">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="b879e-120">후속 빌드는 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-120">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="b879e-121">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="b879e-121">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="b879e-122">`Development` 값을 가진 `ASPNETCORE_Environment` 환경 변수가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-122">Ensure you have an environment variable called `ASPNETCORE_Environment` with a value of `Development`.</span></span> <span data-ttu-id="b879e-123">Windows(PowerShell 이외의 프롬프트)에서 `SET ASPNETCORE_Environment=Development`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-123">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="b879e-124">Linux 또는 macOS에서 `export ASPNETCORE_Environment=Development`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-124">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="b879e-125">[dotnet build](/dotnet/core/tools/dotnet-build)를 실행하여 앱이 제대로 빌드되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-125">Run [dotnet build](/dotnet/core/tools/dotnet-build) to verify the app builds correctly.</span></span> <span data-ttu-id="b879e-126">첫 번째 실행에서 빌드 프로세스는 npm 종속성을 복원하고 이 작업에는 몇 분 정도 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-126">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="b879e-127">후속 빌드는 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-127">Subsequent builds are much faster.</span></span>

<span data-ttu-id="b879e-128">[dotnet run](/dotnet/core/tools/dotnet-run)을 실행하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-128">Run [dotnet run](/dotnet/core/tools/dotnet-run) to start the app.</span></span> <span data-ttu-id="b879e-129">다음과 유사한 메시지가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-129">A message similar to the following is logged:</span></span>

```console
Now listening on: http://localhost:<port>
```

<span data-ttu-id="b879e-130">브라우저에서 이 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-130">Navigate to this URL in a browser.</span></span>

<span data-ttu-id="b879e-131">앱이 백그라운드에서 Angular CLI 서버의 인스턴스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-131">The app starts up an instance of the Angular CLI server in the background.</span></span> <span data-ttu-id="b879e-132">다음과 유사한 메시지가 기록됩니다. *NG Live Development Server는 localhost:&lt;otherport&gt;에서 수신 대기 중이고, http://localhost:&lt;otherport&gt;/에서 브라우저를 엽니다*.</span><span class="sxs-lookup"><span data-stu-id="b879e-132">A message similar to the following is logged: *NG Live Development Server is listening on localhost:&lt;otherport&gt;, open your browser on http://localhost:&lt;otherport&gt;/*.</span></span> <span data-ttu-id="b879e-133">이 메시지 무시&mdash;결합된 ASP.NET Core 및 Angular CLI 앱의 URL이 **아닙니다**.</span><span class="sxs-lookup"><span data-stu-id="b879e-133">Ignore this message&mdash;it's **not** the URL for the combined ASP.NET Core and Angular CLI app.</span></span>

---

<span data-ttu-id="b879e-134">프로젝트 템플릿은 ASP.NET Core 앱과 Angular 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-134">The project template creates an ASP.NET Core app and an Angular app.</span></span> <span data-ttu-id="b879e-135">ASP.NET Core 앱은 데이터 액세스, 권한 부여 및 기타 서버 쪽 문제에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-135">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="b879e-136">*ClientApp* 하위 디렉터리에 있는 Angular 앱은 모든 UI 문제에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-136">The Angular app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="b879e-137">페이지, 이미지, 스타일, 모듈 등을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-137">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="b879e-138">*ClientApp* 디렉터리에는 표준 Angular CLI 앱이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-138">The *ClientApp* directory contains a standard Angular CLI app.</span></span> <span data-ttu-id="b879e-139">자세한 내용은 공식 [Angular 설명서](https://github.com/angular/angular-cli/wiki)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b879e-139">See the official [Angular documentation](https://github.com/angular/angular-cli/wiki) for more information.</span></span>

<span data-ttu-id="b879e-140">이 템플릿에서 만들어진 Angular 앱과 Angular CLI 자체에서(`ng new`을 통해) 만들어진 앱 간에는 약간 차이가 있지만 앱의 기능은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-140">There are slight differences between the Angular app created by this template and the one created by Angular CLI itself (via `ng new`); however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="b879e-141">템플릿에서 만들어진 앱에는 [부트스트랩](https://getbootstrap.com/) 기반 레이아웃 및 기본 라우팅 예제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-141">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="run-ng-commands"></a><span data-ttu-id="b879e-142">ng 명령 실행</span><span class="sxs-lookup"><span data-stu-id="b879e-142">Run ng commands</span></span>

<span data-ttu-id="b879e-143">명령 프롬프트에서 *ClientApp* 하위 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-143">In a command prompt, switch to the *ClientApp* subdirectory:</span></span>

```console
cd ClientApp
```

<span data-ttu-id="b879e-144">`ng` 도구가 전역으로 설치된 경우 해당 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-144">If you have the `ng` tool installed globally, you can run any of its commands.</span></span> <span data-ttu-id="b879e-145">예를 들어 `ng lint`, `ng test` 또는 기타 모든 [Angular CLI 명령](https://github.com/angular/angular-cli/wiki#additional-commands)을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-145">For example, you can run `ng lint`, `ng test`, or any of the other [Angular CLI commands](https://github.com/angular/angular-cli/wiki#additional-commands).</span></span> <span data-ttu-id="b879e-146">ASP.NET Core 앱은 앱의 서버 쪽 및 클라이언트 쪽 파트를 둘 다 처리하기 때문에 `ng serve`를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-146">There's no need to run `ng serve` though, because your ASP.NET Core app deals with serving both server-side and client-side parts of your app.</span></span> <span data-ttu-id="b879e-147">내부적으로는 개발 시 `ng serve`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-147">Internally, it uses `ng serve` in development.</span></span>

<span data-ttu-id="b879e-148">`ng` 도구가 설치되지 않은 경우에는 대신에 `npm run ng`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-148">If you don't have the `ng` tool installed, run `npm run ng` instead.</span></span> <span data-ttu-id="b879e-149">예를 들어 `npm run ng lint` 또는 `npm run ng test`를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-149">For example, you can run `npm run ng lint` or `npm run ng test`.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="b879e-150">npm 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="b879e-150">Install npm packages</span></span>

<span data-ttu-id="b879e-151">타사 npm 패키지를 설치하려면 *ClientApp* 하위 디렉터리에서 명령 프롬프트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-151">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="b879e-152">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="b879e-152">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="b879e-153">게시 및 배포</span><span class="sxs-lookup"><span data-stu-id="b879e-153">Publish and deploy</span></span>

<span data-ttu-id="b879e-154">개발 시에 앱은 개발자 편의를 위해 최적화된 모드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-154">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="b879e-155">예를 들어 디버그할 때 원래 TypeScript 코드를 볼 수 있도록 JavaScript 번들에 소스 맵이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-155">For example, JavaScript bundles include source maps (so that when debugging, you can see your original TypeScript code).</span></span> <span data-ttu-id="b879e-156">앱은 디스크에서 TypeScript, HTML 및 CSS 파일 변경 내용을 감시하고 해당 파일의 변경을 확인하면 자동으로 다시 컴파일하고 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-156">The app watches for TypeScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="b879e-157">프로덕션 시에는 성능에 최적화된 앱의 버전을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-157">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="b879e-158">이는 자동으로 수행하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-158">This is configured to happen automatically.</span></span> <span data-ttu-id="b879e-159">게시할 때 빌드 구성은 클라이언트 쪽 코드의 축소된 AOT(Ahead-Of-Time) 컴파일된 빌드를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-159">When you publish, the build configuration emits a minified, ahead-of-time (AoT) compiled build of your client-side code.</span></span> <span data-ttu-id="b879e-160">개발 빌드와 달리 프로덕션 빌드에는 [서버 쪽 사전 렌더링](#server-side-rendering)을 사용하지 않는 한 서버에 Node.js를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-160">Unlike the development build, the production build doesn't require Node.js to be installed on the server (unless you have enabled [server-side prerendering](#server-side-rendering)).</span></span>

<span data-ttu-id="b879e-161">표준 [ASP.NET Core 호스팅 및 배포 방법](xref:host-and-deploy/index)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-161">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-ng-serve-independently"></a><span data-ttu-id="b879e-162">개별적으로 “ng serve” 실행</span><span class="sxs-lookup"><span data-stu-id="b879e-162">Run "ng serve" independently</span></span>

<span data-ttu-id="b879e-163">프로젝트는 ASP.NET Core 앱이 개발 모드에서 시작될 때 백그라운드에서 Angular CLI 서버의 자체 인스턴스를 시작하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-163">The project is configured to start its own instance of the Angular CLI server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="b879e-164">이 방법은 별도의 서버를 수동으로 실행할 필요가 없기 때문에 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-164">This is convenient because you don't have to run a separate server manually.</span></span>

<span data-ttu-id="b879e-165">이 기본 설정에는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-165">There's a drawback to this default setup.</span></span> <span data-ttu-id="b879e-166">C# 코드를 수정하고 ASP.NET Core 앱을 다시 시작해야 할 때마다 Angular CLI 서버가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-166">Each time you modify your C# code and your ASP.NET Core app needs to restart, the Angular CLI server restarts.</span></span> <span data-ttu-id="b879e-167">백업을 시작하려면 10초 정도가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-167">Around 10 seconds is required to start back up.</span></span> <span data-ttu-id="b879e-168">C# 코드를 자주 편집하고 있고 Angular CLI가 다시 시작될 때까지 기다리지 않으려면 ASP.NET Core 프로세스와는 별도로 Angular CLI 서버를 외부에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-168">If you're making frequent C# code edits and don't want to wait for Angular CLI to restart, run the Angular CLI server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="b879e-169">이를 수행하려면:</span><span class="sxs-lookup"><span data-stu-id="b879e-169">To do so:</span></span>

1. <span data-ttu-id="b879e-170">명령 프롬프트에서 *ClientApp* 하위 디렉터리로 전환하고 Angular CLI 개발 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-170">In a command prompt, switch to the *ClientApp* subdirectory, and launch the Angular CLI development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b879e-171">`ng serve`가 아니라 `npm start`를 사용하여 Angular CLI 개발 서버를 시작하면 *package.json*의 구성이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-171">Use `npm start` to launch the Angular CLI development server, not `ng serve`, so that the configuration in *package.json* is respected.</span></span> <span data-ttu-id="b879e-172">추가 매개 변수를 Angular CLI 서버에 전달하려면 *package.json* 파일의 관련 `scripts` 줄에 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-172">To pass additional parameters to the Angular CLI server, add them to the relevant `scripts` line in your *package.json* file.</span></span>

2. <span data-ttu-id="b879e-173">자체 인스턴스 중 하나를 시작하지 않고 외부 Angular CLI 인스턴스를 사용하도록 ASP.NET Core 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-173">Modify your ASP.NET Core app to use the external Angular CLI instance instead of launching one of its own.</span></span> <span data-ttu-id="b879e-174">*Startup* 클래스에서 `spa.UseAngularCliServer` 호출을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-174">In your *Startup* class, replace the `spa.UseAngularCliServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:4200");
    ```

<span data-ttu-id="b879e-175">ASP.NET Core 앱을 시작할 때 Angular CLI 서버는 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-175">When you start your ASP.NET Core app, it won't launch an Angular CLI server.</span></span> <span data-ttu-id="b879e-176">수동으로 시작한 인스턴스가 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-176">The instance you started manually is used instead.</span></span> <span data-ttu-id="b879e-177">이를 통해 더 빠르게 시작하고 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-177">This enables it to start and restart faster.</span></span> <span data-ttu-id="b879e-178">더 이상 Angular CLI가 매번 클라이언트 앱을 다시 빌드할 때까지 기다리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-178">It's no longer waiting for Angular CLI to rebuild your client app each time.</span></span>

## <a name="server-side-rendering"></a><span data-ttu-id="b879e-179">서버 쪽 렌더링</span><span class="sxs-lookup"><span data-stu-id="b879e-179">Server-side rendering</span></span>

<span data-ttu-id="b879e-180">성능 기능으로 Angular 앱을 클라이언트에서 실행할 뿐 아니라 서버에서 미리 렌더링하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-180">As a performance feature, you can choose to pre-render your Angular app on the server as well as running it on the client.</span></span> <span data-ttu-id="b879e-181">즉, 브라우저는 앱의 초기 UI를 나타내는 HTML 태그를 수신하므로 JavaScript 번들을 다운로드하고 실행하기 전에 이 태그를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-181">This means that browsers receive HTML markup representing your app's initial UI, so they display it even before downloading and executing your JavaScript bundles.</span></span> <span data-ttu-id="b879e-182">이것에 대한 대부분의 구현은 [Angular Universal](https://universal.angular.io/)이라는 Angular 기능에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-182">Most of the implementation of this comes from an Angular feature called [Angular Universal](https://universal.angular.io/).</span></span>

> [!TIP]
> <span data-ttu-id="b879e-183">SSR(서버 쪽 렌더링)을 사용하면 개발 및 배포 중에 몇 가지 문제점이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-183">Enabling server-side rendering (SSR) introduces a number of extra complications both during development and deployment.</span></span> <span data-ttu-id="b879e-184">[SSR의 단점](#drawbacks-of-ssr)을 참조하여 SSR이 요구 사항에 적합한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-184">Read [drawbacks of SSR](#drawbacks-of-ssr) to determine if SSR is a good fit for your requirements.</span></span>

<span data-ttu-id="b879e-185">SSR을 사용하려면 프로젝트에 여러 항목을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-185">To enable SSR, you need to make a number of additions to your project.</span></span>

<span data-ttu-id="b879e-186">*Startup* 클래스에서 `spa.Options.SourcePath`를 구성하는 줄 ‘뒤’ 및 `UseAngularCliServer` 또는 `UseProxyToSpaDevelopmentServer`에 대한 호출 ‘앞’에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-186">In the *Startup* class, *after* the line that configures `spa.Options.SourcePath`, and *before* the call to `UseAngularCliServer` or `UseProxyToSpaDevelopmentServer`, add the following:</span></span>

[!code-csharp[](sample/AngularServerSideRendering/Startup.cs?name=snippet_Call_UseSpa&highlight=5-12)]

<span data-ttu-id="b879e-187">개발 모드에서 이 코드는 *ClientApp\package.json*에 정의된 `build:ssr` 스크립트를 실행하여 SSR 번들을 빌드하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-187">In development mode, this code attempts to build the SSR bundle by running the script `build:ssr`, which is defined in *ClientApp\package.json*.</span></span> <span data-ttu-id="b879e-188">이 빌드는 아직 정의되지 않은 `ssr`이라는 Angular 앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-188">This builds an Angular app named `ssr`, which isn't yet defined.</span></span>

<span data-ttu-id="b879e-189">*ClientApp/.angular-cli.json*에 있는 `apps` 배열의 끝에서 이름이 `ssr`인 추가 앱을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-189">At the end of the `apps` array in *ClientApp/.angular-cli.json*, define an extra app with name `ssr`.</span></span> <span data-ttu-id="b879e-190">다음 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-190">Use the following options:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/.angular-cli.json?range=24-41)]

<span data-ttu-id="b879e-191">이 새 SSR 사용 가능 앱 구성에는 두 개의 추가 파일(*tsconfig.server.json* 및 *main.server.ts*)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-191">This new SSR-enabled app configuration requires two further files: *tsconfig.server.json* and *main.server.ts*.</span></span> <span data-ttu-id="b879e-192">*tsconfig.server.json* 파일은 TypeScript 컴파일 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-192">The *tsconfig.server.json* file specifies TypeScript compilation options.</span></span> <span data-ttu-id="b879e-193">*main.server.ts* 파일은 SSR 중에 코드 진입점으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-193">The *main.server.ts* file serves as the code entry point during SSR.</span></span>

<span data-ttu-id="b879e-194">기존 *tsconfig.app.json*과 함께 *ClientApp/src* 내부에서 다음을 포함하는 *tsconfig.server.json* 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-194">Add a new file called *tsconfig.server.json* inside *ClientApp/src* (alongside the existing *tsconfig.app.json*), containing the following:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/src/tsconfig.server.json)]

<span data-ttu-id="b879e-195">이 파일은 `app.server.module` 모듈을 검색하도록 Angular의 AoT 컴파일러를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-195">This file configures Angular's AoT compiler to look for a module called `app.server.module`.</span></span> <span data-ttu-id="b879e-196">기존 *app.module.ts*와 함께 *ClientApp/src/app/app.server.module.ts*에서 다음을 포함하는 새 파일을 만들어 이 모듈을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-196">Add this by creating a new file at *ClientApp/src/app/app.server.module.ts* (alongside the existing *app.module.ts*) containing the following:</span></span>

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/app/app.server.module.ts)]

<span data-ttu-id="b879e-197">이 모듈은 클라이언트 쪽 `app.module`에서 상속하고 SSR 중에 사용 가능한 추가 Angular 모듈을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-197">This module inherits from your client-side `app.module` and defines which extra Angular modules are available during SSR.</span></span>

<span data-ttu-id="b879e-198">*.angular-cli.json*의 새 `ssr` 항목은 *main.server.ts*라는 진입점 파일을 참조했습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-198">Recall that the new `ssr` entry in *.angular-cli.json* referenced an entry point file called *main.server.ts*.</span></span> <span data-ttu-id="b879e-199">아직 해당 파일을 추가하지 않았으므로 지금 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-199">You haven't yet added that file, and now is time to do so.</span></span> <span data-ttu-id="b879e-200">기존 *main.ts*와 함께 *ClientApp/src/main.server.ts*에서 다음을 포함하는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-200">Create a new file at *ClientApp/src/main.server.ts* (alongside the existing *main.ts*), containing the following:</span></span>

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/main.server.ts)]

<span data-ttu-id="b879e-201">이 파일의 코드는 *Startup* 클래스에 추가한 `UseSpaPrerendering` 미들웨어를 실행할 때 ASP.NET Core에서 각 요청에 대해 실행하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-201">This file's code is what ASP.NET Core executes for each request when it runs the `UseSpaPrerendering` middleware that you added to the *Startup* class.</span></span> <span data-ttu-id="b879e-202">이 코드는 .NET 코드(예: 요청되는 URL)의 `params` 수신을 처리하고 Angular SSR API를 호출하여 결과 HTML을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-202">It deals with receiving `params` from the .NET code (such as the URL being requested), and making calls to Angular SSR APIs to get the resulting HTML.</span></span>

<span data-ttu-id="b879e-203">엄밀히 말하면 개발 모드에서 SSR을 사용하려면 이 코드로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-203">Strictly-speaking, this is sufficient to enable SSR in development mode.</span></span> <span data-ttu-id="b879e-204">앱이 게시될 때 제대로 작동하도록 한 번의 최종 변경을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-204">It's essential to make one final change so that your app works correctly when published.</span></span> <span data-ttu-id="b879e-205">앱의 기본 *.csproj* 파일에서 `BuildServerSideRenderer` 속성 값을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-205">In your app's main *.csproj* file, set the `BuildServerSideRenderer` property value to `true`:</span></span>

[!code-xml[](sample/AngularServerSideRendering/AngularServerSideRendering.csproj?name=snippet_EnableBuildServerSideRenderer)]

<span data-ttu-id="b879e-206">이렇게 하면 SSR 파일을 서버에 게시 및 배포하는 동안 `build:ssr`을 실행하도록 빌드 프로세스가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-206">This configures the build process to run `build:ssr` during publishing and deploy the SSR files to the server.</span></span> <span data-ttu-id="b879e-207">이 기능을 사용하지 않으면 SSR이 프로덕션에서 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-207">If you don't enable this, SSR fails in production.</span></span>

<span data-ttu-id="b879e-208">앱이 개발 또는 프로덕션 모드에서 실행되는 경우 Angular 코드는 서버에서 HTML로 미리 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-208">When your app runs in either development or production mode, the Angular code pre-renders as HTML on the server.</span></span> <span data-ttu-id="b879e-209">클라이언트 쪽 코드는 정상적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-209">The client-side code executes as normal.</span></span>

### <a name="pass-data-from-net-code-into-typescript-code"></a><span data-ttu-id="b879e-210">.NET 코드의 데이터를 TypeScript 코드로 전달</span><span class="sxs-lookup"><span data-stu-id="b879e-210">Pass data from .NET code into TypeScript code</span></span>

<span data-ttu-id="b879e-211">SSR 중에 ASP.NET Core 앱에서 요청별 데이터를 Angular 앱으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-211">During SSR, you might want to pass per-request data from your ASP.NET Core app into your Angular app.</span></span> <span data-ttu-id="b879e-212">예를 들어 쿠키 정보를 전달하거나 데이터베이스에서 무언가를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-212">For example, you could pass cookie information or something read from a database.</span></span> <span data-ttu-id="b879e-213">이를 수행하려면 *Startup* 클래스를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-213">To do this, edit your *Startup* class.</span></span> <span data-ttu-id="b879e-214">`UseSpaPrerendering`에 대한 콜백에서 다음과 같은 `options.SupplyData` 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-214">In the callback for `UseSpaPrerendering`, set a value for `options.SupplyData` such as the following:</span></span>

```csharp
options.SupplyData = (context, data) =>
{
    // Creates a new value called isHttpsRequest that's passed to TypeScript code
    data["isHttpsRequest"] = context.Request.IsHttps;
};
```

<span data-ttu-id="b879e-215">`SupplyData` 콜백을 사용하면 임의, 요청별, JSON serialize 가능 데이터(예: 문자열, 부울 또는 숫자)를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-215">The `SupplyData` callback lets you pass arbitrary, per-request, JSON-serializable data (for example, strings, booleans, or numbers).</span></span> <span data-ttu-id="b879e-216">*main.server.ts* 코드는 이 데이터를 `params.data`로 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-216">Your *main.server.ts* code receives this as `params.data`.</span></span> <span data-ttu-id="b879e-217">예를 들어 앞의 코드 샘플은 부울 값을 `params.data.isHttpsRequest`로 `createServerRenderer` 콜백에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-217">For example, the preceding code sample passes a boolean value as `params.data.isHttpsRequest` into the `createServerRenderer` callback.</span></span> <span data-ttu-id="b879e-218">Angular에서 지원되는 모든 방법으로 앱의 다른 파트에 이 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-218">You can pass this to other parts of your app in any way supported by Angular.</span></span> <span data-ttu-id="b879e-219">예를 들어 *main.server.ts*에서 생성자가 `BASE_URL` 값을 수신하도록 선언된 모든 구성 요소에 이 값을 전달하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b879e-219">For example, see how *main.server.ts* passes the `BASE_URL` value to any component whose constructor is declared to receive it.</span></span>

### <a name="drawbacks-of-ssr"></a><span data-ttu-id="b879e-220">SSR의 단점</span><span class="sxs-lookup"><span data-stu-id="b879e-220">Drawbacks of SSR</span></span>

<span data-ttu-id="b879e-221">일부 앱에서는 SSR의 이점을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-221">Not all apps benefit from SSR.</span></span> <span data-ttu-id="b879e-222">주된 이점은 체감 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-222">The primary benefit is perceived performance.</span></span> <span data-ttu-id="b879e-223">느린 네트워크 연결을 통하거나 느린 모바일 장치에서 앱에 도달하는 방문자는 JavaScript 번들을 페치 또는 구문 분석하는 동안 시간이 걸리더라도 초기 UI를 빠르게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-223">Visitors reaching your app over a slow network connection or on slow mobile devices see the initial UI quickly, even if it takes a while to fetch or parse the JavaScript bundles.</span></span> <span data-ttu-id="b879e-224">그러나 많은 SPA는 앱이 거의 즉각적으로 나타나는 고성능 컴퓨터에서 고속 사내 네트워크를 통해 주로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-224">However, many SPAs are mainly used over fast, internal company networks on fast computers where the app appears almost instantly.</span></span>

<span data-ttu-id="b879e-225">또한, SSR을 사용하는 데는 상당한 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-225">At the same time, there are significant drawbacks to enabling SSR.</span></span> <span data-ttu-id="b879e-226">개발 프로세스가 복잡해지고</span><span class="sxs-lookup"><span data-stu-id="b879e-226">It adds complexity to your development process.</span></span> <span data-ttu-id="b879e-227">코드를 클라이언트 쪽 및 서버 쪽(ASP.NET Core에서 호출되는 Node.js 환경) 등 두 가지 환경에서 실행해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-227">Your code must run in two different environments: client-side and server-side (in a Node.js environment invoked from ASP.NET Core).</span></span> <span data-ttu-id="b879e-228">다음과 같은 몇 가지 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-228">Here are some things to bear in mind:</span></span>

* <span data-ttu-id="b879e-229">SSR을 사용하려면 프로덕션 서버에 Node.js를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-229">SSR requires a Node.js installation on your production servers.</span></span> <span data-ttu-id="b879e-230">Azure App Services와 같은 일부 배포 시나리오의 경우에는 이 내용이 적용되지만 Azure Service Fabric과 같은 다른 배포 시나리오에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-230">This is automatically the case for some deployment scenarios, such as Azure App Services, but not for others, such as Azure Service Fabric.</span></span>
* <span data-ttu-id="b879e-231">`BuildServerSideRenderer` 빌드 플래그를 사용하면 *node_modules* 디렉터리가 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-231">Enabling the `BuildServerSideRenderer` build flag causes your *node_modules* directory to publish.</span></span> <span data-ttu-id="b879e-232">이 폴더에는 20,000개 이상의 파일이 포함되어 있으므로 배포 시간이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-232">This folder contains 20,000+ files, which increases deployment time.</span></span>
* <span data-ttu-id="b879e-233">Node.js 환경에서 코드를 실행하기 위해 `window` 또는 `localStorage`와 같은 브라우저 관련 JavaScript API를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-233">To run your code in a Node.js environment, it can't rely on the existence of browser-specific JavaScript APIs such as `window` or `localStorage`.</span></span> <span data-ttu-id="b879e-234">코드(또는 참조하는 일부 타사 라이브러리)가 이러한 API를 사용하려고 하면 SSR 중에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-234">If your code (or some third-party library you reference) tries to use these APIs, you'll get an error during SSR.</span></span> <span data-ttu-id="b879e-235">예를 들어 많은 위치에서 브라우저 관련 API를 참조하므로 jQuery를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b879e-235">For example, don't use jQuery because it references browser-specific APIs in many places.</span></span> <span data-ttu-id="b879e-236">오류를 방지하려면 SSR 또는 브라우저 관련 API를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b879e-236">To prevent errors, you must either avoid SSR or avoid browser-specific APIs or libraries.</span></span> <span data-ttu-id="b879e-237">검사에서 해당 API에 대한 모든 호출을 래핑하여 SSR 중에 호출되지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-237">You can wrap any calls to such APIs in checks to ensure they aren't invoked during SSR.</span></span> <span data-ttu-id="b879e-238">예를 들어 JavaScript 또는 TypeScript 코드에서 다음과 같은 검사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b879e-238">For example, use a check such as the following in JavaScript or TypeScript code:</span></span>

    ```javascript
    if (typeof window !== 'undefined') {
        // Call browser-specific APIs here
    }
    ```
