---
title: 파일 감시자를 사용하여 ASP.NET Core 앱 개발
author: rick-anderson
description: 이 자습서에서는 ASP.NET Core 앱에서 .NET Core CLI 파일 감시자(dotnet 조사식) 도구를 사용하는 방법을 보여줍니다.
ms.author: riande
ms.date: 05/31/2018
uid: tutorials/dotnet-watch
ms.openlocfilehash: 2a59267b36faf1e00ea2f0cc7e2b9ceb9828f791
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278855"
---
# <a name="develop-aspnet-core-apps-using-a-file-watcher"></a><span data-ttu-id="343fe-103">파일 감시자를 사용하여 ASP.NET Core 앱 개발</span><span class="sxs-lookup"><span data-stu-id="343fe-103">Develop ASP.NET Core apps using a file watcher</span></span>

<span data-ttu-id="343fe-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Victor Hurdugaci](https://twitter.com/victorhurdugaci)</span><span class="sxs-lookup"><span data-stu-id="343fe-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Victor Hurdugaci](https://twitter.com/victorhurdugaci)</span></span>

<span data-ttu-id="343fe-105">`dotnet watch`은 원본 파일을 변경할 때 [.NET Core CLI](/dotnet/core/tools) 명령을 실행하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-105">`dotnet watch` is a tool that runs a [.NET Core CLI](/dotnet/core/tools) command when source files change.</span></span> <span data-ttu-id="343fe-106">예를 들어 파일 변경은 컴파일, 테스트 실행 또는 배포를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-106">For example, a file change can trigger compilation, test execution, or deployment.</span></span>

<span data-ttu-id="343fe-107">이 자습서에서는 합계를 반환하는 엔드포인트 및 제품을 반환하는 엔드포인트 등 두 개의 엔드포인트에서 기존 Web API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-107">This tutorial uses an existing web API with two endpoints: one that returns a sum and one that returns a product.</span></span> <span data-ttu-id="343fe-108">제품 메서드에는 버그가 있습니다. 이 문제가 이 자습서에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-108">The product method has a bug, which is fixed in this tutorial.</span></span>

<span data-ttu-id="343fe-109">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-109">Download the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample).</span></span> <span data-ttu-id="343fe-110">*WebApp*(ASP.NET Core Web API) 및 *WebAppTests*(Web API의 단위 테스트)라는 두 개의 프로젝트로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-110">It consists of two projects: *WebApp* (an ASP.NET Core web API) and *WebAppTests* (unit tests for the web API).</span></span>

<span data-ttu-id="343fe-111">명령 셸에서 *WebApp* 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-111">In a command shell, navigate to the *WebApp* folder.</span></span> <span data-ttu-id="343fe-112">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-112">Run the following command:</span></span>

```console
dotnet run
```

<span data-ttu-id="343fe-113">콘솔 출력은 다음과 유사한 메시지를 표시합니다(앱이 실행되고 요청을 대기하는 것을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="343fe-113">The console output shows messages similar to the following (indicating that the app is running and awaiting requests):</span></span>

```console
$ dotnet run
Hosting environment: Development
Content root path: C:/Docs/aspnetcore/tutorials/dotnet-watch/sample/WebApp
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="343fe-114">웹 브라우저에서 `http://localhost:<port number>/api/math/sum?a=4&b=5`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-114">In a web browser, navigate to `http://localhost:<port number>/api/math/sum?a=4&b=5`.</span></span> <span data-ttu-id="343fe-115">`9`라는 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-115">You should see the result of `9`.</span></span>

<span data-ttu-id="343fe-116">API 제품으로 이동합니다(`http://localhost:<port number>/api/math/product?a=4&b=5`).</span><span class="sxs-lookup"><span data-stu-id="343fe-116">Navigate to the product API (`http://localhost:<port number>/api/math/product?a=4&b=5`).</span></span> <span data-ttu-id="343fe-117">예상한 대로 `20`이 아니라 `9`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-117">It returns `9`, not `20` as you'd expect.</span></span> <span data-ttu-id="343fe-118">이러한 문제는이 자습서의 뒷부분에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-118">That problem is fixed later in the tutorial.</span></span>

::: moniker range="<= aspnetcore-2.0"

## <a name="add-dotnet-watch-to-a-project"></a><span data-ttu-id="343fe-119">프로젝트에 `dotnet watch` 추가</span><span class="sxs-lookup"><span data-stu-id="343fe-119">Add `dotnet watch` to a project</span></span>

<span data-ttu-id="343fe-120">`dotnet watch` 파일 감시자 도구는 .NET Core SDK 버전 2.1.300에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-120">The `dotnet watch` file watcher tool is included with version 2.1.300 of the .NET Core SDK.</span></span> <span data-ttu-id="343fe-121">다음 단계는 이전 버전의 .NET Core SDK를 사용하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-121">The following steps are required when using an earlier version of the .NET Core SDK.</span></span>

1. <span data-ttu-id="343fe-122">`Microsoft.DotNet.Watcher.Tools` 패키지 참조를 *.csproj* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-122">Add a `Microsoft.DotNet.Watcher.Tools` package reference to the *.csproj* file:</span></span>

    ```xml
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup>
    ```

1. <span data-ttu-id="343fe-123">다음 명령을 실행하여 `Microsoft.DotNet.Watcher.Tools` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-123">Install the `Microsoft.DotNet.Watcher.Tools` package by running the following command:</span></span>

    ```console
    dotnet restore
    ```

::: moniker-end

## <a name="run-net-core-cli-commands-using-dotnet-watch"></a><span data-ttu-id="343fe-124">`dotnet watch`를 사용하여 .NET Core CLI 명령 실행</span><span class="sxs-lookup"><span data-stu-id="343fe-124">Run .NET Core CLI commands using `dotnet watch`</span></span>

<span data-ttu-id="343fe-125">모든 [.NET Core CLI 명령](/dotnet/core/tools#cli-commands)을 `dotnet watch`로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-125">Any [.NET Core CLI command](/dotnet/core/tools#cli-commands) can be run with `dotnet watch`.</span></span> <span data-ttu-id="343fe-126">예:</span><span class="sxs-lookup"><span data-stu-id="343fe-126">For example:</span></span>

| <span data-ttu-id="343fe-127">명령</span><span class="sxs-lookup"><span data-stu-id="343fe-127">Command</span></span> | <span data-ttu-id="343fe-128">watch를 사용하는 명령</span><span class="sxs-lookup"><span data-stu-id="343fe-128">Command with watch</span></span> |
| ---- | ----- |
| <span data-ttu-id="343fe-129">dotnet run</span><span class="sxs-lookup"><span data-stu-id="343fe-129">dotnet run</span></span> | <span data-ttu-id="343fe-130">dotnet watch run</span><span class="sxs-lookup"><span data-stu-id="343fe-130">dotnet watch run</span></span> |
| <span data-ttu-id="343fe-131">dotnet run -f netcoreapp2.0</span><span class="sxs-lookup"><span data-stu-id="343fe-131">dotnet run -f netcoreapp2.0</span></span> | <span data-ttu-id="343fe-132">dotnet watch run -f netcoreapp2.0</span><span class="sxs-lookup"><span data-stu-id="343fe-132">dotnet watch run -f netcoreapp2.0</span></span> |
| <span data-ttu-id="343fe-133">dotnet run -f netcoreapp2.0 -- --arg1</span><span class="sxs-lookup"><span data-stu-id="343fe-133">dotnet run -f netcoreapp2.0 -- --arg1</span></span> | <span data-ttu-id="343fe-134">dotnet watch run -f netcoreapp2.0 -- --arg1</span><span class="sxs-lookup"><span data-stu-id="343fe-134">dotnet watch run -f netcoreapp2.0 -- --arg1</span></span> |
| <span data-ttu-id="343fe-135">dotnet test</span><span class="sxs-lookup"><span data-stu-id="343fe-135">dotnet test</span></span> | <span data-ttu-id="343fe-136">dotnet watch 테스트</span><span class="sxs-lookup"><span data-stu-id="343fe-136">dotnet watch test</span></span> |

<span data-ttu-id="343fe-137">*WebApp* 폴더에서 `dotnet watch run`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-137">Run `dotnet watch run` in the *WebApp* folder.</span></span> <span data-ttu-id="343fe-138">콘솔 출력은 `watch`가 시작했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-138">The console output indicates `watch` has started.</span></span>

## <a name="make-changes-with-dotnet-watch"></a><span data-ttu-id="343fe-139">`dotnet watch` 변경</span><span class="sxs-lookup"><span data-stu-id="343fe-139">Make changes with `dotnet watch`</span></span>

<span data-ttu-id="343fe-140">`dotnet watch`가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-140">Make sure `dotnet watch` is running.</span></span>

<span data-ttu-id="343fe-141">합계가 아닌 제품을 반환하도록 *MathController.cs*의 `Product` 메서드에서 버그를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-141">Fix the bug in the `Product` method of *MathController.cs* so it returns the product and not the sum:</span></span>

```csharp
public static int Product(int a, int b)
{
  return a * b;
}
```

<span data-ttu-id="343fe-142">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-142">Save the file.</span></span> <span data-ttu-id="343fe-143">콘솔 출력은 `dotnet watch`에서 파일 변경을 검색했고 앱을 다시 시작했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-143">The console output indicates that `dotnet watch` detected a file change and restarted the app.</span></span>

<span data-ttu-id="343fe-144">`http://localhost:<port number>/api/math/product?a=4&b=5`에서 올바른 결과를 반환하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-144">Verify `http://localhost:<port number>/api/math/product?a=4&b=5` returns the correct result.</span></span>

## <a name="run-tests-using-dotnet-watch"></a><span data-ttu-id="343fe-145">`dotnet watch`를 사용하여 테스트 실행</span><span class="sxs-lookup"><span data-stu-id="343fe-145">Run tests using `dotnet watch`</span></span>

1. <span data-ttu-id="343fe-146">*MathController.cs*의 `Product` 메서드가 합계를 반환하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-146">Change the `Product` method of *MathController.cs* back to returning the sum.</span></span> <span data-ttu-id="343fe-147">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-147">Save the file.</span></span>
1. <span data-ttu-id="343fe-148">명령 셸에서 *WebAppTests* 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-148">In a command shell, navigate to the *WebAppTests* folder.</span></span>
1. <span data-ttu-id="343fe-149">[dotnet restore](/dotnet/core/tools/dotnet-restore)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-149">Run [dotnet restore](/dotnet/core/tools/dotnet-restore).</span></span>
1. <span data-ttu-id="343fe-150">`dotnet watch test`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-150">Run `dotnet watch test`.</span></span> <span data-ttu-id="343fe-151">이 출력은 테스트에 실패했으며 감시자가 파일 변경을 대기 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-151">Its output indicates that a test failed and that the watcher is awaiting file changes:</span></span>

     ```console
     Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
     Test Run Failed.
     ```

1. <span data-ttu-id="343fe-152">제품을 반환하도록 `Product` 메서드 코드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-152">Fix the `Product` method code so it returns the product.</span></span> <span data-ttu-id="343fe-153">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-153">Save the file.</span></span>

<span data-ttu-id="343fe-154">`dotnet watch`는 파일 변경을 검색하고 테스트를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-154">`dotnet watch` detects the file change and reruns the tests.</span></span> <span data-ttu-id="343fe-155">콘솔 출력은 통과된 테스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-155">The console output indicates the tests passed.</span></span>

## <a name="customize-files-list-to-watch"></a><span data-ttu-id="343fe-156">조사할 파일 목록 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="343fe-156">Customize files list to watch</span></span>

<span data-ttu-id="343fe-157">기본적으로 `dotnet-watch`는 다음 GLOB 패턴과 일치하는 모든 파일을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-157">By default, `dotnet-watch` tracks all files matching the following glob patterns:</span></span>

* `**/*.cs`
* `*.csproj`
* `**/*.resx`

<span data-ttu-id="343fe-158">*.csproj* 파일을 편집하여 조사식 목록에 더 많은 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-158">More items can be added to the watch list by editing the *.csproj* file.</span></span> <span data-ttu-id="343fe-159">개별적으로 또는 GLOB 패턴을 사용하여 항목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-159">Items can be specified individually or by using glob patterns.</span></span>

```xml
<ItemGroup>
    <!-- extends watching group to include *.js files -->
    <Watch Include="**\*.js" Exclude="node_modules\**\*;**\*.js.map;obj\**\*;bin\**\*" />
</ItemGroup>
```

## <a name="opt-out-of-files-to-be-watched"></a><span data-ttu-id="343fe-160">감시할 파일 옵트아웃</span><span class="sxs-lookup"><span data-stu-id="343fe-160">Opt-out of files to be watched</span></span>

<span data-ttu-id="343fe-161">기본 설정을 무시하도록 `dotnet-watch`를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-161">`dotnet-watch` can be configured to ignore its default settings.</span></span> <span data-ttu-id="343fe-162">특정 파일을 무시하려면 *.csproj* 파일에서 `Watch="false"` 특성을 항목의 정의로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-162">To ignore specific files, add the `Watch="false"` attribute to an item's definition in the *.csproj* file:</span></span>

```xml
<ItemGroup>
    <!-- exclude Generated.cs from dotnet-watch -->
    <Compile Include="Generated.cs" Watch="false" />

    <!-- exclude Strings.resx from dotnet-watch -->
    <EmbeddedResource Include="Strings.resx" Watch="false" />

    <!-- exclude changes in this referenced project -->
    <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj" Watch="false" />
</ItemGroup>
```

## <a name="custom-watch-projects"></a><span data-ttu-id="343fe-163">사용자 정의 조사식 프로젝트</span><span class="sxs-lookup"><span data-stu-id="343fe-163">Custom watch projects</span></span>

<span data-ttu-id="343fe-164">`dotnet-watch`는 C# 프로젝트로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-164">`dotnet-watch` isn't restricted to C# projects.</span></span> <span data-ttu-id="343fe-165">다른 시나리오를 처리하도록 사용자 지정 조사식 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-165">Custom watch projects can be created to handle different scenarios.</span></span> <span data-ttu-id="343fe-166">다음 프로젝트 레이아웃을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-166">Consider the following project layout:</span></span>

* <span data-ttu-id="343fe-167">**test/**</span><span class="sxs-lookup"><span data-stu-id="343fe-167">**test/**</span></span>
  * <span data-ttu-id="343fe-168">*UnitTests/UnitTests.csproj*</span><span class="sxs-lookup"><span data-stu-id="343fe-168">*UnitTests/UnitTests.csproj*</span></span>
  * <span data-ttu-id="343fe-169">*IntegrationTests/IntegrationTests.csproj*</span><span class="sxs-lookup"><span data-stu-id="343fe-169">*IntegrationTests/IntegrationTests.csproj*</span></span>

<span data-ttu-id="343fe-170">두 프로젝트를 조사하는 것이 목적인 경우 두 프로젝트를 감시하도록 구성된 사용자 지정 프로젝트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-170">If the goal is to watch both projects, create a custom project file configured to watch both projects:</span></span>

```xml
<Project>
    <ItemGroup>
        <TestProjects Include="**\*.csproj" />
        <Watch Include="**\*.cs" />
    </ItemGroup>

    <Target Name="Test">
        <MSBuild Targets="VSTest" Projects="@(TestProjects)" />
    </Target>

    <Import Project="$(MSBuildExtensionsPath)\Microsoft.Common.targets" />
</Project>
```

<span data-ttu-id="343fe-171">파일이 두 프로젝트를 감시하는 시작하려면 *test* 폴더를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-171">To start file watching on both projects, change to the *test* folder.</span></span> <span data-ttu-id="343fe-172">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-172">Execute the following command:</span></span>

```console
dotnet watch msbuild /t:Test
```

<span data-ttu-id="343fe-173">테스트 프로젝트 중 하나에서 파일을 변경하면 VSTest가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-173">VSTest executes when any file changes in either test project.</span></span>

## <a name="dotnet-watch-in-github"></a><span data-ttu-id="343fe-174">GitHub의 `dotnet-watch`</span><span class="sxs-lookup"><span data-stu-id="343fe-174">`dotnet-watch` in GitHub</span></span>

<span data-ttu-id="343fe-175">`dotnet-watch`는 GitHub [DotNetTools 리포지토리](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="343fe-175">`dotnet-watch` is part of the GitHub [DotNetTools repository](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-watch).</span></span>
