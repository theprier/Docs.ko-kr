---
title: ASP.NET Core에서 Razor 페이지 시작
author: rick-anderson
monikerRange: '>= aspnetcore-2.2'
description: 이 자습서 시리즈는 ASP.NET Core에서 Razor Pages를 사용하는 방법을 보여 줍니다. 모델을 만들고, Razor Pages에 대한 코드를 생성하고, Entity Framework Core 및 SQL Server를 데이터 액세스에 사용하고, 검색 기능을 추가하고, 입력 유효성 검사를 추가하고, 마이그레이션을 사용하여 모델을 업데이트하는 방법을 알아봅니다.
ms.author: riande
ms.date: 12/5/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 1152ebfcee48a46ecd28c941fce32d3fc1e05c41
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861630"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="a20ae-104">자습서: ASP.NET Core에서 Razor Pages 시작</span><span class="sxs-lookup"><span data-stu-id="a20ae-104">Tutorial: Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="a20ae-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a20ae-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a20ae-106">이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-106">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span>

<span data-ttu-id="a20ae-107">앱은 동영상 제목의 데이터베이스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-107">The app manages a database of movie titles.</span></span> <span data-ttu-id="a20ae-108">다음과 같은 작업을 수행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-108">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a20ae-109">Razor Pages 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a20ae-109">Create a Razor Pages web app.</span></span>
> * <span data-ttu-id="a20ae-110">모델 추가 및 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="a20ae-110">Add and scaffold a model.</span></span>
> * <span data-ttu-id="a20ae-111">데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="a20ae-111">Work with a database.</span></span>
> * <span data-ttu-id="a20ae-112">검색 및 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="a20ae-112">Add search and validation.</span></span>

<span data-ttu-id="a20ae-113">작업을 완료하면 앱에서 동영상 제목 항목을 관리하고 표시할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-113">At the end, you have an app that can manage and display movie titles items.</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

## <a name="prerequisites"></a><span data-ttu-id="a20ae-114">전제 조건</span><span class="sxs-lookup"><span data-stu-id="a20ae-114">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="a20ae-115">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a20ae-115">Create a Razor web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a20ae-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a20ae-116">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="a20ae-117">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-117">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="a20ae-118">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-118">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="a20ae-119">프로젝트 이름을 **RazorPagesMovie**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-119">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="a20ae-120">코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-120">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
 <span data-ttu-id="a20ae-121">![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2.1.png)</span><span class="sxs-lookup"><span data-stu-id="a20ae-121">![new ASP.NET Core Web Application](razor-pages-start/_static/np_2.1.png)</span></span>

* <span data-ttu-id="a20ae-122">드롭다운에서 **ASP.NET Core 2.2**를 선택한 다음, **웹 애플리케이션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-122">Select **ASP.NET Core 2.2** in the dropdown, and then select **Web Application**.</span></span>

  ![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2_2.2.png)

  <span data-ttu-id="a20ae-124">다음 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-124">The following starter project is created:</span></span>

  ![솔루션 탐색기](razor-pages-start/_static/se2.2.png)

* <span data-ttu-id="a20ae-126">**Ctrl-F5** 키를 눌러서 디버거 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-126">Press **Ctrl-F5** to run without the debugger.</span></span>

  <span data-ttu-id="a20ae-127">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-127">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="a20ae-128">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-128">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="a20ae-129">`localhost`가 로컬 컴퓨터의 표준 호스트 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-129">That's because `localhost` is the standard hostname for the local computer.</span></span> <span data-ttu-id="a20ae-130">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-130">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="a20ae-131">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-131">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="a20ae-132">이전 이미지에서 포트 번호는 5001입니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-132">In the preceding image, the port number is 5001.</span></span> <span data-ttu-id="a20ae-133">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-133">When you run the app, you'll see a different port number.</span></span>

  <span data-ttu-id="a20ae-134">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-134">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="a20ae-135">대부분의 개발자는 페이지 및 보기 변경 내용을 새로 고치기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-135">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="a20ae-136">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a20ae-136">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="a20ae-137">[통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-137">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>
