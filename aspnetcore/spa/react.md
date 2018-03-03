---
title: "React 프로젝트 템플릿을 사용 하 여"
author: SteveSandersonMS
description: "React 및 반응 만들기-앱에 대 한 ASP.NET Core 단일 페이지 응용 프로그램 (SPA) 프로젝트 템플릿으로 시작 하는 방법에 알아봅니다."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/react
ms.openlocfilehash: cda9f52d1f5fa1d240e210488bf1bd5c76e49be7
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="use-the-react-project-template"></a><span data-ttu-id="a3a13-103">React 프로젝트 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a3a13-103">Use the React project template</span></span>

> [!NOTE]
> <span data-ttu-id="a3a13-104">이 설명서 포함 되지 않습니다 React 프로젝트 템플릿에 대 한 ASP.NET 코어 2.0.</span><span class="sxs-lookup"><span data-stu-id="a3a13-104">This documentation isn't about the React project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="a3a13-105">최신 React 서식 파일을 수동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-105">It's about the newer React template to which you can update manually.</span></span> <span data-ttu-id="a3a13-106">서식 파일은 기본적으로 ASP.NET Core 2.1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

<span data-ttu-id="a3a13-107">업데이트 된 React 프로젝트 템플릿은 제공 편리한 시작점을 ASP.NET Core에 대 한 반응을 사용 하 여 앱 및 [react 만들기-app](https://github.com/facebookincubator/create-react-app) (CRA)는 다양 하 고 클라이언트 쪽 UI (사용자 인터페이스)를 구현 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-107">The updated React project template provides a convenient starting point for ASP.NET Core apps using React and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="a3a13-108">서식 파일에는 API 백 엔드 역할을 하는 ASP.NET Core 프로젝트와는 UI, 하지만 둘 다에서 작성 하 고 하나의 단위로 게시할 수 있는 단일 응용 프로그램 프로젝트를 호스트에서 편리 하 게 작동 하는 표준 CRA 반응 프로젝트를 만드는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-108">The template is equivalent to creating both an ASP.NET Core project to act as an API backend, and a standard CRA React project to act as a UI, but with the convenience of hosting both in a single app project that can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="a3a13-109">새 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a3a13-109">Create a new app</span></span>

<span data-ttu-id="a3a13-110">ASP.NET Core 2.0을 사용 하는 경우 확인 했습니다. [업데이트 React 프로젝트 템플릿을 설치](xref:spa/index#installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-110">If using ASP.NET Core 2.0, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span> <span data-ttu-id="a3a13-111">ASP.NET Core 2.1 있을 경우 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-111">If you have ASP.NET Core 2.1, there's no need to install it.</span></span>

<span data-ttu-id="a3a13-112">명령을 사용 하 여 명령 프롬프트에서 새 프로젝트 만들기 `dotnet new react` 빈 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-112">Create a new project from a command prompt using the command `dotnet new react` in an empty directory.</span></span> <span data-ttu-id="a3a13-113">예를 들어 다음 명령에서 응용 프로그램을 만듭니다는 *내-새-app* 디렉터리와 해당 디렉터리에 스위치:</span><span class="sxs-lookup"><span data-stu-id="a3a13-113">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new react -o my-new-app
cd my-new-app
```

<span data-ttu-id="a3a13-114">Visual Studio 또는.NET Core CLI에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-114">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a3a13-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3a13-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="a3a13-116">생성 된 열고 *.csproj* 파일, 및 여기에서 응용 프로그램 정상적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-116">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="a3a13-117">빌드 프로세스는 몇 분 정도 걸릴 수 있는 첫 번째 실행 시 npm 종속성을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-117">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="a3a13-118">후속 빌드는 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-118">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="a3a13-119">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="a3a13-119">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="a3a13-120">라는 환경 변수 해야 `ASPNETCORE_Environment` 의 값과 `Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-120">Ensure you have an environment variable called `ASPNETCORE_Environment` with value of `Development`.</span></span> <span data-ttu-id="a3a13-121">(비 PowerShell 프롬프트)의 Windows에서는 실행 `SET ASPNETCORE_Environment=Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-121">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="a3a13-122">Linux 또는 macOS 실행 `export ASPNETCORE_Environment=Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-122">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="a3a13-123">실행 [dotnet 빌드](/dotnet/core/tools/dotnet-build) 응용 프로그램을 확인 하려면 올바르게를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-123">Run [dotnet build](/dotnet/core/tools/dotnet-build) to verify your app builds correctly.</span></span> <span data-ttu-id="a3a13-124">첫 번째 실행에서 빌드 프로세스 몇 분 정도 걸릴 수 있는 npm 종속성을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-124">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="a3a13-125">후속 빌드는 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-125">Subsequent builds are much faster.</span></span>

<span data-ttu-id="a3a13-126">실행 [실행 dotnet](/dotnet/core/tools/dotnet-run) 앱을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-126">Run [dotnet run](/dotnet/core/tools/dotnet-run) to start the app.</span></span>

---

<span data-ttu-id="a3a13-127">프로젝트 템플릿은 React 응용 프로그램 및 ASP.NET Core 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-127">The project template creates an ASP.NET Core app and a React app.</span></span> <span data-ttu-id="a3a13-128">ASP.NET Core 응용 프로그램은 데이터 액세스, 권한 부여 및 기타 서버 쪽 고려 사항에 대해 사용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-128">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="a3a13-129">에 있는 React 앱은 *ClientApp* 하위 디렉터리를은 모든 UI 문제에 대 한 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-129">The React app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="a3a13-130">페이지, 이미지, 스타일, 모듈 등을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-130">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="a3a13-131">*ClientApp* 디렉터리는 표준 CRA 반응 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-131">The *ClientApp* directory is a standard CRA React app.</span></span> <span data-ttu-id="a3a13-132">공식 참조 [CRA 설명서](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-132">See the official [CRA documentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.</span></span>

<span data-ttu-id="a3a13-133">이 템플릿으로 만든 React 앱과 자체; CRA 하 여 만든 간에 약간의 차이가 있습니다. 그러나 응용 프로그램의 기능을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-133">There are slight differences between the React app created by this template and the one created by CRA itself; however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="a3a13-134">템플릿에서 만든 앱에 포함 되어는 [부트스트랩](https://getbootstrap.com/)-레이아웃 및 기본 라우팅 예제를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-134">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="a3a13-135">Npm 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-135">Install npm packages</span></span>

<span data-ttu-id="a3a13-136">제 3 자 npm 패키지를 설치 하려면 명령 프롬프트를 사용 하 여는 *ClientApp* 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-136">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="a3a13-137">예:</span><span class="sxs-lookup"><span data-stu-id="a3a13-137">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="a3a13-138">게시 및 배포</span><span class="sxs-lookup"><span data-stu-id="a3a13-138">Publish and deploy</span></span>

<span data-ttu-id="a3a13-139">개발, 응용 프로그램 개발자 편의 위해 최적화 된 모드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-139">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="a3a13-140">예를 들어 JavaScript 번들 (있도록를 디버깅할 때 원래 소스 코드를 볼 수 있습니다) 소스 맵이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-140">For example, JavaScript bundles include source maps (so that when debugging, you can see your original source code).</span></span> <span data-ttu-id="a3a13-141">응용 프로그램 JavaScript, HTML 및 CSS 파일을 디스크에 변경 내용을 감시 하 고 자동으로 다시 컴파일 수 하 고이 변경 하 이러한 파일을 발견 시 다시 로드 하는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-141">The app watches JavaScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="a3a13-142">프로덕션으로 성능에 최적화 된 응용 프로그램의 버전을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-142">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="a3a13-143">자동으로 실행 되도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-143">This is configured to happen automatically.</span></span> <span data-ttu-id="a3a13-144">게시 하면 빌드 구성을 클라이언트 쪽 코드의 경우, transpiled 빌드를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-144">When you publish, the build configuration emits a minified, transpiled build of your client-side code.</span></span> <span data-ttu-id="a3a13-145">개발 빌드 달리 프로덕션 빌드 서버에 설치 되는 Node.js 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-145">Unlike the development build, the production build doesn't require Node.js to be installed on the server.</span></span>

<span data-ttu-id="a3a13-146">사용할 수 [ASP.NET Core 호스팅 및 배포 방법](xref:host-and-deploy/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-146">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-the-cra-server-independently"></a><span data-ttu-id="a3a13-147">CRA 서버를 독립적으로 실행</span><span class="sxs-lookup"><span data-stu-id="a3a13-147">Run the CRA server independently</span></span>

<span data-ttu-id="a3a13-148">프로젝트 개발 모드에서 ASP.NET Core 응용 프로그램이 시작 하는 경우 백그라운드에서 고유한 인스턴스의 CRA 개발 서버를 시작 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-148">The project is configured to start its own instance of the CRA development server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="a3a13-149">별도 서버를 수동으로 실행할 수 없는 것을 의미 하기 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-149">This is convenient because it means you don't have to run a separate server manually.</span></span>

<span data-ttu-id="a3a13-150">이 기본 설정에는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-150">There's a drawback to this default setup.</span></span> <span data-ttu-id="a3a13-151">C# 코드와 응용 프로그램을 다시 시작 해야 하는 경우 ASP.NET 핵심을 수정할 때마다 CRA 서버 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-151">Each time you modify your C# code and your ASP.NET Core app needs to restart, the CRA server restarts.</span></span> <span data-ttu-id="a3a13-152">몇 초 정도 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-152">A few seconds are required to start back up.</span></span> <span data-ttu-id="a3a13-153">자주 수행 하면 경우 C# 코드를 편집 하 고 싶지 CRA 서버가 다시 시작 될 때까지 기다리는 CRA 서버 외부에서 ASP.NET Core 프로세스는 독립적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-153">If you're making frequent C# code edits and don't want to wait for the CRA server to restart, run the CRA server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="a3a13-154">이렇게 하려면</span><span class="sxs-lookup"><span data-stu-id="a3a13-154">To do so:</span></span>

1. <span data-ttu-id="a3a13-155">명령 프롬프트에서 전환 하는 *ClientApp* 하위 디렉터리 및 실행 CRA 개발 서버:</span><span class="sxs-lookup"><span data-stu-id="a3a13-155">In a command prompt, switch to the *ClientApp* subdirectory, and launch the CRA development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

2. <span data-ttu-id="a3a13-156">자체 중 하나를 실행 하는 대신 외부 CRA 서버 인스턴스를 사용 하려면 ASP.NET Core 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-156">Modify your ASP.NET Core app to use the external CRA server instance instead of launching one of its own.</span></span> <span data-ttu-id="a3a13-157">사용자 *시작* 클래스, 대체는 `spa.UseReactDevelopmentServer` 다음으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-157">In your *Startup* class, replace the `spa.UseReactDevelopmentServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

<span data-ttu-id="a3a13-158">ASP.NET Core 응용 프로그램을 시작 하면 CRA 서버를 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-158">When you start your ASP.NET Core app, it won't launch a CRA server.</span></span> <span data-ttu-id="a3a13-159">수동으로 시작 된 인스턴스가 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-159">The instance you started manually is used instead.</span></span> <span data-ttu-id="a3a13-160">이 통해 시작 하 고 더 빠르게 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-160">This enables it to start and restart faster.</span></span> <span data-ttu-id="a3a13-161">더 이상 될 때마다 다시 작성 하려면 React 앱에 대 한 대기입니다.</span><span class="sxs-lookup"><span data-stu-id="a3a13-161">It's no longer waiting for your React app to rebuild each time.</span></span>
