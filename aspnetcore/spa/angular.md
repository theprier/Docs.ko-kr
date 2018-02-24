---
title: "각 프로젝트 템플릿을 사용 하 여"
author: SteveSandersonMS
description: "각 및 각도 CLI에 대 한 ASP.NET Core 단일 페이지 응용 프로그램 (SPA) 프로젝트 템플릿으로 시작 하는 방법에 알아봅니다."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/angular
ms.openlocfilehash: f81130b67d61ee063b697f19862449c3054d547d
ms.sourcegitcommit: 49fb3b7669b504d35edad34db8285e56b958a9fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="use-the-angular-project-template"></a><span data-ttu-id="bbe07-103">각 프로젝트 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="bbe07-103">Use the Angular project template</span></span>

> [!NOTE]
> <span data-ttu-id="bbe07-104">이 설명서 포함 되지 않습니다 각도 프로젝트 템플릿에 대 한 ASP.NET 코어 2.0.</span><span class="sxs-lookup"><span data-stu-id="bbe07-104">This documentation isn't about the Angular project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="bbe07-105">최신 각도 서식 파일을 수동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-105">It's about the newer Angular template to which you can update manually.</span></span> <span data-ttu-id="bbe07-106">서식 파일은 기본적으로 ASP.NET Core 2.1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

<span data-ttu-id="bbe07-107">업데이트 된 각 프로젝트 템플릿은 있는 편리 하 게 시작 지점을 제공 ASP.NET Core에 대 한 각 및 각도 CLI를 사용 하는 다양 하 고 클라이언트 쪽 UI (사용자 인터페이스)를 구현 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-107">The updated Angular project template provides a convenient starting point for ASP.NET Core apps using Angular and the Angular CLI to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="bbe07-108">템플릿에 API 백 엔드 역할을 하는 ASP.NET Core 프로젝트 및는 각도 CLI 프로젝트의 역할을 하는 UI를 만드는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-108">The template is equivalent to creating an ASP.NET Core project to act as an API backend and an Angular CLI project to act as a UI.</span></span> <span data-ttu-id="bbe07-109">서식 파일은 단일 응용 프로그램 프로젝트의 두 프로젝트 형식 호스팅의 편의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-109">The template offers the convenience of hosting both project types in a single app project.</span></span> <span data-ttu-id="bbe07-110">따라서 응용 프로그램 프로젝트 빌드 및 단일 단위로 게시 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-110">Consequently, the app project can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="bbe07-111">새 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="bbe07-111">Create a new app</span></span>