* <span data-ttu-id="a20ae-138">디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-138">Change directories (`cd`) to a folder which will contain the project.</span></span>
* <span data-ttu-id="a20ae-139">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-139">Run the following command:</span></span>

   ```console
   dotnet new webapp -o RazorPagesMovie
   code -r RazorPagesMovie
   ```

  * <span data-ttu-id="a20ae-140">다음과 같은 대화 상자가 표시됩니다. **빌드 및 디버그에 필요한 자산이 'RazorPagesMovie'에서 누락되었습니다. 추가할까요?**</span><span class="sxs-lookup"><span data-stu-id="a20ae-140">A dialog box appears with **Required assets to build and debug are missing from 'RazorPagesMovie'. Add them?**</span></span>  <span data-ttu-id="a20ae-141">**예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-141">Select **Yes**</span></span>

  * <span data-ttu-id="a20ae-142">`dotnet new webapp -o RazorPagesMovie`: *RazorPagesMovie* 폴더에서 새 Razor Pages 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-142">`dotnet new webapp -o RazorPagesMovie`: creates a new Razor Pages project in the *RazorPagesMovie* folder.</span></span>
  * <span data-ttu-id="a20ae-143">`code -r RazorPagesMovie`: Visual Studio Code에서 *RazorPagesMovie.csproj* 프로젝트 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-143">`code -r RazorPagesMovie`: Loads the *RazorPagesMovie.csproj* project file in Visual Studio Code.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="a20ae-144">앱 시작</span><span class="sxs-lookup"><span data-stu-id="a20ae-144">Launch the app</span></span>

* <span data-ttu-id="a20ae-145">**Ctrl-F5** 키를 눌러서 디버거 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-145">Press **Ctrl-F5** to run without the debugger.</span></span>

  <span data-ttu-id="a20ae-146">Visual Studio Code가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-146">Visual Studio Code starts starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5001`.</span></span> <span data-ttu-id="a20ae-147">주소 표시줄에 `localhost:port:5001`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-147">The address bar shows `localhost:port:5001` and not something like `example.com`.</span></span> <span data-ttu-id="a20ae-148">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-148">That's because `localhost` is the standard hostname for  local computer.</span></span> <span data-ttu-id="a20ae-149">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-149">Localhost only serves web requests from the local computer.</span></span>

  <span data-ttu-id="a20ae-150">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-150">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="a20ae-151">대부분의 개발자는 페이지 및 보기 변경 내용을 새로 고치기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-151">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="a20ae-152">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="a20ae-152">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="a20ae-153">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-153">From a terminal, run the following commands:</span></span>

<!-- TODO: update these instruction once mac support 2.2 projects -->

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

<span data-ttu-id="a20ae-154">이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 Razor 페이지 프로젝트를 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-154">The preceding commands use the [.NET Core CLI](/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="a20ae-155">브라우저를 열고 http://localhost:5000으로 이동하여 응용 프로그램을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-155">Open a browser to http://localhost:5000 to view the application.</span></span>

## <a name="open-the-project"></a><span data-ttu-id="a20ae-156">프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="a20ae-156">Open the project</span></span>

<span data-ttu-id="a20ae-157">Ctrl+C를 눌러 응용 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-157">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="a20ae-158">Visual Studio에서 **파일 > 열기**를 선택하고 *RazorPagesMovie.csproj* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-158">From Visual Studio, select **File > Open**, and then select the *RazorPagesMovie.csproj* file.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="a20ae-159">앱 시작</span><span class="sxs-lookup"><span data-stu-id="a20ae-159">Launch the app</span></span>

