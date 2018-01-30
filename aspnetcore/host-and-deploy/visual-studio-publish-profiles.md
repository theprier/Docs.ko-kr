---
title: "Visual Studio ASP.NET Core 응용 프로그램 배포에 대 한 프로필 게시"
author: rick-anderson
description: "만드는 방법을 익힐 Visual Studio에서 ASP.NET Core 응용 프로그램에 대 한 프로필을 게시 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 09/26/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/visual-studio-publish-profiles
ms.openlocfilehash: 138b60d0e7c2a3d8848d534ffed854feaf0f5661
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="visual-studio-publish-profiles-for-aspnet-core-app-deployment"></a><span data-ttu-id="f7473-103">Visual Studio ASP.NET Core 응용 프로그램 배포에 대 한 프로필 게시</span><span class="sxs-lookup"><span data-stu-id="f7473-103">Visual Studio publish profiles for ASP.NET Core app deployment</span></span>

<span data-ttu-id="f7473-104">작성자: [Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f7473-104">By [Sayed Ibrahim Hashimi](https://github.com/sayedihashimi) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f7473-105">이 문서에서는 Visual Studio 2017을 사용하여 게시 프로필을 만드는 방법에 초점을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-105">This article focuses on using Visual Studio 2017 to create publish profiles.</span></span> <span data-ttu-id="f7473-106">Visual Studio에서 만들어진 게시 프로필은 MSBuild 및 Visual Studio 2017에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-106">The publish profiles created with Visual Studio can be run from MSBuild and Visual Studio 2017.</span></span> <span data-ttu-id="f7473-107">문서는 게시 프로세스의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-107">The article provides details of the publishing process.</span></span> <span data-ttu-id="f7473-108">Azure에 게시에 관한 지침은 [Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시](xref:tutorials/publish-to-azure-webapp-using-vs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7473-108">See [Publish an ASP.NET Core web app to Azure App Service using Visual Studio](xref:tutorials/publish-to-azure-webapp-using-vs) for instructions on publishing to Azure.</span></span>

<span data-ttu-id="f7473-109">다음 *.csproj* 파일은 `dotnet new mvc` 명령을 사용하여 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-109">The following *.csproj* file was created with the command `dotnet new mvc`:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="f7473-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="f7473-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
  </ItemGroup>

  <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
  </ItemGroup>

</Project>
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="f7473-111">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="f7473-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp1.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore" Version="1.1.5" />
    <PackageReference Include="Microsoft.AspNetCore.Mvc" Version="1.1.6" />
    <PackageReference Include="Microsoft.AspNetCore.StaticFiles" Version="1.1.3" />
  </ItemGroup>

</Project>
```

---

<span data-ttu-id="f7473-112">위 태그의 첫째 줄에 있는 `<Project>` 요소의 `Sdk` 특성은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-112">The `Sdk` attribute in the `<Project>` element (in the first line) of the markup above does the following:</span></span>

* <span data-ttu-id="f7473-113">속성 파일에서 가져온 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props* 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-113">Imports the properties file from *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.Props* at the beginning.</span></span>
* <span data-ttu-id="f7473-114">종료 시 *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets*에서 대상 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-114">Imports the targets file from *$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web\Sdk\Sdk.targets* at the end.</span></span>

<span data-ttu-id="f7473-115">`MSBuildSDKsPath`의 기본 위치(Visual Studio 2017 Enterprise 사용)는 *%programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-115">The default location for `MSBuildSDKsPath` (with Visual Studio 2017 Enterprise) is the *%programfiles(x86)%\Microsoft Visual Studio\2017\Enterprise\MSBuild\Sdks* folder.</span></span>

<span data-ttu-id="f7473-116">`Microsoft.NET.Sdk.Web`은 다음에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-116">`Microsoft.NET.Sdk.Web` depends on:</span></span>

* <span data-ttu-id="f7473-117">*Microsoft.NET.Sdk.Web.ProjectSystem*</span><span class="sxs-lookup"><span data-stu-id="f7473-117">*Microsoft.NET.Sdk.Web.ProjectSystem*</span></span>
* <span data-ttu-id="f7473-118">*Microsoft.NET.Sdk.Publish*</span><span class="sxs-lookup"><span data-stu-id="f7473-118">*Microsoft.NET.Sdk.Publish*</span></span>

<span data-ttu-id="f7473-119">그러면 다음과 같은 속성 및 가져올 대상:</span><span class="sxs-lookup"><span data-stu-id="f7473-119">Which causes the following properties and targets to be imported:</span></span>

* <span data-ttu-id="f7473-120">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props</span><span class="sxs-lookup"><span data-stu-id="f7473-120">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.Props</span></span>
* <span data-ttu-id="f7473-121">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets</span><span class="sxs-lookup"><span data-stu-id="f7473-121">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Web.ProjectSystem\Sdk\Sdk.targets</span></span>
* <span data-ttu-id="f7473-122">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props</span><span class="sxs-lookup"><span data-stu-id="f7473-122">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.Props</span></span>
* <span data-ttu-id="f7473-123">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets</span><span class="sxs-lookup"><span data-stu-id="f7473-123">$(MSBuildSDKsPath)\Microsoft.NET.Sdk.Publish\Sdk\Sdk.targets</span></span>

<span data-ttu-id="f7473-124">대상을 가져오기 오른쪽 사용 되는 게시 방법에 따라 대상 집합을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-124">Publish targets import the right set of targets based on the publish method used.</span></span>

<span data-ttu-id="f7473-125">MSBuild 또는 Visual Studio가 프로젝트를 로드하면 다음 높은 수준의 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-125">When MSBuild or Visual Studio loads a project, the following high level actions are performed:</span></span>

* <span data-ttu-id="f7473-126">프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="f7473-126">Build project</span></span>
* <span data-ttu-id="f7473-127">게시할 파일 계산</span><span class="sxs-lookup"><span data-stu-id="f7473-127">Compute files to publish</span></span>
* <span data-ttu-id="f7473-128">대상에 파일 게시</span><span class="sxs-lookup"><span data-stu-id="f7473-128">Publish files to destination</span></span>

### <a name="compute-project-items"></a><span data-ttu-id="f7473-129">프로젝트 항목 계산</span><span class="sxs-lookup"><span data-stu-id="f7473-129">Compute project items</span></span>

<span data-ttu-id="f7473-130">프로젝트가 로드되면 프로젝트 항목(파일)이 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-130">When the project is loaded, the project items (files) are computed.</span></span> <span data-ttu-id="f7473-131">`item type` 특성에 따라 파일 처리 방법이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-131">The `item type` attribute determines how the file is processed.</span></span> <span data-ttu-id="f7473-132">기본적으로 *.cs* 파일은 `Compile` 항목 목록에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-132">By default, *.cs* files are included in the `Compile` item list.</span></span> <span data-ttu-id="f7473-133">`Compile` 항목 목록의 파일이 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-133">Files in the `Compile` item list are compiled.</span></span>

<span data-ttu-id="f7473-134">`Content` 항목 목록에 빌드 출력 외에도 게시 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-134">The `Content` item list contains files that are published in addition to the build outputs.</span></span> <span data-ttu-id="f7473-135">기본적으로 패턴과 일치 하는 파일 `wwwroot/**` 에 포함 된 `Content` 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-135">By default, files matching the pattern `wwwroot/**` are included in the `Content` item.</span></span> <span data-ttu-id="f7473-136">[wwwroot /\* \* 와일드 카드 사용 패턴은](https://gruntjs.com/configuring-tasks#globbing-patterns) 의 모든 파일을 지정 하는 *wwwroot* 폴더 **및** 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-136">[wwwroot/\*\* is a globbing pattern](https://gruntjs.com/configuring-tasks#globbing-patterns) that specifies all files in the *wwwroot* folder **and** subfolders.</span></span> <span data-ttu-id="f7473-137">게시 목록에 파일을 명시적으로 추가하려면 [포함하는 파일](#including-files)에 표시된 대로 *.csproj* 파일에서 직접 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-137">To explicitly add a file to the publish list, add the file directly in the *.csproj* file as shown in [Including Files](#including-files).</span></span>

<span data-ttu-id="f7473-138">선택 하는 경우는 **게시** 단추 Visual Studio 또는 명령줄에서 게시 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="f7473-138">When selecting the **Publish** button in Visual Studio or when publishing from the command line:</span></span>

* <span data-ttu-id="f7473-139">속성/항목이 계산됩니다(빌드하는 데 필요한 파일).</span><span class="sxs-lookup"><span data-stu-id="f7473-139">The properties/items are computed (the files that are needed to build).</span></span>
* <span data-ttu-id="f7473-140">Visual Studio에만 해당: NuGet 패키지가 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-140">Visual Studio only: NuGet packages are restored.</span></span> <span data-ttu-id="f7473-141">(CLI에서 사용자가 명시적으로 복원해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f7473-141">(Restore needs to be explicit by the user on the CLI.)</span></span>
* <span data-ttu-id="f7473-142">프로젝트가 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-142">The project builds.</span></span>
* <span data-ttu-id="f7473-143">게시 항목이 계산됩니다(게시하는 데 필요한 파일).</span><span class="sxs-lookup"><span data-stu-id="f7473-143">The publish items are computed (the files that are needed to publish).</span></span>
* <span data-ttu-id="f7473-144">프로젝트가 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-144">The project is published.</span></span> <span data-ttu-id="f7473-145">계산된 파일이 게시 대상에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-145">(The computed files are copied to the publish destination.)</span></span>

<span data-ttu-id="f7473-146">ASP.NET Core 프로젝트가 참조 하는 경우 `Microsoft.NET.Sdk.Web` 프로젝트 파일에는 *app_offline.htm* 파일이 웹 응용 프로그램 디렉터리의 루트에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-146">When an ASP.NET Core project references `Microsoft.NET.Sdk.Web` in the project file, an *app_offline.htm* file is placed at the root of the web app directory.</span></span> <span data-ttu-id="f7473-147">파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-147">When the file is present, the ASP.NET Core Module gracefully shuts down the app and serves the *app_offline.htm* file during the deployment.</span></span> <span data-ttu-id="f7473-148">자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#appofflinehtm)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7473-148">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#appofflinehtm).</span></span>

## <a name="basic-command-line-publishing"></a><span data-ttu-id="f7473-149">기본 명령줄 게시</span><span class="sxs-lookup"><span data-stu-id="f7473-149">Basic command-line publishing</span></span>

<span data-ttu-id="f7473-150">명령줄 게시.NET Core 지원 되는 모든 플랫폼에서 작동 하며 Visual Studio 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-150">Command-line publishing works on all .NET Core supported platforms and doesn't require Visual Studio.</span></span> <span data-ttu-id="f7473-151">아래 샘플에서 `dotnet publish` 명령은 *.csproj* 파일이 포함된 프로젝트 디렉터리에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-151">In the samples below, the `dotnet publish` command is run from the project directory (which contains the *.csproj* file).</span></span> <span data-ttu-id="f7473-152">그렇지 않으면 프로젝트 폴더의 프로젝트 파일 경로에 명시적으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-152">If not in the project folder, explicitly pass in the project file path.</span></span> <span data-ttu-id="f7473-153">예:</span><span class="sxs-lookup"><span data-stu-id="f7473-153">For example:</span></span>

```console
dotnet publish c:/webs/web1
```

<span data-ttu-id="f7473-154">다음 명령을 실행하여 웹앱을 만들고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-154">Run the following commands to create and publish a web app:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="f7473-155">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="f7473-155">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```console
dotnet new mvc
dotnet publish
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="f7473-156">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="f7473-156">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```console
dotnet new mvc
dotnet restore
dotnet publish
```

---

<span data-ttu-id="f7473-157">`dotnet publish`는 다음과 비슷한 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-157">The `dotnet publish` produces output similar to the following:</span></span>

```console
C:\Webs\Web1>dotnet publish
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\Web1.dll
  Web1 -> C:\Webs\Web1\bin\Debug\netcoreapp2.0\publish\
```

<span data-ttu-id="f7473-158">기본 게시 폴더는 `bin\$(Configuration)\netcoreapp<version>\publish`입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-158">The default publish folder is `bin\$(Configuration)\netcoreapp<version>\publish`.</span></span> <span data-ttu-id="f7473-159">`$(Configuration)`의 기본값은 Debug입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-159">The default for `$(Configuration)` is Debug.</span></span> <span data-ttu-id="f7473-160">위의 샘플에서 `<TargetFramework>`는 `netcoreapp2.0`입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-160">In the sample above, the `<TargetFramework>` is `netcoreapp2.0`.</span></span>

<span data-ttu-id="f7473-161">`dotnet publish -h`는 게시에 대한 도움말 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-161">`dotnet publish -h` displays help information for publish.</span></span>

<span data-ttu-id="f7473-162">다음 명령은 `Release` 빌드 및 게시 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-162">The following command specifies a `Release` build and the publishing directory:</span></span>

```console
dotnet publish -c Release -o C:/MyWebs/test
```

<span data-ttu-id="f7473-163">`dotnet publish` 호출 하는 MSBuild를 호출 하는 명령에서 `Publish` 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-163">The `dotnet publish` command calls MSBuild which invokes the `Publish` target.</span></span> <span data-ttu-id="f7473-164">모든 매개 변수가 전달 `dotnet publish` MSBuild에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-164">Any parameters passed to `dotnet publish` are passed to MSBuild.</span></span> <span data-ttu-id="f7473-165">`-c` 매개 변수는 `Configuration` MSBuild 속성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-165">The `-c` parameter maps to the `Configuration` MSBuild property.</span></span> <span data-ttu-id="f7473-166">`-o` 매개 변수는 `OutputPath`에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-166">The `-o` parameter maps to `OutputPath`.</span></span>

<span data-ttu-id="f7473-167">MSBuild 속성 형식 중 하나를 사용 하 여 전달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-167">MSBuild properties can be passed using either of the following formats:</span></span>

* ` p:<NAME>=<VALUE>`
* `/p:<NAME>=<VALUE>`

<span data-ttu-id="f7473-168">다음 명령은 `Release` 빌드를 네트워크 공유에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-168">The following command publishes a `Release` build to a network share:</span></span>

`dotnet publish -c Release /p:PublishDir=//r8/release/AdminWeb`

<span data-ttu-id="f7473-169">네트워크 공유는 슬래시(*//r8/*)를 사용하여 지정하고 모든 .NET Core 지원 플랫폼에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-169">The network share is specified with forward slashes (*//r8/*) and works on all .NET Core supported platforms.</span></span>

<span data-ttu-id="f7473-170">배포할 게시된 앱이 실행되고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-170">Confirm that the published app for deployment isn't running.</span></span> <span data-ttu-id="f7473-171">앱이 실행 중이면 *publish* 폴더의 파일이 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-171">Files in the *publish* folder are locked when the app is running.</span></span> <span data-ttu-id="f7473-172">잠긴 파일을 복사할 수 없으므로 배포를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-172">Deployment can't occur because locked files can't be copied.</span></span>

## <a name="publish-profiles"></a><span data-ttu-id="f7473-173">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="f7473-173">Publish profiles</span></span>

<span data-ttu-id="f7473-174">이 섹션에서는 Visual Studio 2017 이상을 사용하여 게시 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-174">This section uses Visual Studio 2017 and higher to create publishing profiles.</span></span> <span data-ttu-id="f7473-175">를 만든 후 Visual Studio 또는 명령줄에서 게시를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-175">Once created, publishing from Visual Studio or the command line is available.</span></span>

<span data-ttu-id="f7473-176">게시 프로필을 사용하면 게시 프로세스를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-176">Publish profiles can simplify the publishing process.</span></span> <span data-ttu-id="f7473-177">게시 프로필을 여러 개 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-177">Multiple publish profiles can exist.</span></span> <span data-ttu-id="f7473-178">Visual Studio에서 게시 프로필을 만들려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-178">To create a publish profile in Visual Studio, right-click on the project in Solution Explorer and select **Publish**.</span></span> <span data-ttu-id="f7473-179">또는 선택 **게시 \<프로젝트 이름 >** 빌드 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-179">Alternatively, select **Publish \<project name>** from the build menu.</span></span> <span data-ttu-id="f7473-180">응용 프로그램 기능 페이지의 **게시** 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-180">The **Publish** tab of the application capacities page is displayed.</span></span> <span data-ttu-id="f7473-181">프로젝트에 게시 프로필이 없으면 다음 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-181">If the project doesn't contain a publish profile, the following page is displayed:</span></span>

![Azure, IIS, FTB, Azure와 폴더를 보여 주는 용량 페이지에 응용 프로그램의 게시 탭을 선택 합니다.](visual-studio-publish-profiles/_static/az.png)

<span data-ttu-id="f7473-184">**폴더**가 선택되면 **게시** 단추는 폴더 게시 프로필을 만들고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-184">When **Folder** is selected, the **Publish** button creates a folder publish profile and publishes.</span></span>

![Azure, IIS, FTB, 폴더를 보여 주는 응용 프로그램 기능 페이지의 **게시** 탭](visual-studio-publish-profiles/_static/pub1.png)

<span data-ttu-id="f7473-186">게시 프로필을 만든 후의 **게시** 변경 내용 탭을 선택한 **새 프로필 만들기** 새 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-186">Once a publish profile is created, the **Publish** tab changes, and select **Create new profile** to create a new profile.</span></span>

![마지막 단계에서 만들어진 FolderProfile 및 새 프로필 만들기 링크를 보여 주는 응용 프로그램 기능 페이지의 **게시** 탭](visual-studio-publish-profiles/_static/create_new.png)

<span data-ttu-id="f7473-188">게시 마법사는 다음 게시 대상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-188">The Publish wizard supports the following publish targets:</span></span>

* <span data-ttu-id="f7473-189">Microsoft Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f7473-189">Microsoft Azure App Service</span></span>
* <span data-ttu-id="f7473-190">IIS, FTP 등(웹 서버의 경우)</span><span class="sxs-lookup"><span data-stu-id="f7473-190">IIS, FTP, etc (for any web server)</span></span>
* <span data-ttu-id="f7473-191">폴더</span><span class="sxs-lookup"><span data-stu-id="f7473-191">Folder</span></span>
* <span data-ttu-id="f7473-192">프로필을 (프로필 가져오기 수 있음)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-192">Import profile (allows profile import).</span></span>
* <span data-ttu-id="f7473-193">Microsoft Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="f7473-193">Microsoft Azure Virtual Machines</span></span>

<span data-ttu-id="f7473-194">자세한 내용은 [내게 적합한 게시 옵션](https://docs.microsoft.com/visualstudio/ide/not-in-toc/web-publish-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7473-194">See [What publishing options are right for me?](https://docs.microsoft.com/visualstudio/ide/not-in-toc/web-publish-options) for more information.</span></span>

<span data-ttu-id="f7473-195">Visual Studio와 함께 게시 프로필을 만들 때 한 *속성/PublishProfiles/\<게시 이름입니다. >.pubxml* MSBuild 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-195">When creating a publish profile with Visual Studio, a *Properties/PublishProfiles/\<publish name>.pubxml* MSBuild file is created.</span></span> <span data-ttu-id="f7473-196">이 *.pubxml* 파일은 MSBuild 파일이고 게시 구성 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-196">This *.pubxml* file is a MSBuild file and contains publish configuration settings.</span></span> <span data-ttu-id="f7473-197">빌드 사용자 지정 및 프로세스를 게시 하려면이 파일을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-197">This file can be changed to customize the build and publish process.</span></span> <span data-ttu-id="f7473-198">게시 프로세스에서 이 파일을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-198">This file is read by the publishing process.</span></span> <span data-ttu-id="f7473-199">`<LastUsedBuildConfiguration>`전역 속성을 빌드에 가져온 모든 파일에 되지 않아야 하기 때문에 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-199">`<LastUsedBuildConfiguration>` is special because it's a global property and shouldn't be in any file that's imported in the build.</span></span> <span data-ttu-id="f7473-200">자세한 내용은 [MSBuild: 구성 속성을 설정하는 방법](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7473-200">See [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) for more info.</span></span>
<span data-ttu-id="f7473-201">*.pubxml* 있기 때문에 소스 제어에 파일을 체크 인할 수 해서는 안는 *.user* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-201">The *.pubxml* file shouldn't be checked into source control because it depends on the *.user* file.</span></span> <span data-ttu-id="f7473-202">*.user* 파일은 중요 정보를 포함할 수 있고 하나의 사용자 및 컴퓨터에 대해서만 유효하므로 소스 제어에 체크 인되면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-202">The *.user* file should never be checked into source control because it can contain sensitive information and it's only valid for one user and machine.</span></span>

<span data-ttu-id="f7473-203">중요 정보(예: 게시 암호)는 사용자/컴퓨터 수준별로 암호화되고 *Properties/PublishProfiles/\<publish name>.pubxml.user* 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-203">Sensitive information (like the publish password) is encrypted on a per user/machine level and stored in the *Properties/PublishProfiles/\<publish name>.pubxml.user* file.</span></span> <span data-ttu-id="f7473-204">이 파일에는 중요 정보가 포함될 수 있으므로 소스 제어에 체크 인되면 **안 됩니다**.</span><span class="sxs-lookup"><span data-stu-id="f7473-204">Because this file can contain sensitive information, it should **not** be checked into source control.</span></span>

<span data-ttu-id="f7473-205">ASP.NET core 웹 앱을 게시 하는 방법에 대 한 개요를 참조 하십시오. [호스트 하 고 배포](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-205">For an overview of how to publish a web app on ASP.NET Core see [Host and deploy](index.md).</span></span> <span data-ttu-id="f7473-206">[호스트 및 배포](index.md) https://github.com/aspnet/websdk에서 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-206">[Host and deploy](index.md) is an open source project at https://github.com/aspnet/websdk.</span></span>

<span data-ttu-id="f7473-207">`dotnet publish`폴더를 MSDeploy צ ְ ײ 및 [KUDU](https://github.com/projectkudu/kudu/wiki) 게시 프로필:</span><span class="sxs-lookup"><span data-stu-id="f7473-207">`dotnet publish` can use folder, MSDeploy, and [KUDU](https://github.com/projectkudu/kudu/wiki) publish profiles:</span></span>
 
<span data-ttu-id="f7473-208">폴더 (플랫폼 간에 작동):`dotnet publish WebApplication.csproj /p:PublishProfile=<FolderProfileName>`</span><span class="sxs-lookup"><span data-stu-id="f7473-208">Folder (works cross-platform): `dotnet publish WebApplication.csproj /p:PublishProfile=<FolderProfileName>`</span></span>

<span data-ttu-id="f7473-209">MSDeploy (현재는 기능만 MSDeploy 없는 플랫폼 간 이후 windows의):`dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>`</span><span class="sxs-lookup"><span data-stu-id="f7473-209">MSDeploy (currently this only works in windows since MSDeploy isn't cross-platform): `dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>`</span></span>

<span data-ttu-id="f7473-210">MSDeploy 패키지 (현재는 기능만 MSDeploy 없는 플랫폼 간 이후 windows의):`dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>`</span><span class="sxs-lookup"><span data-stu-id="f7473-210">MSDeploy package(currently this only works in windows since MSDeploy isn't cross-platform): `dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>`</span></span>

<span data-ttu-id="f7473-211">위의 샘플에서 **하지** 전달 `deployonbuild` 를 `dotnet publish`합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-211">In the preceeding samples, **don't** pass `deployonbuild` to `dotnet publish`.</span></span>

<span data-ttu-id="f7473-212">자세한 내용은 참조 [Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-212">For more information, see [Microsoft.NET.Sdk.Publish](https://github.com/aspnet/websdk#microsoftnetsdkpublish).</span></span>

<span data-ttu-id="f7473-213">`dotnet publish`는 모든 플랫폼에서 Azure에 게시하기 위해 KUDU API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-213">`dotnet publish` supports KUDU apis to publish to Azure from any platform.</span></span> <span data-ttu-id="f7473-214">Visual Studio 게시 교차 구획 Azure에 게시에 대 한 KUDU Api 하지만 websdk에서 지원 되는 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-214">Visual Studio publish does support the KUDU APIs but it's supported by websdk for cross plat publish to Azure.</span></span>

<span data-ttu-id="f7473-215">다음 콘텐츠와 함께 *Properties/PublishProfiles* 폴더에 게시 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-215">Add a publish profile to *Properties/PublishProfiles* folder with the following content:</span></span>

```xml
<Project>
  <PropertyGroup>
    <PublishProtocol>Kudu</PublishProtocol>
    <PublishSiteName>nodewebapp</PublishSiteName>
    <UserName>username</UserName>
    <Password>password</Password>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="f7473-216">다음 명령을 실행 게시 콘텐츠를 이동 하 고 KUDU Api를 사용 하 여 Azure에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-216">Running the following command zips up the publish contents and publish it to Azure using the KUDU APIs:</span></span>

`dotnet publish /p:PublishProfile=Azure /p:Configuration=Release`

<span data-ttu-id="f7473-217">게시 프로필을 사용할 경우 다음 MSBuild 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-217">Set the following MSBuild properties when using a publish profile:</span></span>

* `DeployOnBuild=true`
* `PublishProfile=<Publish profile name>`

<span data-ttu-id="f7473-218">명명 된 프로필을 게시할 때 *FolderProfile*, 다음 명령 중 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-218">When publishing with a profile named *FolderProfile*, either of the commands below can be executed:</span></span>

* `dotnet build /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`
* `msbuild      /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

<span data-ttu-id="f7473-219">호출할 때 `dotnet build`, 호출 `msbuild` 를 빌드를 실행 하 고 프로세스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-219">When invoking `dotnet build`, it calls `msbuild` to run the build and publish process.</span></span> <span data-ttu-id="f7473-220">호출 `dotnet build` 또는 `msbuild` 폴더 프로 파일에 전달할 때 기본적으로 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-220">Calling `dotnet build` or `msbuild` is essentially equivalent when passing in a folder profile.</span></span> <span data-ttu-id="f7473-221">MSBuild를 Windows에서 직접 호출할 때.NET Framework 버전의 MSBuild 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-221">When calling MSBuild directly on Windows, the .NET Framework version of MSBuild is used.</span></span> <span data-ttu-id="f7473-222">MSDeploy는 현재 게시를 위해 Windows 컴퓨터로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-222">MSDeploy is currently limited to Windows machines for publishing.</span></span> <span data-ttu-id="f7473-223">폴더가 아닌 프로필에서 `dotnet build`를 호출하면 MSBuild가 호출되고 MSBuild는 폴더가 아닌 프로필에서 MSDeploy를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-223">Calling `dotnet build` on a non-folder profile invokes MSBuild, and MSBuild uses MSDeploy on non-folder profiles.</span></span> <span data-ttu-id="f7473-224">폴더가 아닌 프로필에서 `dotnet build`를 호출하면 MSBuild가 호출되고(MSDeploy 사용) Windows 플랫폼에서 실행될 경우에도 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-224">Calling `dotnet build` on a non-folder profile invokes MSBuild (using MSDeploy) and results in a failure (even when running on a Windows platform).</span></span> <span data-ttu-id="f7473-225">폴더가 아닌 프로필을 사용하여 게시하려면 MSBuild를 직접 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-225">To publish with a non-folder profile, call MSBuild directly.</span></span>

<span data-ttu-id="f7473-226">다음 폴더 게시 프로필은 Visual Studio를 사용하여 만들어졌고 네트워크 공유에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-226">The following folder publish profile was created with Visual Studio and publishes to a network share:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework>netcoreapp1.1</PublishFramework>
    <ProjectGuid>c30c453c-312e-40c4-aec9-394a145dee0b</ProjectGuid>
    <publishUrl>\\r8\Release\AdminWeb</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="f7473-227">`<LastUsedBuildConfiguration>`은 `Release`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-227">Note `<LastUsedBuildConfiguration>` is set to `Release`.</span></span> <span data-ttu-id="f7473-228">Visual Studio에서 게시할 경우 `<LastUsedBuildConfiguration>` 구성 속성 값은 게시 프로세스가 시작될 때의 값을 사용하여 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-228">When publishing from Visual Studio, the `<LastUsedBuildConfiguration>` configuration property value is set using the value when the publish process is started.</span></span> <span data-ttu-id="f7473-229">`<LastUsedBuildConfiguration>` 구성 속성은 특수 하며 가져온된 MSBuild 파일에서 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-229">The `<LastUsedBuildConfiguration>` configuration property is special and shouldn't be overridden in an imported MSBuild file.</span></span> <span data-ttu-id="f7473-230">명령줄에서이 속성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-230">This property can be overridden from the command line.</span></span> <span data-ttu-id="f7473-231">예:</span><span class="sxs-lookup"><span data-stu-id="f7473-231">For example:</span></span>

`dotnet build -c Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

<span data-ttu-id="f7473-232">MSBuild 사용:</span><span class="sxs-lookup"><span data-stu-id="f7473-232">Using MSBuild:</span></span>

`msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile`

## <a name="publish-to-an-msdeploy-endpoint-from-the-command-line"></a><span data-ttu-id="f7473-233">명령줄에서 MSDeploy 끝점에 게시</span><span class="sxs-lookup"><span data-stu-id="f7473-233">Publish to an MSDeploy endpoint from the command line</span></span>

<span data-ttu-id="f7473-234">에서 설명한 대로 사용 하 여 게시를 수행할 수 있습니다 `dotnet publish` 또는 `msbuild` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-234">As previously mentioned, publishing can be accomplished using `dotnet publish` or the `msbuild` command.</span></span> <span data-ttu-id="f7473-235">`dotnet publish`는 .NET Core의 컨텍스트에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-235">`dotnet publish` runs in the context of .NET Core.</span></span> <span data-ttu-id="f7473-236">`msbuild` 명령은.NET framework가 필요 이므로 Windows 환경으로 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-236">The `msbuild` command requires .NET framework, and is therefore limited to Windows environments.</span></span>

<span data-ttu-id="f7473-237">MSDeploy를 사용하여 게시하는 가장 좋은 방법은 먼저 Visual Studio 2017에서 게시 프로필을 만들고 명령줄에서 프로필을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-237">The easiest way to publish with MSDeploy is to first create a publish profile in Visual Studio 2017 and use the profile from the command line.</span></span>

<span data-ttu-id="f7473-238">다음 샘플에서는 ASP.NET Core 웹 앱을 만듭니다 (사용 하 여 `dotnet new mvc`), Azure 게시 프로필이 Visual Studio와 함께 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-238">In the following sample, an ASP.NET Core web app is created (using `dotnet new mvc`), and an Azure publish profile is added with Visual Studio.</span></span>

<span data-ttu-id="f7473-239">실행 `msbuild` 에서 **VS 2017 용 개발자 명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-239">Run `msbuild` from a **Developer Command Prompt for VS 2017**.</span></span> <span data-ttu-id="f7473-240">개발자 명령 프롬프트에 올바른 *msbuild.exe* 일부 MSBuild 변수 집합과 그 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-240">The Developer Command Prompt has the correct *msbuild.exe* in its path with some MSBuild variables set.</span></span>

<span data-ttu-id="f7473-241">MSBuild는 다음 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-241">MSBuild uses the following syntax:</span></span>

`msbuild <path-to-project-file> /p:DeployOnBuild=true /p:PublishProfile=<Publish Profile> /p:Username=<USERNAME> /p:Password=<PASSWORD>`

<span data-ttu-id="f7473-242">가져오기는 `Password` 에서 * \<게시 이름 >. PublishSettings* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-242">Get the `Password` from the *\<Publish name>.PublishSettings* file.</span></span> <span data-ttu-id="f7473-243">다운로드는 *합니다. PublishSettings* 파일 중 하나에서:</span><span class="sxs-lookup"><span data-stu-id="f7473-243">Download the *.PublishSettings* file from either:</span></span>

* <span data-ttu-id="f7473-244">솔루션 탐색기: 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 선택 **게시 프로필 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-244">Solution Explorer: Right-click on the Web App and select **Download Publish Profile**.</span></span>
* <span data-ttu-id="f7473-245">Azure 관리 포털: 선택 **Get 게시 프로필** 웹 앱 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-245">The Azure Management Portal: Select **Get publish profile** from the Web App blade.</span></span>

<span data-ttu-id="f7473-246">`Username`은 게시 프로필에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-246">`Username` can be found in the publish profile.</span></span>

<span data-ttu-id="f7473-247">다음 샘플에서는 “Web11112 - Web Deploy” 게시 프로필을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-247">The following sample uses the "Web11112 - Web Deploy" publish profile:</span></span>

```console
msbuild "C:\Webs\Web1\Web1.csproj" /p:DeployOnBuild=true
 /p:PublishProfile="Web11112 - Web Deploy"  /p:Username="$Web11112"
 /p:Password="<password removed>"
```

## <a name="excluding-files"></a><span data-ttu-id="f7473-248">파일 제외</span><span class="sxs-lookup"><span data-stu-id="f7473-248">Excluding files</span></span>

<span data-ttu-id="f7473-249">ASP.NET Core 웹앱을 게시할 경우 *wwwroot* 폴더의 빌드 아티팩트 및 콘텐츠가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-249">When publishing ASP.NET Core web apps, the build artifacts and contents of the *wwwroot* folder are included.</span></span> <span data-ttu-id="f7473-250">`msbuild`는 [와일드카드 사용 패턴](https://gruntjs.com/configuring-tasks#globbing-patterns)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-250">`msbuild` supports [globbing patterns](https://gruntjs.com/configuring-tasks#globbing-patterns).</span></span> <span data-ttu-id="f7473-251">예를 들어, 다음 `<Content>` 모든 텍스트를 제외 하는 요소 태그로 (*.txt*)에서 파일을 *wwwroot/content* 폴더와 모든 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-251">For example, the following `<Content>` element markup excludes all text (*.txt*) files from the *wwwroot/content* folder and all its subfolders.</span></span>

```xml
<ItemGroup>
  <Content Update="wwwroot/content/**/*.txt" CopyToPublishDirectory="Never" />
</ItemGroup>
```

<span data-ttu-id="f7473-252">위의 태그는 게시 프로필 또는 *.csproj* 파일에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-252">The markup above can be added to a publish profile or the *.csproj* file.</span></span> <span data-ttu-id="f7473-253">*.csproj* 파일에 추가된 규칙은 프로젝트의 모든 게시 프로필에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-253">When added to the *.csproj* file, the rule is added to all publish profiles in the project.</span></span>

<span data-ttu-id="f7473-254">다음 `<MsDeploySkipRules>` 요소 태그는 *wwwroot/content* 폴더에서 모든 파일을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-254">The following `<MsDeploySkipRules>` element markup exludes all files from the *wwwroot/content* folder:</span></span>

```xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFolder">
    <ObjectName>dirPath</ObjectName>
    <AbsolutePath>wwwroot\\content</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

<span data-ttu-id="f7473-255">`<MsDeploySkipRules>`삭제 되지 않습니다는 *건너뛸* 배포 사이트에서 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-255">`<MsDeploySkipRules>` won't delete the *skip* targets from the deployment site.</span></span> <span data-ttu-id="f7473-256">`<Content>`대상된 파일 및 폴더는 배포 사이트에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-256">`<Content>` targeted files and folders are deleted from the deployment site.</span></span> <span data-ttu-id="f7473-257">예를 들어 배포 된 웹 응용 프로그램에는 다음 파일이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-257">For example, suppose a deployed web app had the following files:</span></span>

* <span data-ttu-id="f7473-258">*Views/Home/About1.cshtml*</span><span class="sxs-lookup"><span data-stu-id="f7473-258">*Views/Home/About1.cshtml*</span></span>
* <span data-ttu-id="f7473-259">*Views/Home/About2.cshtml*</span><span class="sxs-lookup"><span data-stu-id="f7473-259">*Views/Home/About2.cshtml*</span></span>
* <span data-ttu-id="f7473-260">*Views/Home/About3.cshtml*</span><span class="sxs-lookup"><span data-stu-id="f7473-260">*Views/Home/About3.cshtml*</span></span>

<span data-ttu-id="f7473-261">하는 경우 다음 `<MsDeploySkipRules>` 태그를 추가, 배포 사이트에서 해당 파일을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-261">If the following `<MsDeploySkipRules>` markup is added, those files wouldn't be deleted on the deployment site.</span></span>

``` xml
<ItemGroup>
  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About1.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About2.cshtml</AbsolutePath>
  </MsDeploySkipRules>

  <MsDeploySkipRules Include="CustomSkipFile">
    <ObjectName>filePath</ObjectName>
    <AbsolutePath>Views\\Home\\About3.cshtml</AbsolutePath>
  </MsDeploySkipRules>
</ItemGroup>
```

<span data-ttu-id="f7473-262">`<MsDeploySkipRules>` 태그 위에 표시 된 것을 금지는 *건너뛴* depoyed 없도록 파일 하지만 배포 되는 되 면 해당 파일을 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-262">The `<MsDeploySkipRules>` markup shown above prevents the *skipped* files from being depoyed but won't delete those files once they're deployed.</span></span>

<span data-ttu-id="f7473-263">다음 `<Content>` 태그 배포 사이트에서 대상으로 지정 된 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-263">The following `<Content>` markup deletes the targeted files at the deployment site:</span></span>

``` xml
<ItemGroup>
  <Content Update="Views/Home/About?.cshtml" CopyToPublishDirectory="Never" />
</ItemGroup>
```

<span data-ttu-id="f7473-264">명령줄 배포를 사용 하는 `<Content>` 태그 위에 다음과 유사한 출력 결과:</span><span class="sxs-lookup"><span data-stu-id="f7473-264">Using command-line deployment with the `<Content>` markup above results in output similar to the following:</span></span>

``` console
MSDeployPublish:
  Starting Web deployment task from source: manifest(C:\Webs\Web1\obj\Release\netcoreapp1.1\PubTmp\Web1.SourceManifest.
  xml) to Destination: auto().
  Deleting file (Web11112\Views\Home\About1.cshtml).
  Deleting file (Web11112\Views\Home\About2.cshtml).
  Deleting file (Web11112\Views\Home\About3.cshtml).
  Updating file (Web11112\web.config).
  Updating file (Web11112\Web1.deps.json).
  Updating file (Web11112\Web1.dll).
  Updating file (Web11112\Web1.pdb).
  Updating file (Web11112\Web1.runtimeconfig.json).
  Successfully executed Web deployment task.
  Publish Succeeded.
Done Building Project "C:\Webs\Web1\Web1.csproj" (default targets).
```

## <a name="including-files"></a><span data-ttu-id="f7473-265">포함하는 파일</span><span class="sxs-lookup"><span data-stu-id="f7473-265">Including files</span></span>

<span data-ttu-id="f7473-266">다음 태그를 포함 한 *이미지* 폴더를 프로젝트 디렉터리 외부의 *wwwroot/이미지* 게시 사이트의 폴더:</span><span class="sxs-lookup"><span data-stu-id="f7473-266">The following markup includes an *images* folder outside the project directory to the *wwwroot/images* folder of the publish site:</span></span>

``` xml
<ItemGroup>
  <_CustomFiles Include="$(MSBuildProjectDirectory)/../images/**/*" />
  <DotnetPublishFiles Include="@(_CustomFiles)">
    <DestinationRelativePath>wwwroot/images/%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
  </DotnetPublishFiles>
</ItemGroup>
```

<span data-ttu-id="f7473-267">태그는 *.csproj* 파일 또는 게시 프로필에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-267">The markup can be added to the *.csproj* file or the publish profile.</span></span> <span data-ttu-id="f7473-268">에 추가 되 면는 *.csproj* 파일을 프로젝트에 각 게시 프로필에 포함 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-268">If it's added to the *.csproj* file, it's included in each publish profile in the project.</span></span>

<span data-ttu-id="f7473-269">다음 강조 표시된 태그는 방법을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-269">The following highlighted markup shows how to:</span></span>

* <span data-ttu-id="f7473-270">프로젝트 외부에서 *wwwroot* 폴더로 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-270">Copy a file from outside the project into the *wwwroot* folder.</span></span>
* <span data-ttu-id="f7473-271">*wwwroot\Content* 폴더를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-271">Exclude the *wwwroot\Content* folder.</span></span>
* <span data-ttu-id="f7473-272">*Views\Home\About2.cshtml*을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-272">Exclude *Views\Home\About2.cshtml*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project.
You can customize the behavior of this process by editing this 
MSBuild file.
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish />
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <ExcludeApp_Data>False</ExcludeApp_Data>
    <PublishFramework />
    <ProjectGuid>afa9f185-7ce0-4935-9da1-ab676229d68a</ProjectGuid>
    <publishUrl>bin\Release\PublishOutput</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>
  <ItemGroup>
    <ResolvedFileToPublish Include="..\ReadMe2.MD">
      <RelativePath>wwwroot\ReadMe2.MD</RelativePath>
    </ResolvedFileToPublish>

    <Content Update="wwwroot\Content\**\*" CopyToPublishDirectory="Never" />
    <Content Update="Views\Home\About2.cshtml" CopyToPublishDirectory="Never" />

  </ItemGroup>
</Project>
```

<span data-ttu-id="f7473-273">더 많은 배포 샘플을 보려면 [WebSDK Readme](https://github.com/aspnet/websdk)(WebSDK 추가 정보)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7473-273">See the [WebSDK Readme](https://github.com/aspnet/websdk) for more deployment samples.</span></span>

### <a name="run-a-target-before-or-after-publishing"></a><span data-ttu-id="f7473-274">게시 이전 또는 이후 대상 실행</span><span class="sxs-lookup"><span data-stu-id="f7473-274">Run a target before or after publishing</span></span>

<span data-ttu-id="f7473-275">기본 제공 `BeforePublish` 및 `AfterPublish` 대상 앞 이나 뒤 게시 대상이 대상이 실행 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-275">The built-in `BeforePublish` and `AfterPublish` targets can be used to execute a target before or after the publish target.</span></span> <span data-ttu-id="f7473-276">다음 태그를 게시 프로필에 추가하여 게시 이전 및 이후에 콘솔 출력에 메시지를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-276">The following markup can be added to the publish profile to log messages to the console output before and after publishing:</span></span>

``` xml
<Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Inside BeforePublish" Importance="high" />
  </Target>
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Inside AfterPublish" Importance="high" />
</Target>
```

## <a name="the-kudu-service"></a><span data-ttu-id="f7473-277">Kudu 서비스</span><span class="sxs-lookup"><span data-stu-id="f7473-277">The Kudu service</span></span>

<span data-ttu-id="f7473-278">파일을 보려면는 Azure 앱 서비스 웹 응용 프로그램 배포를 사용 하 여는 [Kudu 서비스](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-278">To view the files in the an Azure Apps Service web app deployment, use the [Kudu service](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service).</span></span> <span data-ttu-id="f7473-279">추가 `scm` 토큰을 웹 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-279">Append the `scm` token to the name of the web app.</span></span> <span data-ttu-id="f7473-280">예:</span><span class="sxs-lookup"><span data-stu-id="f7473-280">For example:</span></span>

| <span data-ttu-id="f7473-281">URL</span><span class="sxs-lookup"><span data-stu-id="f7473-281">URL</span></span>                                    | <span data-ttu-id="f7473-282">결과</span><span class="sxs-lookup"><span data-stu-id="f7473-282">Result</span></span>      |
| -------------------------------------- | ----------- |
| `http://mysite.azurewebsites.net/`     | <span data-ttu-id="f7473-283">웹앱</span><span class="sxs-lookup"><span data-stu-id="f7473-283">Web App</span></span>     |
| `http://mysite.scm.azurewebsites.net/` | <span data-ttu-id="f7473-284">Kudu 서비스</span><span class="sxs-lookup"><span data-stu-id="f7473-284">Kudu sevice</span></span> |

<span data-ttu-id="f7473-285">[디버그 콘솔](https://github.com/projectkudu/kudu/wiki/Kudu-console) 메뉴 항목을 선택하여 파일을 표시/편집/삭제/추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-285">Select the [Debug Console](https://github.com/projectkudu/kudu/wiki/Kudu-console) menu item to view/edit/delete/add files.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7473-286">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f7473-286">Additional resources</span></span>

* <span data-ttu-id="f7473-287">[웹 배포](https://www.iis.net/downloads/microsoft/web-deploy) (MSDeploy)는 웹 응용 프로그램 및 웹 사이트는 IIS 서버에 배포를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7473-287">[Web Deploy](https://www.iis.net/downloads/microsoft/web-deploy) (MSDeploy) simplifies deployment of web apps and websites to IIS servers.</span></span>
* <span data-ttu-id="f7473-288">[https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues): 배포에 대한 파일 문제 및 요청 기능.</span><span class="sxs-lookup"><span data-stu-id="f7473-288">[https://github.com/aspnet/websdk](https://github.com/aspnet/websdk/issues): File issues and request features for deployment.</span></span>
