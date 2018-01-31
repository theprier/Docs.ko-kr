---
title: "Mac용 Visual Studio를 사용하여 Razor 페이지 앱에 모델 추가"
author: rick-anderson
description: "Mac용 Visual Studio를 사용하여 ASP.NET Core에서 Razor 페이지 앱에 모델 추가"
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-mac/model
ms.openlocfilehash: f4fb4fc3402c866fa9f956341c06be34ca9f4763
ms.sourcegitcommit: 09b342b45e7372ba9ebf17f35eee331e5a08fb26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2018
---
# <a name="adding-a-model-to-a-razor-pages-app-in-aspnet-core-with-visual-studio-for-mac"></a><span data-ttu-id="ee2a2-103">Mac용 Visual Studio를 사용하여 ASP.NET Core에서 Razor 페이지 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="ee2a2-103">Adding a model to a Razor Pages app in ASP.NET Core with Visual Studio for Mac</span></span>

[!INCLUDE[model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="ee2a2-104">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="ee2a2-104">Add a data model</span></span>

* <span data-ttu-id="ee2a2-105">솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-105">In Solution Explorer, right-click the **RazorPagesMovie** project, and then select **Add** > **New Folder**.</span></span> <span data-ttu-id="ee2a2-106">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-106">Name the folder *Models*.</span></span>
* <span data-ttu-id="ee2a2-107">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-107">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span>
* <span data-ttu-id="ee2a2-108">**새 파일** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="ee2a2-108">In the **New File** dialog:</span></span>

  * <span data-ttu-id="ee2a2-109">왼쪽 창에서 **일반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-109">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="ee2a2-110">가운데 창에서 **빈 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-110">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="ee2a2-111">클래스 이름을 **Movie**로 지정하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-111">Name the class **Movie** and select **New**.</span></span>

[!INCLUDE[model 2](../../includes/RP/model2.md)]
[!INCLUDE[model 2a](../../includes/RP/model2a.md)]

[!code-csharp[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="ee2a2-112">줄 `services.AddDbContext<MovieContext>(options =>`에서 빨간색 물결선을 마우스 오른쪽 단추로 클릭합니다(예: `MovieContext`).</span><span class="sxs-lookup"><span data-stu-id="ee2a2-112">Right click on a red squiggly line, for example `MovieContext` in the line `services.AddDbContext<MovieContext>(options =>`.</span></span> <span data-ttu-id="ee2a2-113">**빠른 수정 > using RazorPagesMovie.Models;**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-113">Select **Quick Fix > using RazorPagesMovie.Models;**.</span></span> <span data-ttu-id="ee2a2-114">Visual Studio가 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-114">Visual studio adds the using statement.</span></span>

<span data-ttu-id="ee2a2-115">프로젝트를 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-115">Build the project to verify you don't have any errors.</span></span>

![페이지 만들기](model/red.png)

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="ee2a2-117">마이그레이션을 위한 Entity Framework Core NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="ee2a2-117">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="ee2a2-118">CLI(명령줄 인터페이스)용 EF 도구는 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-118">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="ee2a2-119">사용할 버전 번호를 얻으려면 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-119">Click on the [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) link to get the version number to use.</span></span> <span data-ttu-id="ee2a2-120">이 패키지를 설치하려면 *.csproj* 파일의 `DotNetCliToolReference` 컬렉션에 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-120">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="ee2a2-121">**참고:** *.csproj* 파일을 편집하여 이 패키지를 설치해야 합니다. `install-package` 명령이나 패키지 관리자 GUI를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-121">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="ee2a2-122">*.csproj* 파일을 편집하려면:</span><span class="sxs-lookup"><span data-stu-id="ee2a2-122">To edit a *.csproj* file:</span></span>

* <span data-ttu-id="ee2a2-123">**파일** > **열기**를 선택한 다음, *.csproj* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-123">Select **File** > **Open**, and then select the *.csproj* file.</span></span>
* <span data-ttu-id="ee2a2-124">**옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-124">Select **Options**.</span></span>
* <span data-ttu-id="ee2a2-125">**연결 프로그램**을 **소스 코드 편집기**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-125">Change **Open with** to **Source Code Editor**.</span></span>

![csproj 파일 편집](model/csproj.png)

<span data-ttu-id="ee2a2-127">`Microsoft.EntityFrameworkCore.Tools.DotNet` 도구 참조를 두 번째 **\<ItemGroup>**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-127">Add the `Microsoft.EntityFrameworkCore.Tools.DotNet` tool reference to the second **\<ItemGroup>**.:</span></span>

[!code-xml[Main](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj?highlight=10)]

<span data-ttu-id="ee2a2-128">다음 코드에 표시된 버전 번호는 작성 당시 정확했습니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-128">The version numbers shown in the following code were correct at the time of writing.</span></span>

[!INCLUDE[model3](../../includes/RP/model3.md)]
[!INCLUDE[model 4x](../../includes/RP/model4x.md)]

[!INCLUDE[model 4 exit](../../includes/RP/model4exit.md)]

[!INCLUDE[model 4](../../includes/RP/model4.md)]

### <a name="add-the-pagesmovies-files-to-the-project"></a><span data-ttu-id="ee2a2-129">프로젝트에 Pages/Movies 파일 추가</span><span class="sxs-lookup"><span data-stu-id="ee2a2-129">Add the Pages/Movies files to the project</span></span>

* <span data-ttu-id="ee2a2-130">Visual Studio에서 *Pages* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 > 기존 폴더 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-130">In Visual Studio, Right-click the *Pages* folder and select **Add > Add existing Folder**.</span></span>
* <span data-ttu-id="ee2a2-131">*Movies* 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-131">Select the *Movies* folder.</span></span>
* <span data-ttu-id="ee2a2-132">*프로젝트에 포함할 파일 선택* 대화 상자에서 **모두 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-132">In the *Chosse files to include in the project* dialog, select **Include All**.</span></span>

<span data-ttu-id="ee2a2-133">다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ee2a2-133">The next tutorial explains the files created by scaffolding.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="ee2a2-134">[이전: 시작](xref:tutorials/razor-pages-mac/razor-pages-start)
[다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="ee2a2-134">[Previous: Getting Started](xref:tutorials/razor-pages-mac/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>