<span data-ttu-id="a20ae-160">**실행 > 디버깅하지 않고 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-160">Select **Run > Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="a20ae-161">Visual Studio가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-161">Visual Studio starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5001`.</span></span>

<!-- End of VS tabs -->

---

* <span data-ttu-id="a20ae-162">**승인**을 선택하여 추적에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-162">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="a20ae-163">이 앱은 개인 정보를 추적하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-163">This app doesn't track personal information.</span></span> <span data-ttu-id="a20ae-164">템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-164">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/homeGDPR2.2.png)

  <span data-ttu-id="a20ae-166">다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-166">The following image shows the app after accepting tracking:</span></span>

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.2.png)

## <a name="project-files-and-folders"></a><span data-ttu-id="a20ae-168">프로젝트 파일 및 폴더</span><span class="sxs-lookup"><span data-stu-id="a20ae-168">Project files and folders</span></span>

<span data-ttu-id="a20ae-169">다음 표에는 프로젝트의 파일 및 폴더가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-169">The following table lists the files and folders in the project.</span></span> <span data-ttu-id="a20ae-170">자습서의 이 시점에서 *Startup.cs* 파일을 이해하는 것이 가장 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-170">At this point in the tutorial, the *Startup.cs* file is the most important to understand.</span></span> <span data-ttu-id="a20ae-171">아래 제공된 각 링크를 검토할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-171">You don't need to review each link provided below.</span></span> <span data-ttu-id="a20ae-172">프로젝트의 파일이나 폴더에 대한 자세한 정보가 필요할 경우 링크가 참조로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-172">The links are provided as a reference when you need more information on a file or folder in the project.</span></span>

| <span data-ttu-id="a20ae-173">파일 또는 폴더</span><span class="sxs-lookup"><span data-stu-id="a20ae-173">File or folder</span></span>              | <span data-ttu-id="a20ae-174">용도</span><span class="sxs-lookup"><span data-stu-id="a20ae-174">Purpose</span></span> |
| ----------------- | ------------ |
| <span data-ttu-id="a20ae-175">*wwwroot*</span><span class="sxs-lookup"><span data-stu-id="a20ae-175">*wwwroot*</span></span> | <span data-ttu-id="a20ae-176">정적 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-176">Contains static files.</span></span> <span data-ttu-id="a20ae-177">[고정 파일](xref:fundamentals/static-files)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a20ae-177">See [Static files](xref:fundamentals/static-files).</span></span> |
| <span data-ttu-id="a20ae-178">*페이지*</span><span class="sxs-lookup"><span data-stu-id="a20ae-178">*Pages*</span></span> | <span data-ttu-id="a20ae-179">[Razor 페이지](xref:razor-pages/index)에 대한 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-179">Folder for [Razor Pages](xref:razor-pages/index).</span></span> |
| <span data-ttu-id="a20ae-180">*appsettings.json*</span><span class="sxs-lookup"><span data-stu-id="a20ae-180">*appsettings.json*</span></span> | [<span data-ttu-id="a20ae-181">구성</span><span class="sxs-lookup"><span data-stu-id="a20ae-181">Configuration</span></span>](xref:fundamentals/configuration/index) |
| <span data-ttu-id="a20ae-182">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="a20ae-182">*Program.cs*</span></span> | <span data-ttu-id="a20ae-183">ASP.NET Core 앱을 [호스트](xref:fundamentals/host/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-183">[Hosts](xref:fundamentals/host/index) the ASP.NET Core app.</span></span>|
| <span data-ttu-id="a20ae-184">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="a20ae-184">*Startup.cs*</span></span> | <span data-ttu-id="a20ae-185">서비스 및 요청 파이프라인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-185">Configures services and the request pipeline.</span></span> <span data-ttu-id="a20ae-186">[시작](xref:fundamentals/startup)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a20ae-186">See [Startup](xref:fundamentals/startup).</span></span>|

### <a name="the-pages-folder"></a><span data-ttu-id="a20ae-187">Pages 폴더</span><span class="sxs-lookup"><span data-stu-id="a20ae-187">The Pages folder</span></span>

<span data-ttu-id="a20ae-188">*_Layout.cshtml* 파일은 공통적인 HTML 요소(스크립트 및 스타일시트)를 포함하고 응용 프로그램 레이아웃을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-188">The *_Layout.cshtml* file contains common HTML elements (scripts and stylesheets) and sets the layout for the application.</span></span> <span data-ttu-id="a20ae-189">예를 들어 **RazorPagesMovie**, **홈** 또는 **개인 정보**를 클릭하면 동일한 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-189">For example, when you click on **RazorPagesMovie**, **Home**, or **Privacy**, you see the same elements.</span></span> <span data-ttu-id="a20ae-190">공통적인 요소에는 창 위쪽의 탐색 메뉴 및 아래쪽의 헤더가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-190">The common elements include the navigation menu on the top and the header on the bottom of the window.</span></span> <span data-ttu-id="a20ae-191">자세한 내용은 [레이아웃](xref:mvc/views/layout)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a20ae-191">See [Layout](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="a20ae-192">*_ViewImports.cshtml* 파일에는 각 Razor 페이지로 가져온 Razor 지시문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-192">The *_ViewImports.cshtml* file contains Razor directives that are imported into each Razor Page.</span></span> <span data-ttu-id="a20ae-193">자세한 내용은 [공유된 지시문 가져오기](xref:mvc/views/layout#importing-shared-directives)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a20ae-193">See [Importing Shared Directives](xref:mvc/views/layout#importing-shared-directives) for more information.</span></span>

<span data-ttu-id="a20ae-194">*_ViewStart.cshtml*은 Razor 페이지 `Layout` 속성을 설정하여 *_Layout.cshtml* 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-194">The *_ViewStart.cshtml* sets the Razor Pages `Layout` property to use the *_Layout.cshtml* file.</span></span> <span data-ttu-id="a20ae-195">자세한 내용은 [레이아웃](xref:mvc/views/layout)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a20ae-195">See [Layout](xref:mvc/views/layout) for more information.</span></span>

<span data-ttu-id="a20ae-196">*_ValidationScriptsPartial.cshtml* 파일은 [jQuery](https://jquery.com/) 유효성 검사 스크립트에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-196">The *_ValidationScriptsPartial.cshtml* file provides a reference to [jQuery](https://jquery.com/) validation scripts.</span></span> <span data-ttu-id="a20ae-197">자습서의 뒷부분에서 `Create` 및 `Edit` 페이지를 추가하면 *_ValidationScriptsPartial.cshtml* 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-197">When the `Create` and `Edit` pages are added later in the tutorial, the *_ValidationScriptsPartial.cshtml* file will be used.</span></span>

<span data-ttu-id="a20ae-198">다음 작업에 `Index`, `Error` 및 `Privacy` 페이지가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-198">`Index`, `Error`, and `Privacy` pages are provided to:</span></span>

* <span data-ttu-id="a20ae-199">`Index`: 앱 시작</span><span class="sxs-lookup"><span data-stu-id="a20ae-199">`Index`: Start an app.</span></span>
* <span data-ttu-id="a20ae-200">`Error`: 오류 정보 표시</span><span class="sxs-lookup"><span data-stu-id="a20ae-200">`Error`: Display error information.</span></span>
* <span data-ttu-id="a20ae-201">`Privacy`: 사이트의 개인 정보 취급 방침에 대한 세부 정보 지정</span><span class="sxs-lookup"><span data-stu-id="a20ae-201">`Privacy`: Specify details about the site's privacy policy.</span></span>

<span data-ttu-id="a20ae-202">이 자습서에서는 이전 페이지를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-202">For this tutorial, the preceding pages are not used.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="a20ae-203">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a20ae-203">Visual Studio</span></span>](#tab/visual-studio)

<a name="f7"></a>
### <a name="use-f7-to-toggle-between-a-razor-page-and-the-pagemodel"></a><span data-ttu-id="a20ae-204">F7 키를 사용하여 Razor 페이지와 PageModel 간에 토글</span><span class="sxs-lookup"><span data-stu-id="a20ae-204">Use F7 to toggle between a Razor Page and the PageModel</span></span>

<span data-ttu-id="a20ae-205">F7 키를 사용하면 Razor Page(*\*.cshtml* 파일)와 C# 파일(*\*.cshtml.cs*)을 토글할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-205">F7 toggles between a Razor Page (*\*.cshtml* file) and the C# file (*\*.cshtml.cs*).</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="a20ae-206">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a20ae-206">Visual Studio Code</span></span>](#tab/visual-studio-code)

<!-- TODO review  Need something in these tabs -->

<span data-ttu-id="a20ae-207">규칙에 따라 Razor Page(*\*.cshtml* 파일)와 연결된 `PageModel`에는 동일한 루트 파일 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-207">By convention, the Razor Page (*\*.cshtml* file) and the associated `PageModel` have the same root file name.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="a20ae-208">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="a20ae-208">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="a20ae-209">규칙에 따라 Razor Page(*\*.cshtml* 파일)와 연결된 `PageModel`에는 동일한 루트 파일 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a20ae-209">By convention, the Razor Page (*\*.cshtml* file) and the associated `PageModel` have the same root file name.</span></span>

---

> [!div class="step-by-step"]
> [<span data-ttu-id="a20ae-210">다음: 모델 추가</span><span class="sxs-lookup"><span data-stu-id="a20ae-210">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)