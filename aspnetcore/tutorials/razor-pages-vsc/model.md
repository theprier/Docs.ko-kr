---
title: Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 앱에 모델 추가
author: rick-anderson
description: Visual Studio Code를 사용하여 ASP.NET Core의 Razor 페이지 앱에 모델을 추가하는 방법을 배웁니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages-vsc/model
ms.openlocfilehash: 20282b491162e9f35e40702655532a78edceb89a
ms.sourcegitcommit: 2ab550f8c46e1a8a5d45e58be44d151c676af256
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2018
---
# <a name="add-a-model-to-an-aspnet-core-razor-pages-app-with-visual-studio-code"></a><span data-ttu-id="9fd14-103">Visual Studio Code를 사용하여 ASP.NET Core Razor 페이지 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="9fd14-103">Add a model to an ASP.NET Core Razor Pages app with Visual Studio Code</span></span>

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="9fd14-104">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="9fd14-104">Add a data model</span></span>

* <span data-ttu-id="9fd14-105">*Models* 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-105">Add a folder named *Models*.</span></span>
* <span data-ttu-id="9fd14-106">*Models* 폴더에 *Movie.cs* 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-106">Add a class to the *Models* folder named *Movie.cs*.</span></span>
* <span data-ttu-id="9fd14-107">*Models/Movie.cs* 파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-107">Add the following code to the *Models/Movie.cs* file:</span></span>

[!INCLUDE [model 2](../../includes/RP/model2.md)]

[!INCLUDE [model 2a](../../includes/RP/model2a.md)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="9fd14-108">프로젝트를 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-108">Build the project to verify you don't have any errors.</span></span>

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="9fd14-109">마이그레이션을 위한 Entity Framework Core NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="9fd14-109">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="9fd14-110">CLI(명령줄 인터페이스)용 EF 도구는 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-110">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="9fd14-111">이 패키지를 설치하려면 *.csproj* 파일의 `DotNetCliToolReference` 컬렉션에 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-111">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="9fd14-112">**참고:** *.csproj* 파일을 편집하여 이 패키지를 설치해야 합니다. `install-package` 명령이나 패키지 관리자 GUI를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-112">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="9fd14-113">*RazorPagesMovie.csproj* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-113">Edit the *RazorPagesMovie.csproj* file:</span></span>

* <span data-ttu-id="9fd14-114">**파일** > **파일 열기**를 선택한 다음, *RazorPagesMovie.csproj* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-114">Select **File** > **Open File**, and then select the *RazorPagesMovie.csproj* file.</span></span>
* <span data-ttu-id="9fd14-115">`Microsoft.EntityFrameworkCore.Tools.DotNet`에 대한 도구 참조를 두 번째 **\<ItemGroup>** 에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-115">Add tool reference for `Microsoft.EntityFrameworkCore.Tools.DotNet` to the second **\<ItemGroup>**:</span></span>

[!code-xml[](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj)]

[!INCLUDE [model 3](../../includes/RP/model3.md)]

<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="9fd14-116">Movie 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="9fd14-116">Scaffold the Movie model</span></span>

* <span data-ttu-id="9fd14-117">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-117">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="9fd14-118">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-118">Run the following command:</span></span>

<span data-ttu-id="9fd14-119">**참고: Windows에서는 다음 명령을 실행합니다. MacOS 및 Linux의 경우 다음 명령 참조**</span><span class="sxs-lookup"><span data-stu-id="9fd14-119">**Note: Run the following command on Windows. For MacOS and Linux, see the next command**</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* <span data-ttu-id="9fd14-120">MacOS 및 Linux에서는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-120">On MacOS and Linux, run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

<span data-ttu-id="9fd14-121">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="9fd14-121">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="9fd14-122">Visual Studio를 종료하고 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-122">Exit Visual Studio and run the command again.</span></span>

[!INCLUDE [model 4](../../includes/RP/model4.md)]

<span data-ttu-id="9fd14-123">다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9fd14-123">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9fd14-124">[이전: 시작](xref:tutorials/razor-pages-vsc/razor-pages-start)
> [다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages-vsc/page)</span><span class="sxs-lookup"><span data-stu-id="9fd14-124">[Previous: Get Started](xref:tutorials/razor-pages-vsc/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages-vsc/page)</span></span>
