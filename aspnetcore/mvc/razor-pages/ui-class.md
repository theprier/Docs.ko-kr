---
title: ASP.NET Core를 사용하여 클래스 라이브러리에서 재사용 가능한 Razor UI
author: Rick-Anderson
description: 클래스 라이브러리에서 재사용 가능한 Razor UI를 만드는 방법을 설명합니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 4/31/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: advanced
uid: mvc/razor-pages/ui-class
ms.openlocfilehash: 731d37a8f4983b18ded114f05470f8a408deb7cd
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-reusable-ui-using-the-razor-class-library-project-in-aspnet-core"></a><span data-ttu-id="6312f-103">ASP.NET Core에서 Razor 클래스 라이브러리 프로젝트를 사용하여 재사용 가능한 UI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-103">Create reusable UI using the Razor Class Library project in ASP.NET Core.</span></span>

<span data-ttu-id="6312f-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6312f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="6312f-105">Razor 클래스 Library(RCL)에 Razor 보기, 페이지, 컨트롤러, 페이지 모델 및 데이터 모델을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-105">Razor views, pages, controllers, page models, and data models can be built into a Razor Class Library(RCL).</span></span> <span data-ttu-id="6312f-106">RCL은 패키지되고 재사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-106">The RCL can be and packaged and reused.</span></span> <span data-ttu-id="6312f-107">응용 프로그램은 RCL 포함할 수 있고 RCL이 포함하는 보기 및 페이지를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-107">Applications can include the RCL and override the views and pages it contains.</span></span> <span data-ttu-id="6312f-108">보기, 부분 보기 또는 Razor 페이지가 웹앱 및 RCL 모두에 있는 경우 웹앱에서 Razor 태그(*.cshtml* 파일)가 우선적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-108">When a view, partial view, or Razor Page is found in both the web app and the RCL, the Razor markup (*.cshtml* file) in the web app takes precedence.</span></span>

<span data-ttu-id="6312f-109">이 기능을 사용하려면 [!INCLUDE[](~/includes/2.1-SDK.md)]가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-109">This feature requires [!INCLUDE[](~/includes/2.1-SDK.md)]</span></span>

[!INCLUDE[](~/includes/2.1.md)]

<span data-ttu-id="6312f-110">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="6312f-110">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="create-a-class-library-containing-razor-ui"></a><span data-ttu-id="6312f-111">Razor UI를 포함하는 클래스 라이브러리 만들기</span><span class="sxs-lookup"><span data-stu-id="6312f-111">Create a class library containing Razor UI</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="6312f-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6312f-112">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="6312f-113">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-113">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="6312f-114">**새 ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-114">Select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="6312f-115">**ASP.NET Core 2.1** 이상이 선택됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-115">Verify **ASP.NET Core 2.1** or later is selected.</span></span>
* <span data-ttu-id="6312f-116">**Razor 클래스 라이브러리** > **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-116">Select **Razor Class Library** > **OK**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="6312f-117">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6312f-117">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="6312f-118">명령줄에서 `dotnet new razorclasslib`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-118">From the commandline, run `dotnet new razorclasslib`.</span></span> <span data-ttu-id="6312f-119">예:</span><span class="sxs-lookup"><span data-stu-id="6312f-119">For example:</span></span>

``` CLI
dotnet new razorclasslib -o RazorUIClassLib
```

<span data-ttu-id="6312f-120">자세한 내용은 [dotnet new](/dotnet/core/tools/dotnet-new)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-120">For more information, see [dotnet new](/dotnet/core/tools/dotnet-new).</span></span>

------
<span data-ttu-id="6312f-121">RCL에 Razor 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-121">Add Razor files to the RCL.</span></span>

<span data-ttu-id="6312f-122">RCL 콘텐츠를 *영역* 폴더로 이동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-122">We recommend RCL content go in the *Areas* folder.</span></span> 


## <a name="referencing-razor-class-library-content"></a><span data-ttu-id="6312f-123">Razor 클래스 라이브러리 콘텐츠 참조</span><span class="sxs-lookup"><span data-stu-id="6312f-123">Referencing Razor Class Library content</span></span>

<span data-ttu-id="6312f-124">RCL은 다음에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-124">The RCL can be referenced by:</span></span>

