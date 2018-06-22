---
title: ASP.NET Core에 React 프로젝트 템플릿 사용
author: SteveSandersonMS
description: React 및 create-react-app에 대한 ASP.NET Core SPA(단일 페이지 응용 프로그램) 프로젝트 템플릿을 시작하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/react
ms.openlocfilehash: 721ea1d4197ddd17dde657924f12dee2a6858d97
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36291506"
---
# <a name="use-the-react-project-template-with-aspnet-core"></a><span data-ttu-id="cb37a-103">ASP.NET Core에 React 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="cb37a-103">Use the React project template with ASP.NET Core</span></span>

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> <span data-ttu-id="cb37a-104">이 문서는 ASP.NET Core 2.0에 포함된 React 프로젝트 템플릿에 대한 내용이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-104">This documentation isn't about the React project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="cb37a-105">수동으로 업데이트할 수 있는 최신 React 템플릿에 대한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-105">It's about the newer React template to which you can update manually.</span></span> <span data-ttu-id="cb37a-106">템플릿은 ASP.NET Core 2.1에 기본적으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

::: moniker-end

<span data-ttu-id="cb37a-107">업데이트된 React 프로젝트 템플릿은 React 및 CRA([create-react-app](https://github.com/facebookincubator/create-react-app)) 규칙을 사용하여 풍부한 클라이언트 쪽 UI(사용자 인터페이스)를 구현하는 ASP.NET Core 앱에 대한 편리한 시작점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-107">The updated React project template provides a convenient starting point for ASP.NET Core apps using React and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="cb37a-108">이 템플릿은 API 백 엔드로 사용되는 ASP.NET Core 프로젝트 및 UI로 사용되는 표준 CRA React 프로젝트를 둘 다 만드는 것과 동일하지만, 단일 단위로 빌드 및 게시할 수 있는 단일 앱 프로젝트에 두 프로젝트를 모두 편리하게 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-108">The template is equivalent to creating both an ASP.NET Core project to act as an API backend, and a standard CRA React project to act as a UI, but with the convenience of hosting both in a single app project that can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="cb37a-109">새 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="cb37a-109">Create a new app</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="cb37a-110">ASP.NET Core 2.0을 사용하는 경우 [업데이트된 React 프로젝트 템플릿을 설치](xref:spa/index#installation)했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-110">If using ASP.NET Core 2.0, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span>

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="cb37a-111">ASP.NET Core 2.1이 설치 되어 있을 경우 React 프로젝트 템플릿을 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-111">If you have ASP.NET Core 2.1 installed, there's no need to install the React project template.</span></span>

::: moniker-end

<span data-ttu-id="cb37a-112">빈 디렉터리에 `dotnet new react` 명령을 사용하여 명령 프롬프트에서 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-112">Create a new project from a command prompt using the command `dotnet new react` in an empty directory.</span></span> <span data-ttu-id="cb37a-113">예를 들어 다음 명령은 *my-new-app* 디렉터리에 앱을 만들고 해당 디렉터리로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-113">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new react -o my-new-app
cd my-new-app
```

<span data-ttu-id="cb37a-114">Visual Studio 또는 .NET Core CLI에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-114">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="cb37a-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb37a-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="cb37a-116">생성된 *.csproj* 파일을 열고 여기에서 정상적으로 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-116">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="cb37a-117">빌드 프로세스는 첫 번째 실행에서 npm 종속성을 복원하고 이 작업에는 몇 분 정도 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-117">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="cb37a-118">후속 빌드는 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-118">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="cb37a-119">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="cb37a-119">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="cb37a-120">`Development` 값을 가진 `ASPNETCORE_Environment` 환경 변수가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-120">Ensure you have an environment variable called `ASPNETCORE_Environment` with value of `Development`.</span></span> <span data-ttu-id="cb37a-121">Windows(PowerShell 이외의 프롬프트)에서 `SET ASPNETCORE_Environment=Development`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-121">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="cb37a-122">Linux 또는 macOS에서 `export ASPNETCORE_Environment=Development`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-122">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="cb37a-123">[dotnet build](/dotnet/core/tools/dotnet-build)를 실행하여 앱이 제대로 빌드되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-123">Run [dotnet build](/dotnet/core/tools/dotnet-build) to verify your app builds correctly.</span></span> <span data-ttu-id="cb37a-124">첫 번째 실행에서 빌드 프로세스는 npm 종속성을 복원하고 이 작업에는 몇 분 정도 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-124">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="cb37a-125">후속 빌드는 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-125">Subsequent builds are much faster.</span></span>

<span data-ttu-id="cb37a-126">[dotnet run](/dotnet/core/tools/dotnet-run)을 실행하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-126">Run [dotnet run](/dotnet/core/tools/dotnet-run) to start the app.</span></span>

---

<span data-ttu-id="cb37a-127">프로젝트 템플릿은 ASP.NET Core 앱과 React 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-127">The project template creates an ASP.NET Core app and a React app.</span></span> <span data-ttu-id="cb37a-128">ASP.NET Core 앱은 데이터 액세스, 권한 부여 및 기타 서버 쪽 문제에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-128">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="cb37a-129">*ClientApp* 하위 디렉터리에 있는 React 앱은 모든 UI 문제에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-129">The React app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="cb37a-130">페이지, 이미지, 스타일, 모듈 등을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-130">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="cb37a-131">*ClientApp* 디렉터리는 표준 CRA React 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-131">The *ClientApp* directory is a standard CRA React app.</span></span> <span data-ttu-id="cb37a-132">자세한 내용은 공식 [CRA 설명서](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb37a-132">See the official [CRA documentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.</span></span>

<span data-ttu-id="cb37a-133">이 템플릿에서 만들어진 React 앱과 CRA 자체에서 만들어진 앱 간에는 약간 차이가 있지만 앱의 기능은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-133">There are slight differences between the React app created by this template and the one created by CRA itself; however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="cb37a-134">템플릿에서 만들어진 앱에는 [부트스트랩](https://getbootstrap.com/) 기반 레이아웃 및 기본 라우팅 예제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-134">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="cb37a-135">npm 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="cb37a-135">Install npm packages</span></span>

<span data-ttu-id="cb37a-136">타사 npm 패키지를 설치하려면 *ClientApp* 하위 디렉터리에서 명령 프롬프트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-136">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="cb37a-137">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="cb37a-137">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="cb37a-138">게시 및 배포</span><span class="sxs-lookup"><span data-stu-id="cb37a-138">Publish and deploy</span></span>

<span data-ttu-id="cb37a-139">개발 시에 앱은 개발자 편의를 위해 최적화된 모드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-139">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="cb37a-140">예를 들어 디버그할 때 원래 소스 코드를 볼 수 있도록 JavaScript 번들에 소스 맵이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-140">For example, JavaScript bundles include source maps (so that when debugging, you can see your original source code).</span></span> <span data-ttu-id="cb37a-141">앱은 디스크에서 JavaScript, HTML 및 CSS 파일 변경 내용을 감시하고 해당 파일의 변경을 확인하면 자동으로 다시 컴파일하고 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-141">The app watches JavaScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="cb37a-142">프로덕션 시에는 성능에 최적화된 앱의 버전을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-142">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="cb37a-143">이는 자동으로 수행하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-143">This is configured to happen automatically.</span></span> <span data-ttu-id="cb37a-144">게시할 때 빌드 구성은 클라이언트 쪽 코드의 축소된 변환 컴파일된 빌드를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-144">When you publish, the build configuration emits a minified, transpiled build of your client-side code.</span></span> <span data-ttu-id="cb37a-145">개발 빌드와 달리 프로덕션 빌드는 서버에 Node.js를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-145">Unlike the development build, the production build doesn't require Node.js to be installed on the server.</span></span>

<span data-ttu-id="cb37a-146">표준 [ASP.NET Core 호스팅 및 배포 방법](xref:host-and-deploy/index)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-146">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-the-cra-server-independently"></a><span data-ttu-id="cb37a-147">개별적으로 CRA 서버 실행</span><span class="sxs-lookup"><span data-stu-id="cb37a-147">Run the CRA server independently</span></span>

<span data-ttu-id="cb37a-148">프로젝트는 ASP.NET Core 앱이 개발 모드에서 시작될 때 백그라운드에서 CRA 개발 서버의 자체 인스턴스를 시작하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-148">The project is configured to start its own instance of the CRA development server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="cb37a-149">이 방법은 별도의 서버를 수동으로 실행할 필요가 없기 때문에 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-149">This is convenient because it means you don't have to run a separate server manually.</span></span>

<span data-ttu-id="cb37a-150">이 기본 설정에는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-150">There's a drawback to this default setup.</span></span> <span data-ttu-id="cb37a-151">C# 코드를 수정하고 ASP.NET Core 앱을 다시 시작해야 할 때마다 CRA 서버가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-151">Each time you modify your C# code and your ASP.NET Core app needs to restart, the CRA server restarts.</span></span> <span data-ttu-id="cb37a-152">백업을 시작하려면 몇 초 정도가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-152">A few seconds are required to start back up.</span></span> <span data-ttu-id="cb37a-153">C# 코드를 자주 편집하고 있고 CRA 서버가 다시 시작될 때까지 기다리지 않으려면 ASP.NET Core 프로세스와는 별도로 CRA 서버를 외부에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-153">If you're making frequent C# code edits and don't want to wait for the CRA server to restart, run the CRA server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="cb37a-154">이를 수행하려면:</span><span class="sxs-lookup"><span data-stu-id="cb37a-154">To do so:</span></span>

1. <span data-ttu-id="cb37a-155">명령 프롬프트에서 *ClientApp* 하위 디렉터리로 전환하고 CRA 개발 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-155">In a command prompt, switch to the *ClientApp* subdirectory, and launch the CRA development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

2. <span data-ttu-id="cb37a-156">자체 인스턴스 중 하나를 시작하지 않고 외부 CRA 서버 인스턴스를 사용하도록 ASP.NET Core 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-156">Modify your ASP.NET Core app to use the external CRA server instance instead of launching one of its own.</span></span> <span data-ttu-id="cb37a-157">*Startup* 클래스에서 `spa.UseReactDevelopmentServer` 호출을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-157">In your *Startup* class, replace the `spa.UseReactDevelopmentServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

<span data-ttu-id="cb37a-158">ASP.NET Core 앱을 시작할 때 CRA 서버는 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-158">When you start your ASP.NET Core app, it won't launch a CRA server.</span></span> <span data-ttu-id="cb37a-159">수동으로 시작한 인스턴스가 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-159">The instance you started manually is used instead.</span></span> <span data-ttu-id="cb37a-160">이를 통해 더 빠르게 시작하고 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-160">This enables it to start and restart faster.</span></span> <span data-ttu-id="cb37a-161">더 이상 React 앱이 매번 다시 빌드할 때까지 기다리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb37a-161">It's no longer waiting for your React app to rebuild each time.</span></span>