<span data-ttu-id="bbe07-112">ASP.NET Core 2.0을 사용 하는 경우 확인 했습니다. [설치 된 업데이트 된 각 프로젝트 템플릿](xref:spa/index#installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-112">If using ASP.NET Core 2.0, ensure you've [installed the updated Angular project template](xref:spa/index#installation).</span></span> <span data-ttu-id="bbe07-113">ASP.NET Core 2.1 있을 경우 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-113">If you have ASP.NET Core 2.1, there's no need to install it.</span></span>

<span data-ttu-id="bbe07-114">명령을 사용 하 여 명령 프롬프트에서 새 프로젝트 만들기 `dotnet new angular` 빈 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-114">Create a new project from a command prompt using the command `dotnet new angular` in an empty directory.</span></span> <span data-ttu-id="bbe07-115">예를 들어 다음 명령에서 응용 프로그램을 만듭니다는 *내-새-app* 디렉터리와 해당 디렉터리에 스위치:</span><span class="sxs-lookup"><span data-stu-id="bbe07-115">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new angular -o my-new-app
cd my-new-app
```

<span data-ttu-id="bbe07-116">Visual Studio 또는.NET Core CLI에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-116">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="bbe07-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbe07-117">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="bbe07-118">생성 된 열고 *.csproj* 파일, 및 여기에서 응용 프로그램 정상적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-118">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="bbe07-119">빌드 프로세스는 몇 분 정도 걸릴 수 있는 첫 번째 실행 시 npm 종속성을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-119">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="bbe07-120">후속 빌드는 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-120">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="bbe07-121">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="bbe07-121">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="bbe07-122">라는 환경 변수 해야 `ASPNETCORE_Environment` 값 `Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-122">Ensure you have an environment variable called `ASPNETCORE_Environment` with a value of `Development`.</span></span> <span data-ttu-id="bbe07-123">(비 PowerShell 프롬프트)의 Windows에서는 실행 `SET ASPNETCORE_Environment=Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-123">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="bbe07-124">Linux 또는 macOS 실행 `export ASPNETCORE_Environment=Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-124">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="bbe07-125">실행 `dotnet build` 응용 프로그램을 확인 하기 올바르게를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-125">Run `dotnet build` to verify the app builds correctly.</span></span> <span data-ttu-id="bbe07-126">첫 번째 실행에서 빌드 프로세스 몇 분 정도 걸릴 수 있는 npm 종속성을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-126">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="bbe07-127">후속 빌드는 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-127">Subsequent builds are much faster.</span></span>

<span data-ttu-id="bbe07-128">실행 `dotnet run` 앱을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-128">Run `dotnet run` to start the app.</span></span> <span data-ttu-id="bbe07-129">다음과 비슷한 메시지가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-129">A message similar to the following is logged:</span></span>

```console
Now listening on: http://localhost:<port>
```

<span data-ttu-id="bbe07-130">브라우저에서이 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-130">Navigate to this URL in a browser.</span></span>

<span data-ttu-id="bbe07-131">응용 프로그램의 백그라운드에서 각도 CLI 서버 인스턴스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-131">The app starts up an instance of the Angular CLI server in the background.</span></span> <span data-ttu-id="bbe07-132">다음과 비슷한 메시지가 기록 됩니다: *NG 라이브 개발 서버가 수신 하는 localhost:&lt;otherport&gt;, http://localhost에 브라우저를 열고:&lt;otherport&gt; /* .</span><span class="sxs-lookup"><span data-stu-id="bbe07-132">A message similar to the following is logged: *NG Live Development Server is listening on localhost:&lt;otherport&gt;, open your browser on http://localhost:&lt;otherport&gt;/*.</span></span> <span data-ttu-id="bbe07-133">이 메시지는 무시&mdash;있기 **하지** 결합 된 각도 CLI 및 ASP.NET Core 응용 프로그램에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-133">Ignore this message&mdash;it's **not** the URL for the combined ASP.NET Core and Angular CLI app.</span></span>

---

<span data-ttu-id="bbe07-134">프로젝트 템플릿은 각도 응용 프로그램 및 ASP.NET Core 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-134">The project template creates an ASP.NET Core app and an Angular app.</span></span> <span data-ttu-id="bbe07-135">ASP.NET Core 응용 프로그램은 데이터 액세스, 권한 부여 및 기타 서버 쪽 고려 사항에 대해 사용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-135">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="bbe07-136">에 있는 각 응용 프로그램의 *ClientApp* 하위 디렉터리를은 모든 UI 문제에 대 한 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-136">The Angular app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="bbe07-137">페이지, 이미지, 스타일, 모듈 등을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-137">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="bbe07-138">*ClientApp* 표준 각도 CLI 앱을 포함 하는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-138">The *ClientApp* directory contains a standard Angular CLI app.</span></span> <span data-ttu-id="bbe07-139">공식 참조 [각도 설명서](https://github.com/angular/angular-cli/wiki) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-139">See the official [Angular documentation](https://github.com/angular/angular-cli/wiki) for more information.</span></span>

<span data-ttu-id="bbe07-140">이 템플릿으로 만든 각도 앱과 자체 각도 CLI를 통해 만든 간에 약간의 차이가 있습니다 (통해 `ng new`); 그러나 응용 프로그램의 기능 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-140">There are slight differences between the Angular app created by this template and the one created by Angular CLI itself (via `ng new`); however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="bbe07-141">템플릿에서 만든 앱에 포함 되어는 [부트스트랩](https://getbootstrap.com/)-레이아웃 및 기본 라우팅 예제를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-141">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="run-ng-commands"></a><span data-ttu-id="bbe07-142">Ng 명령 실행</span><span class="sxs-lookup"><span data-stu-id="bbe07-142">Run ng commands</span></span>

<span data-ttu-id="bbe07-143">명령 프롬프트에서 전환 하는 *ClientApp* 하위 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="bbe07-143">In a command prompt, switch to the *ClientApp* subdirectory:</span></span>

```console
cd ClientApp
```

<span data-ttu-id="bbe07-144">있는 경우는 `ng` 전역으로 설치 하는 도구를 실행할 수 있습니다 해당 명령 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-144">If you have the `ng` tool installed globally, you can run any of its commands.</span></span> <span data-ttu-id="bbe07-145">예를 들어 실행할 수 있습니다 `ng lint`, `ng test`, 또는 다른 [각도 CLI 명령을](https://github.com/angular/angular-cli/wiki#additional-commands)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-145">For example, you can run `ng lint`, `ng test`, or any of the other [Angular CLI commands](https://github.com/angular/angular-cli/wiki#additional-commands).</span></span> <span data-ttu-id="bbe07-146">실행할 필요가 없는 `ng serve` 하지만 ASP.NET Core 응용 프로그램 처리 응용 프로그램의 서버 쪽 및 클라이언트 쪽 모두 부분을 처리 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-146">There's no need to run `ng serve` though, because your ASP.NET Core app deals with serving both server-side and client-side parts of your app.</span></span> <span data-ttu-id="bbe07-147">사용 하 여 내부적으로 `ng serve` 개발에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-147">Internally, it uses `ng serve` in development.</span></span>

<span data-ttu-id="bbe07-148">없는 경우는 `ng` 도구 설치 됨, 실행 `npm run ng` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-148">If you don't have the `ng` tool installed, run `npm run ng` instead.</span></span> <span data-ttu-id="bbe07-149">예를 들어 실행할 수 있습니다 `npm run ng lint` 또는 `npm run ng test`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-149">For example, you can run `npm run ng lint` or `npm run ng test`.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="bbe07-150">Npm 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-150">Install npm packages</span></span>

<span data-ttu-id="bbe07-151">제 3 자 npm 패키지를 설치 하려면 명령 프롬프트를 사용 하 여는 *ClientApp* 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-151">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="bbe07-152">예:</span><span class="sxs-lookup"><span data-stu-id="bbe07-152">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="bbe07-153">게시 및 배포</span><span class="sxs-lookup"><span data-stu-id="bbe07-153">Publish and deploy</span></span>

<span data-ttu-id="bbe07-154">개발, 응용 프로그램 개발자 편의 위해 최적화 된 모드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-154">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="bbe07-155">예를 들어 JavaScript 번들 (있도록를 디버깅할 때 원래 TypeScript 코드를 볼 수 있습니다) 소스 맵이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-155">For example, JavaScript bundles include source maps (so that when debugging, you can see your original TypeScript code).</span></span> <span data-ttu-id="bbe07-156">응용 프로그램 디스크에서 TypeScript, HTML 및 CSS 파일 변경 내용을 감시 하 고 자동으로 다시 컴파일 수 하 고이 변경 하 이러한 파일을 발견 시 다시 로드 하는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-156">The app watches for TypeScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="bbe07-157">프로덕션으로 성능에 최적화 된 응용 프로그램의 버전을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-157">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="bbe07-158">자동으로 실행 되도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-158">This is configured to happen automatically.</span></span> <span data-ttu-id="bbe07-159">게시 하면 빌드 구성을 내보냅니다는 축소 된, 미리 시간 (AoT) 컴파일된 클라이언트 쪽 코드의 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-159">When you publish, the build configuration emits a minified, ahead-of-time (AoT) compiled build of your client-side code.</span></span> <span data-ttu-id="bbe07-160">개발 빌드 달리 프로덕션 빌드 서버에 설치 되는 Node.js 필요 하지 않습니다 (활성화 하지 않은 경우 [서버 쪽 사전 렌더링이](#server-side-rendering)).</span><span class="sxs-lookup"><span data-stu-id="bbe07-160">Unlike the development build, the production build doesn't require Node.js to be installed on the server (unless you have enabled [server-side prerendering](#server-side-rendering)).</span></span>

<span data-ttu-id="bbe07-161">사용할 수 [ASP.NET Core 호스팅 및 배포 방법](xref:host-and-deploy/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-161">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-ng-serve-independently"></a><span data-ttu-id="bbe07-162">"Ng serve"를 독립적으로 실행</span><span class="sxs-lookup"><span data-stu-id="bbe07-162">Run "ng serve" independently</span></span>

<span data-ttu-id="bbe07-163">프로젝트 개발 모드에서 ASP.NET Core 응용 프로그램이 시작 하는 경우 백그라운드에서 각도 CLI 서버의 자체 인스턴스를 시작 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-163">The project is configured to start its own instance of the Angular CLI server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="bbe07-164">별도 서버를 수동으로 실행할 수 없기 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-164">This is convenient because you don't have to run a separate server manually.</span></span>

<span data-ttu-id="bbe07-165">이 기본 설정에는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-165">There's a drawback to this default setup.</span></span> <span data-ttu-id="bbe07-166">C# 코드와 응용 프로그램을 다시 시작 해야 하는 경우 ASP.NET 핵심을 수정할 때마다 각도 CLI 서버 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-166">Each time you modify your C# code and your ASP.NET Core app needs to restart, the Angular CLI server restarts.</span></span> <span data-ttu-id="bbe07-167">약 10 초를 다시 시작 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-167">Around 10 seconds is required to start back up.</span></span> <span data-ttu-id="bbe07-168">자주 C# 코드 편집 작업을 수행 하는 각도 CLI를 다시 시작 될 때까지 기다리는 하지 않으려는 경우 각도 CLI 서버 외부에서 ASP.NET Core 프로세스와 독립적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-168">If you're making frequent C# code edits and don't want to wait for Angular CLI to restart, run the Angular CLI server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="bbe07-169">이렇게 하려면</span><span class="sxs-lookup"><span data-stu-id="bbe07-169">To do so:</span></span>

1. <span data-ttu-id="bbe07-170">명령 프롬프트에서 전환 하는 *ClientApp* 하위 디렉터리 및 시작 각도 CLI 개발 서버:</span><span class="sxs-lookup"><span data-stu-id="bbe07-170">In a command prompt, switch to the *ClientApp* subdirectory, and launch the Angular CLI development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="bbe07-171">사용 하 여 `npm start` 하지 각도 CLI 개발 서버를 시작 하려면 `ng serve`되도록 구성에 *package.json* 가 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-171">Use `npm start` to launch the Angular CLI development server, not `ng serve`, so that the configuration in *package.json* is respected.</span></span> <span data-ttu-id="bbe07-172">관련 추가 각도 CLI 서버에 추가 매개 변수를 전달 하려면 `scripts` 줄 프로그램 *package.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-172">To pass additional parameters to the Angular CLI server, add them to the relevant `scripts` line in your *package.json* file.</span></span>

2. <span data-ttu-id="bbe07-173">자체 중 하나를 실행 하는 대신 외부 각도 CLI 인스턴스를 사용 하려면 ASP.NET Core 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-173">Modify your ASP.NET Core app to use the external Angular CLI instance instead of launching one of its own.</span></span> <span data-ttu-id="bbe07-174">사용자 *시작* 클래스, 대체는 `spa.UseAngularCliServer` 다음으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-174">In your *Startup* class, replace the `spa.UseAngularCliServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:4200");
    ```

<span data-ttu-id="bbe07-175">ASP.NET Core 응용 프로그램을 시작 하면 각 CLI 서버를 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-175">When you start your ASP.NET Core app, it won't launch an Angular CLI server.</span></span> <span data-ttu-id="bbe07-176">수동으로 시작 된 인스턴스가 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-176">The instance you started manually is used instead.</span></span> <span data-ttu-id="bbe07-177">이 통해 시작 하 고 더 빠르게 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-177">This enables it to start and restart faster.</span></span> <span data-ttu-id="bbe07-178">클라이언트 앱 될 때마다 다시 작성 하는 각도 CLI에 대 한 대기 중 더 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-178">It's no longer waiting for Angular CLI to rebuild your client app each time.</span></span>

## <a name="server-side-rendering"></a><span data-ttu-id="bbe07-179">서버 쪽 렌더링</span><span class="sxs-lookup"><span data-stu-id="bbe07-179">Server-side rendering</span></span>

<span data-ttu-id="bbe07-180">성능 기능으로, 클라이언트에서 실행할 뿐 아니라 서버에서 각 앱을 미리 렌더링을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-180">As a performance feature, you can choose to pre-render your Angular app on the server as well as running it on the client.</span></span> <span data-ttu-id="bbe07-181">이 경우에 브라우저 때문에 다운로드 하 고 JavaScript 번들을 실행 하기 전에 표시 될 응용 프로그램의 초기 UI를 나타내는 HTML 태그를 수신 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-181">This means that browsers receive HTML markup representing your app's initial UI, so they display it even before downloading and executing your JavaScript bundles.</span></span> <span data-ttu-id="bbe07-182">대부분이 구성의 호출 하는 각 기능에서 제공 [각도 유니버설](https://universal.angular.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-182">Most of the implementation of this comes from an Angular feature called [Angular Universal](https://universal.angular.io/).</span></span>

> [!TIP]
> <span data-ttu-id="bbe07-183">서버 쪽 렌더링을 사용 하도록 설정 (SSR) 많은 개발 및 배포 하는 동안 추가 문제가 모두를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-183">Enabling server-side rendering (SSR) introduces a number of extra complications both during development and deployment.</span></span> <span data-ttu-id="bbe07-184">읽기 [SSR의 단점](#drawbacks-of-ssr) SSR 요구 사항에 가장 잘 맞는 인지 확인 하려면.</span><span class="sxs-lookup"><span data-stu-id="bbe07-184">Read [drawbacks of SSR](#drawbacks-of-ssr) to determine if SSR is a good fit for your requirements.</span></span>

<span data-ttu-id="bbe07-185">SSR를 사용 하도록 설정 하려면 프로젝트에 추가 된 횟수를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-185">To enable SSR, you need to make a number of additions to your project.</span></span>

<span data-ttu-id="bbe07-186">에 *시작* 클래스 *후* 를 구성 하는 줄 `spa.Options.SourcePath`, 및 *하기 전에* 호출 `UseAngularCliServer` 또는 `UseProxyToSpaDevelopmentServer`, 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="bbe07-186">In the *Startup* class, *after* the line that configures `spa.Options.SourcePath`, and *before* the call to `UseAngularCliServer` or `UseProxyToSpaDevelopmentServer`, add the following:</span></span>

[!code-csharp[](sample/AngularServerSideRendering/Startup.cs?name=snippet_Call_UseSpa&highlight=5-12)]

<span data-ttu-id="bbe07-187">개발 모드에서이 코드는 스크립트를 실행 하 여 SSR 번들 작성 하려고 `build:ssr`에 정의 된 *ClientApp\package.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-187">In development mode, this code attempts to build the SSR bundle by running the script `build:ssr`, which is defined in *ClientApp\package.json*.</span></span> <span data-ttu-id="bbe07-188">각 앱 작성이 `ssr`, 아직 정의 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-188">This builds an Angular app named `ssr`, which isn't yet defined.</span></span> 

<span data-ttu-id="bbe07-189">끝에는 `apps` 배열로 *ClientApp/.angular-cli.json*, 이름을 사용 하 여 추가 앱 정의 `ssr`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-189">At the end of the `apps` array in *ClientApp/.angular-cli.json*, define an extra app with name `ssr`.</span></span> <span data-ttu-id="bbe07-190">다음 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-190">Use the following options:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/.angular-cli.json?range=24-41)]

<span data-ttu-id="bbe07-191">이 새 SSR 사용이 가능한 앱 구성에는 두 개의 추가 파일이 필요: *tsconfig.server.json* 및 *main.server.ts*합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-191">This new SSR-enabled app configuration requires two further files: *tsconfig.server.json* and *main.server.ts*.</span></span> <span data-ttu-id="bbe07-192">*tsconfig.server.json* 파일 TypeScript 컴파일 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-192">The *tsconfig.server.json* file specifies TypeScript compilation options.</span></span> <span data-ttu-id="bbe07-193">*main.server.ts* 파일 SSR 하는 동안 코드 진입점으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-193">The *main.server.ts* file serves as the code entry point during SSR.</span></span>

<span data-ttu-id="bbe07-194">라는 새 파일을 추가 *tsconfig.server.json* 내 *ClientApp/src* (기존 함께 *tsconfig.app.json*), 다음을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-194">Add a new file called *tsconfig.server.json* inside *ClientApp/src* (alongside the existing *tsconfig.app.json*), containing the following:</span></span>

[!code-json[](sample/AngularServerSideRendering/ClientApp/src/tsconfig.server.json)]

<span data-ttu-id="bbe07-195">이 파일의 각 AoT 컴파일러를 호출 하는 모듈을 찾도록 구성 `app.server.module`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-195">This file configures Angular's AoT compiler to look for a module called `app.server.module`.</span></span> <span data-ttu-id="bbe07-196">에 새 파일을 만들어이 추가할 *ClientApp/src/app/app.server.module.ts* (기존 함께 *app.module.ts*) 다음 포함 된:</span><span class="sxs-lookup"><span data-stu-id="bbe07-196">Add this by creating a new file at *ClientApp/src/app/app.server.module.ts* (alongside the existing *app.module.ts*) containing the following:</span></span> 

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/app/app.server.module.ts)]

<span data-ttu-id="bbe07-197">클라이언트 쪽에서이 모듈 상속 `app.module` SSR 하는 동안 사용할 수 있는 추가 Angular 모듈을 정의 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-197">This module inherits from your client-side `app.module` and defines which extra Angular modules are available during SSR.</span></span>

<span data-ttu-id="bbe07-198">이전에 설명한 대로 새 `ssr` 항목 *.angular cli.json* 라는 항목 지점 파일로 참조 *main.server.ts*합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-198">Recall that the new `ssr` entry in *.angular-cli.json* referenced an entry point file called *main.server.ts*.</span></span> <span data-ttu-id="bbe07-199">해당 파일을 아직 추가 하지 않은 하 고 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-199">You haven't yet added that file, and now is time to do so.</span></span> <span data-ttu-id="bbe07-200">에 새 파일을 만들 *ClientApp/src/main.server.ts* (기존 함께 *main.ts*), 다음을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-200">Create a new file at *ClientApp/src/main.server.ts* (alongside the existing *main.ts*), containing the following:</span></span>

[!code-typescript[](sample/AngularServerSideRendering/ClientApp/src/main.server.ts)]

<span data-ttu-id="bbe07-201">이 파일의이 코드를 실행할 때의 ASP.NET Core를 실행 각 요청에 대 한는 `UseSpaPrerendering` 에 추가 하는 미들웨어는 *시작* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-201">This file's code is what ASP.NET Core executes for each request when it runs the `UseSpaPrerendering` middleware that you added to the *Startup* class.</span></span> <span data-ttu-id="bbe07-202">수신 다루는 `params` (예: URL 요청 되 고),.NET 코드 및 결과 HTML을 가져올 각도 SSR Api를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-202">It deals with receiving `params` from the .NET code (such as the URL being requested), and making calls to Angular SSR APIs to get the resulting HTML.</span></span> 

<span data-ttu-id="bbe07-203">엄격 하 게-말하기, 이것이 SSR 개발 모드에서 사용 하도록 설정 하는 데 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-203">Strictly-speaking, this is sufficient to enable SSR in development mode.</span></span> <span data-ttu-id="bbe07-204">게시 된 경우 앱이 제대로 작동 되도록 한 마지막 변경 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-204">It's essential to make one final change so that your app works correctly when published.</span></span> <span data-ttu-id="bbe07-205">응용 프로그램의 main에서 *.csproj* 파일에서 설정 된 `BuildServerSideRenderer` 속성 값을 `true`:</span><span class="sxs-lookup"><span data-stu-id="bbe07-205">In your app's main *.csproj* file, set the `BuildServerSideRenderer` property value to `true`:</span></span>

[!code-xml[](sample/AngularServerSideRendering/AngularServerSideRendering.csproj?name=snippet_EnableBuildServerSideRenderer)]

<span data-ttu-id="bbe07-206">이렇게 하면 빌드 프로세스가 실행 되도록 구성 `build:ssr` 게시 하는 동안 SSR 파일 서버에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-206">This configures the build process to run `build:ssr` during publishing and deploy the SSR files to the server.</span></span> <span data-ttu-id="bbe07-207">이 사용 하지 않을 경우, 프로덕션 환경에서 SSR 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-207">If you don't enable this, SSR fails in production.</span></span>

<span data-ttu-id="bbe07-208">응용 프로그램 개발 또는 프로덕션 모드에서 실행 되 면 각도 코드가 미리 렌더링 되는 HTML로 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-208">When your app runs in either development or production mode, the Angular code pre-renders as HTML on the server.</span></span> <span data-ttu-id="bbe07-209">클라이언트 쪽 코드를 정상적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-209">The client-side code executes as normal.</span></span>

### <a name="pass-data-from-net-code-into-typescript-code"></a><span data-ttu-id="bbe07-210">TypeScript 코드를.NET 코드에서 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="bbe07-210">Pass data from .NET code into TypeScript code</span></span>

<span data-ttu-id="bbe07-211">SSR, 하는 동안 각 앱에 ASP.NET Core 응용 프로그램에서 요청 데이터를 전달 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-211">During SSR, you might want to pass per-request data from your ASP.NET Core app into your Angular app.</span></span> <span data-ttu-id="bbe07-212">예를 들어 쿠키 정보를 전달할 수 또는 데이터베이스에서 읽는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-212">For example, you could pass cookie information or something read from a database.</span></span> <span data-ttu-id="bbe07-213">이 작업을 수행 하려면 편집 하 여 *시작* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-213">To do this, edit your *Startup* class.</span></span> <span data-ttu-id="bbe07-214">에 대 한 콜백을 `UseSpaPrerendering`에 대 한 값 설정 `options.SupplyData` 다음과 같은:</span><span class="sxs-lookup"><span data-stu-id="bbe07-214">In the callback for `UseSpaPrerendering`, set a value for `options.SupplyData` such as the following:</span></span>

```csharp
options.SupplyData = (context, data) =>
{
    // Creates a new value called isHttpsRequest that's passed to TypeScript code
    data["isHttpsRequest"] = context.Request.IsHttps;
};
```

<span data-ttu-id="bbe07-215">`SupplyData` 전달 임의의 콜백 수, 요청, (문자열, 부울 또는 숫자)에 JSON 직렬화 가능한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-215">The `SupplyData` callback lets you pass arbitrary, per-request, JSON-serializable data (for example, strings, booleans, or numbers).</span></span> <span data-ttu-id="bbe07-216">프로그램 *main.server.ts* 관리 코드를 수신으로 `params.data`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-216">Your *main.server.ts* code receives this as `params.data`.</span></span> <span data-ttu-id="bbe07-217">위의 코드 예제는 부울 값으로 전달 하는 예를 들어 `params.data.isHttpsRequest` 에 `createServerRenderer` 콜백 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-217">For example, the preceding code sample passes a boolean value as `params.data.isHttpsRequest` into the `createServerRenderer` callback.</span></span> <span data-ttu-id="bbe07-218">각에서 지 원하는 어떤 방식으로든 응용 프로그램의 다른 부분에이 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-218">You can pass this to other parts of your app in any way supported by Angular.</span></span> <span data-ttu-id="bbe07-219">예를 들어 참조 방법을 *main.server.ts* 전달는 `BASE_URL` 값의 생성자는 받기 위해 선언 된 모든 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-219">For example, see how *main.server.ts* passes the `BASE_URL` value to any component whose constructor is declared to receive it.</span></span>

### <a name="drawbacks-of-ssr"></a><span data-ttu-id="bbe07-220">SSR의 단점</span><span class="sxs-lookup"><span data-stu-id="bbe07-220">Drawbacks of SSR</span></span>

<span data-ttu-id="bbe07-221">일부 앱 SSR에서 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-221">Not all apps benefit from SSR.</span></span> <span data-ttu-id="bbe07-222">주요 이점은 성능을 인식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-222">The primary benefit is perceived performance.</span></span> <span data-ttu-id="bbe07-223">느린 네트워크 연결을 통해 또는 느린 모바일 장치에 응용 프로그램에 도달 하는 방문자까지 약간의 시간이 데이터를 가져오거나 JavaScript 번들을 구문 분석 하는 경우에 초기 UI 신속 하 게 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-223">Visitors reaching your app over a slow network connection or on slow mobile devices see the initial UI quickly, even if it takes a while to fetch or parse the JavaScript bundles.</span></span> <span data-ttu-id="bbe07-224">그러나 많은 SPAs는 주로 빠른 컴퓨터 신속 하 고 내부 회사 네트워크를 통해 응용 프로그램이 거의 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-224">However, many SPAs are mainly used over fast, internal company networks on fast computers where the app appears almost instantly.</span></span>

<span data-ttu-id="bbe07-225">이와 동시에는 SSR를 사용 하도록 설정 하는 중요 한 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-225">At the same time, there are significant drawbacks to enabling SSR.</span></span> <span data-ttu-id="bbe07-226">개발 프로세스에 복잡성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-226">It adds complexity to your development process.</span></span> <span data-ttu-id="bbe07-227">코드는 두 개의 서로 다른 환경에서 실행 해야 합니다: 클라이언트 및 서버 쪽은 Node.js 환경에서 ASP.NET Core에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-227">Your code must run in two different environments: client-side and server-side (in a Node.js environment invoked from ASP.NET Core).</span></span> <span data-ttu-id="bbe07-228">기억해 야 할 일부의 원인 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-228">Here are some things to bear in mind:</span></span>

* <span data-ttu-id="bbe07-229">SSR은 프로덕션 서버에서 Node.js 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-229">SSR requires a Node.js installation on your production servers.</span></span> <span data-ttu-id="bbe07-230">Azure 앱 서비스 등의 일부 배포 시나리오에 대 한 있지만 대 한 Azure 서비스 패브릭 등의 다른 경우 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-230">This is automatically the case for some deployment scenarios, such as Azure App Services, but not for others, such as Azure Service Fabric.</span></span>
* <span data-ttu-id="bbe07-231">사용 하도록 설정는 `BuildServerSideRenderer` 플래그 원인 빌드 프로그램 *node_modules* 게시 하는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-231">Enabling the `BuildServerSideRenderer` build flag causes your *node_modules* directory to publish.</span></span> <span data-ttu-id="bbe07-232">이 폴더에 20, 000 명 파일이 배포 시간을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-232">This folder contains 20,000+ files, which increases deployment time.</span></span>
* <span data-ttu-id="bbe07-233">Node.js 환경에서 코드를 실행 하려면이를 사용할 수 없게 브라우저의 JavaScript Api의 존재 여부와 같은 `window` 또는 `localStorage`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-233">To run your code in a Node.js environment, it can't rely on the existence of browser-specific JavaScript APIs such as `window` or `localStorage`.</span></span> <span data-ttu-id="bbe07-234">코드 (또는 일부 다른 공급 업체 라이브러리 참조)를 하 려 하면 이러한 Api를 사용 하 여 얻게 됩니다 오류가 SSR 중.</span><span class="sxs-lookup"><span data-stu-id="bbe07-234">If your code (or some third-party library you reference) tries to use these APIs, you'll get an error during SSR.</span></span> <span data-ttu-id="bbe07-235">예를 들어 사용 하지 않는 jQuery 여러 위치에서 브라우저의 Api를 참조 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-235">For example, don't use jQuery because it references browser-specific APIs in many places.</span></span> <span data-ttu-id="bbe07-236">오류를 방지 하려면 SSR 것을 방지 하거나 브라우저 전용 Api 또는 라이브러리를 방지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-236">To prevent errors, you must either avoid SSR or avoid browser-specific APIs or libraries.</span></span> <span data-ttu-id="bbe07-237">위해 SSR 중에 호출 되지 않습니다 확인에 이러한 Api에 대 한 모든 호출을 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbe07-237">You can wrap any calls to such APIs in checks to ensure they aren't invoked during SSR.</span></span> <span data-ttu-id="bbe07-238">예를 들어 다음과 같은 확인을 사용 하 여 JavaScript 또는 TypeScript 코드에서:</span><span class="sxs-lookup"><span data-stu-id="bbe07-238">For example, use a check such as the following in JavaScript or TypeScript code:</span></span>

    ```javascript
    if (typeof window !== 'undefined') {
        // Call browser-specific APIs here
    }
    ```