* <span data-ttu-id="6312f-125">NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="6312f-125">NuGet package.</span></span> <span data-ttu-id="6312f-126">[NuGet 패키지 만들기](/nuget/create-packages/creating-a-package), [dotnet 추가 패키지](/dotnet/core/tools/dotnet-add-package) 및 [NuGet 패키지 만들기 및 게시](/nuget/quickstart/create-and-publish-a-package-using-visual-studio)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-126">See [Creating NuGet packages](/nuget/create-packages/creating-a-package) and [dotnet add package](/dotnet/core/tools/dotnet-add-package) and [Create and publish a NuGet package](/nuget/quickstart/create-and-publish-a-package-using-visual-studio).</span></span>
* <span data-ttu-id="6312f-127">*{ProjectName}.csproj*.</span><span class="sxs-lookup"><span data-stu-id="6312f-127">*{ProjectName}.csproj*.</span></span> <span data-ttu-id="6312f-128">[dotnet-add reference](/dotnet/core/tools/dotnet-add-reference)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-128">See [dotnet-add reference](/dotnet/core/tools/dotnet-add-reference).</span></span>

### <a name="partial-files-access-in-the-rcl"></a><span data-ttu-id="6312f-129">RCL에 부분 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="6312f-129">Partial files access in the RCL</span></span>

<span data-ttu-id="6312f-130">RCL 외부 콘텐츠의 경우 ASP.NET Core 런타임은 RCL에서 부분 파일을 검색하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-130">For content outside the RCL, the ASP.NET Core runtime does not search for partial files in the RCL.</span></span>

<span data-ttu-id="6312f-131">예를 들어, 샘플 다운로드에서 *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* 부분 보기는 *WebApp1\Pages\About.cshtml* 에서 참조될 수 **없습니다**.</span><span class="sxs-lookup"><span data-stu-id="6312f-131">For example, in the sample download, the *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* partial view can **not** be referenced in *WebApp1\Pages\About.cshtml*.</span></span> <span data-ttu-id="6312f-132">그러나 RCL의 페이지(*RazorUIClassLib/* 는 *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*에 액세스**할 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="6312f-132">However, pages in the RCL ( *RazorUIClassLib/* **can** access *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*.</span></span>

## <a name="walkthrough-create-a-razor-class-library-project-and-use-from-a-razor-pages-project"></a><span data-ttu-id="6312f-133">연습: Razor 클래스 라이브러리 프로젝트를 만들고 Razor 페이지 프로젝트에서 사용</span><span class="sxs-lookup"><span data-stu-id="6312f-133">Walkthrough: Create a Razor Class Library project and use from a Razor Pages project</span></span>

<span data-ttu-id="6312f-134">[전체 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples)를 다운로드하여 만들지 않고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-134">You can download the [complete project](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/ui-class/samples) and test it rather than creating it.</span></span> <span data-ttu-id="6312f-135">샘플 다운로드에는 프로젝트를 쉽게 테스트하게 하는 링크와 추가 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-135">The sample download contains additional code and links that make the project easy to test.</span></span> <span data-ttu-id="6312f-136">샘플 다운로드 대 단계별 지침에 대한 주석을 사용하여 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/6098)에서 사용자 의견을 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-136">You can leave feedback in [this GitHub issue](https://github.com/aspnet/Docs/issues/6098) with your comments on download samples versus step-by-step instructions.</span></span>

### <a name="test-the-download-app"></a><span data-ttu-id="6312f-137">다운로드 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="6312f-137">Test the download app</span></span>

<span data-ttu-id="6312f-138">완료된 앱을 다운로드하지 않고 연습 프로젝트를 만들려는 경우 [다음 섹션](#create-a-razor-class-library)으로 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-138">If you haven't downloaded the completed app and would rather create the walkthrough project, skip to the [next section](#create-a-razor-class-library).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="6312f-139">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6312f-139">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="6312f-140">Visual Studio에서 *.sln* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-140">Open the *.sln* file in Visual Studio.</span></span> <span data-ttu-id="6312f-141">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-141">Run the app.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="6312f-142">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6312f-142">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="6312f-143">*cli* 디렉터리의 명령 프롬프트에서 RCL 및 웹앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-143">From a command prompt in the *cli* directory, build the RCL and web app.</span></span>

``` CLI
dotnet build
```

<span data-ttu-id="6312f-144">*WebApp1* 디렉터리로 이동해 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-144">Move to the *WebApp1* directory and run the app:</span></span>

``` CLI
dotnet run
```
------

<span data-ttu-id="6312f-145">[WebApp1 테스트](#test)의 지침 준수</span><span class="sxs-lookup"><span data-stu-id="6312f-145">Follow the instructions in [Test WebApp1](#test)</span></span>

## <a name="create-a-razor-class-library"></a><span data-ttu-id="6312f-146">Razor 클래스 라이브러리 만들기</span><span class="sxs-lookup"><span data-stu-id="6312f-146">Create a Razor Class Library</span></span>

<span data-ttu-id="6312f-147">이 섹션에서는 Razor 클래스 라이브러리(RCL)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-147">In this section, a Razor Class Library (RCL) is created.</span></span> <span data-ttu-id="6312f-148">Razor 파일이 RCL에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-148">Razor files are added to the RCL.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="6312f-149">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6312f-149">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="6312f-150">RCL 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-150">Create the RCL project:</span></span>

* <span data-ttu-id="6312f-151">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-151">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="6312f-152">**새 ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-152">Select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="6312f-153">**RazorUIClassLib** 앱 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-153">Name the app **RazorUIClassLib**.</span></span>
* <span data-ttu-id="6312f-154">**ASP.NET Core 2.1** 이상이 선택됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-154">Verify **ASP.NET Core 2.1** or later is selected.</span></span>
* <span data-ttu-id="6312f-155">**Razor 클래스 라이브러리** > **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-155">Select **Razor Class Library** > **OK**.</span></span>

<span data-ttu-id="6312f-156">Razor 페이지 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-156">Create the Razor Pages web app:</span></span>

* <span data-ttu-id="6312f-157">**솔루션 탐색기**에서 솔루션 > **추가** >  **새 프로젝트**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-157">From **Solution Explorer**, right-click the solution > **Add** >  **New Project**.</span></span>
* <span data-ttu-id="6312f-158">**새 ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-158">Select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="6312f-159">**WebApp1** 앱 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-159">Name the app **WebApp1**.</span></span>
* <span data-ttu-id="6312f-160">**ASP.NET Core 2.1** 이상이 선택됐는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-160">Verify **ASP.NET Core 2.1** or later is selected.</span></span>
* <span data-ttu-id="6312f-161">**웹 응용 프로그램** > **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-161">Select **Web Application** > **OK**.</span></span>

### <a name="add-razor-files-and-folders-to-the-project"></a><span data-ttu-id="6312f-162">Razor 파일 및 폴더를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-162">Add Razor files and folders to the project.</span></span>

* <span data-ttu-id="6312f-163">*RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*이라는 Razor 부분 보기 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-163">Add a Razor partial view file named *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*.</span></span>
* <span data-ttu-id="6312f-164">*RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*에서 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-164">Replace the markup in *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* with the following code:</span></span>

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml)]

* <span data-ttu-id="6312f-165">WebApp1 프로젝트에서 *_ViewStart.cshtml* 파일을 *RazorUIClassLib/Areas/MyFeature/Pages/_ViewStart.cshtml*으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-165">Copy the *_ViewStart.cshtml* file from the WebApp1 project to  *RazorUIClassLib/Areas/MyFeature/Pages/_ViewStart.cshtml*.</span></span>

  <span data-ttu-id="6312f-166">[viewstart](xref:mvc/views/layout#running-code-before-each-view) 파일은 Razor 페이지 프로젝트의 레이아웃을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-166">The [viewstart](xref:mvc/views/layout#running-code-before-each-view) file is required to use the layout of the Razor Pages project.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="6312f-167">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6312f-167">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="6312f-168">명령줄에서 다음을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="6312f-168">From the command line, run the following:</span></span>

``` CLI
dotnet new razorclasslib -o RazorUIClassLib
dotnet new page -n _Message -np -o RazorUIClassLib/Areas/MyFeature/Pages/Shared
dotnet new viewstart -o RazorUIClassLib/Areas/MyFeature/Pages
```

<span data-ttu-id="6312f-169">이전 명령은:</span><span class="sxs-lookup"><span data-stu-id="6312f-169">The preceding commands:</span></span>

* <span data-ttu-id="6312f-170">`RazorUIClassLib` Razor 클래스 라이브러리(RCL)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-170">Creates the `RazorUIClassLib` Razor Class Library (RCL).</span></span>
* <span data-ttu-id="6312f-171">Razor _Message 페이지를 만들어 RCL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-171">Creates a Razor _Message page, and adds it to the RCL.</span></span> <span data-ttu-id="6312f-172">`-np` 매개 변수는 `PageModel`가 없는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-172">The `-np` parameter creates the page without a `PageModel`.</span></span>
* <span data-ttu-id="6312f-173">[viewstart](xref:mvc/views/layout#running-code-before-each-view) 파일을 만들어 RCL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-173">Creates a [viewstart](xref:mvc/views/layout#running-code-before-each-view) file and adds it to the RCL.</span></span>

<span data-ttu-id="6312f-174">viewstart 파일은 Razor 페이지 프로젝트(다음 섹션에서 추가된)의 레이아웃을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-174">The viewstart file is required to use the layout of the Razor Pages project (which is added in the next section).</span></span>

<span data-ttu-id="6312f-175">Razor 페이지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-175">Update the Razor Pages:</span></span>

* <span data-ttu-id="6312f-176">*RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml*에서 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-176">Replace the markup in *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* with the following code:</span></span>

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml)]

* <span data-ttu-id="6312f-177">*RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml*에서 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-177">Replace the markup in *RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml* with the following code:</span></span>

[!code-html[Main](ui-class/samples/cli/RazorUIClassLib/Areas/MyFeature/Pages/Page1.cshtml)]

<span data-ttu-id="6312f-178">`@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers`은 부분 보기(`<partial name="_Message" />`)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-178">`@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers` is required to use the partial view (`<partial name="_Message" />`).</span></span> <span data-ttu-id="6312f-179">`@addTagHelper` 지시문을 포함하지 않고 *_ViewImports.cshtml* 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-179">Rather than including the `@addTagHelper` directive, you can add a *_ViewImports.cshtml* file.</span></span> <span data-ttu-id="6312f-180">예:</span><span class="sxs-lookup"><span data-stu-id="6312f-180">For example:</span></span>

``` CLI
dotnet new viewimports -o RazorUIClassLib/Areas/MyFeature/Pages
```

<span data-ttu-id="6312f-181">자세한 내용은 [공유된 지시문 가져오기](xref:mvc/views/layout#importing-shared-directives)를 참조</span><span class="sxs-lookup"><span data-stu-id="6312f-181">For more information on viewimports, see [Importing Shared Directives](xref:mvc/views/layout#importing-shared-directives)</span></span>

* <span data-ttu-id="6312f-182">컴파일러 오류가 없는지 확인하려면 클래스 라이브러리를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="6312f-182">Build the class library to verify there are no compiler errors:</span></span>

``` CLI
dotnet build RazorUIClassLib
```

<span data-ttu-id="6312f-183">빌드 출력은 *RazorUIClassLib.dll* 및 *RazorUIClassLib.Views.dll*을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-183">The build output contains *RazorUIClassLib.dll* and *RazorUIClassLib.Views.dll*.</span></span> <span data-ttu-id="6312f-184">*RazorUIClassLib.Views.dll*은 컴파일된 Razor 콘텐츠를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-184">*RazorUIClassLib.Views.dll* contains the compiled Razor content.</span></span>

------

### <a name="use-the-razor-ui-library-from-a-razor-pages-project"></a><span data-ttu-id="6312f-185">Razor 페이지 프로젝트에서 Razor UI 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="6312f-185">Use the Razor UI library from a Razor Pages project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="6312f-186">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6312f-186">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="6312f-187">**솔루션 탐색기**에서 **WebApp1**를 마우스 오른쪽 단추로 클릭하고 **스타트업 프로젝트로 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-187">From **Solution Explorer**, right-click on **WebApp1** and select **Set as StartUp Project**.</span></span>
* <span data-ttu-id="6312f-188">**솔루션 탐색기**에서 **WebApp1**를 마우스 오른쪽 단추로 클릭하고 **빌드 종속성** > **프로젝트 종속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-188">From **Solution Explorer**, right-click on **WebApp1** and select **Build Dependencies** > **Project Dependencies**.</span></span>
* <span data-ttu-id="6312f-189">**RazorUIClassLib**를 **WebApp1**의 종속성으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-189">Check **RazorUIClassLib** as a dependency of **WebApp1**.</span></span>
* <span data-ttu-id="6312f-190">**솔루션 탐색기**에서 **WebApp1**를 마우스 오른쪽 단추로 클릭하고 **추가** > **참조**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-190">From **Solution Explorer**, right-click on **WebApp1** and select **Add** > **Reference**.</span></span>
* <span data-ttu-id="6312f-191">**참조 관리자** 대화 상자에서 **RazorUIClassLib** > **확인**을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-191">In the **Reference Manager** dialog, check **RazorUIClassLib** > **OK**.</span></span>

<span data-ttu-id="6312f-192">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-192">Run the app.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="6312f-193">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6312f-193">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="6312f-194">Razor 페이지 앱 및 Razor 클래스 라이브러리를 포함하는 솔루션 파일 및 Razor 페이지 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-194">Create a Razor Pages web app and a solution file containing the Razor Pages app and the Razor Class Library:</span></span>

``` CLI
dotnet new razor -o WebApp1
dotnet new sln
dotnet sln add WebApp1
dotnet sln add RazorUIClassLib
dotnet add WebApp1 reference RazorUIClassLib
```

<span data-ttu-id="6312f-195">웹앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-195">Build and run the web app:</span></span>

``` CLI
cd WebApp1
dotnet run
```

------

<a name="test"></a>

### <a name="test-webapp1"></a><span data-ttu-id="6312f-196">WebApp1 테스트</span><span class="sxs-lookup"><span data-stu-id="6312f-196">Test WebApp1</span></span>

<span data-ttu-id="6312f-197">Razor UI 클래스 라이브러리를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-197">Verify the Razor UI class library is being used.</span></span>

* <span data-ttu-id="6312f-198">`/MyFeature/Page1`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-198">Browse to `/MyFeature/Page1`.</span></span>

## <a name="override-views-partial-views-and-pages"></a><span data-ttu-id="6312f-199">보기, 부분 보기 및 페이지 재정의</span><span class="sxs-lookup"><span data-stu-id="6312f-199">Override views, partial views, and pages</span></span>

<span data-ttu-id="6312f-200">보기, 부분 보기 또는 Razor 페이지가 웹앱 및 Razor 클래스 라이브러리 모두에 있는 경우 웹앱에서 Razor 태그(*.cshtml* 파일)가 우선적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-200">When a view, partial view, or Razor Page is found in both the web app and the Razor Class Library, the Razor markup (*.cshtml* file) in the web app takes precedence.</span></span> <span data-ttu-id="6312f-201">예를 들어 *WebApp1/Areas/MyFeature/Pages/Page1.cshtml*을 WebApp1에 추가하면 WebApp1의 페이지1은 Razor 클래스 라이브러리의 페이지1에 비해 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-201">For example, add *WebApp1/Areas/MyFeature/Pages/Page1.cshtml* to WebApp1, and Page1 in the WebApp1 will take precedence over Page1in the Razor Class Library.</span></span>

<span data-ttu-id="6312f-202">샘플 다운로드에서 *WebApp1/Areas/MyFeature2*를 *WebApp1/Areas/MyFeature*로 이름을 바꾸어 우선적으로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-202">In the sample download, rename *WebApp1/Areas/MyFeature2* to *WebApp1/Areas/MyFeature* to test precedence.</span></span>

<span data-ttu-id="6312f-203">*RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* 부분 보기를 *WebApp1/Areas/MyFeature/Pages/Shared/_Message.cshtml*에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-203">Copy the *RazorUIClassLib/Areas/MyFeature/Pages/Shared/_Message.cshtml* partial view to *WebApp1/Areas/MyFeature/Pages/Shared/_Message.cshtml*.</span></span> <span data-ttu-id="6312f-204">새 위치를 나타내기 위해 태그를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-204">Update the markup to indicate the new location.</span></span> <span data-ttu-id="6312f-205">해당 부분의 앱 버전이 사용되고 있는지 확인하려면 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6312f-205">Build and run the app to verify the app's version of the partial is being used.</span></span>
