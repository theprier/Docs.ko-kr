---
title: '자습서: ASP.NET Core에서 Razor 페이지 시작'
author: rick-anderson
description: 이 자습서 시리즈는 ASP.NET Core에서 Razor Pages를 사용하는 방법을 보여 줍니다. 모델을 만들고, Razor Pages에 대한 코드를 생성하고, Entity Framework Core 및 SQL Server를 데이터 액세스에 사용하고, 검색 기능을 추가하고, 입력 유효성 검사를 추가하고, 마이그레이션을 사용하여 모델을 업데이트하는 방법을 알아봅니다.
ms.author: riande
ms.date: 12/5/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: bec5838c2efaffb933828260eaf1a840ff202140
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667767"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="7c3e0-104">자습서: ASP.NET Core에서 Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="7c3e0-104">Tutorial: Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="7c3e0-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7c3e0-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="7c3e0-106">이 시리즈의 첫 번째 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-106">This is the first tutorial of a series.</span></span> <span data-ttu-id="7c3e0-107">[시리즈](xref:tutorials/razor-pages/index)에서는 ASP.NET Core Razor Pages 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-107">[The series](xref:tutorials/razor-pages/index) teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span>

[!INCLUDE[](~/includes/advancedRP.md)]

<span data-ttu-id="7c3e0-108">시리즈가 끝나면 영화의 데이터베이스를 관리하는 앱이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-108">At the end of the series you'll have an app that manages a database of movies.</span></span>  

[!INCLUDE[View or download sample code](~/includes/rp/download.md)]

<span data-ttu-id="7c3e0-109">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c3e0-110">Razor Pages 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7c3e0-110">Create a Razor Pages web app.</span></span>
> * <span data-ttu-id="7c3e0-111">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-111">Run the app.</span></span>
> * <span data-ttu-id="7c3e0-112">프로젝트 파일을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-112">Examine the project files.</span></span>

<span data-ttu-id="7c3e0-113">이 자습서가 끝나면 나중에 자습서에서 빌드할 Razor Pages 웹앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-113">At the end of this tutorial you'll have a working Razor Pages web app that you'll build on in later tutorials.</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.2.png)

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="7c3e0-115">Razor 페이지 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7c3e0-115">Create a Razor Pages web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7c3e0-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c3e0-116">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="7c3e0-117">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-117">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>

* <span data-ttu-id="7c3e0-118">새 ASP.NET Core 웹 애플리케이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-118">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="7c3e0-119">프로젝트 이름을 **RazorPagesMovie**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-119">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="7c3e0-120">코드를 복사하여 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-120">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy and paste code.</span></span>

  ![새 ASP.NET Core 웹 애플리케이션](razor-pages-start/_static/np_2.1.png)

* <span data-ttu-id="7c3e0-122">드롭다운에서 **ASP.NET Core 2.2**를 선택한 다음, **웹 애플리케이션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-122">Select **ASP.NET Core 2.2** in the dropdown, and then select **Web Application**.</span></span>

  ![새 ASP.NET Core 웹 애플리케이션](razor-pages-start/_static/np_2_2.2.png)

  <span data-ttu-id="7c3e0-124">다음 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-124">The following starter project is created:</span></span>

  ![솔루션 탐색기](razor-pages-start/_static/se2.2.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="7c3e0-126">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7c3e0-126">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="7c3e0-127">[통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-127">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>

* <span data-ttu-id="7c3e0-128">디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-128">Change directories (`cd`) to a folder which will contain the project.</span></span>

* <span data-ttu-id="7c3e0-129">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-129">Run the following commands:</span></span>

  ```console
  dotnet new webapp -o RazorPagesMovie
  code -r RazorPagesMovie
  ```

  * <span data-ttu-id="7c3e0-130">`dotnet new` 명령은 *RazorPagesMovie* 폴더에서 새 Razor Pages 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-130">The `dotnet new` command creates a new Razor Pages project in the *RazorPagesMovie* folder.</span></span>
  * <span data-ttu-id="7c3e0-131">`code` 명령은 Visual Studio Code의 새 인스턴스에서 *RazorPagesMovie* 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-131">The `code` command opens the *RazorPagesMovie* folder in a new instance of Visual Studio Code.</span></span>

  <span data-ttu-id="7c3e0-132">다음과 같은 대화 상자가 표시됩니다. **빌드 및 디버그에 필요한 자산이 'RazorPagesMovie'에서 누락되었습니다. 추가할까요?**</span><span class="sxs-lookup"><span data-stu-id="7c3e0-132">A dialog box appears with **Required assets to build and debug are missing from 'RazorPagesMovie'. Add them?**</span></span>

* <span data-ttu-id="7c3e0-133">**예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-133">Select **Yes**</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="7c3e0-134">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="7c3e0-134">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="7c3e0-135">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-135">From a terminal, run the following commands:</span></span>

<!-- TODO: update these instruction once mac support 2.2 projects -->

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
```

<span data-ttu-id="7c3e0-136">이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 Razor Pages 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-136">The preceding commands use the [.NET Core CLI](/dotnet/core/tools/dotnet) to create a Razor Pages project.</span></span>

## <a name="open-the-project"></a><span data-ttu-id="7c3e0-137">프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="7c3e0-137">Open the project</span></span>

<span data-ttu-id="7c3e0-138">Visual Studio에서 **파일 > 열기**를 선택하고 *RazorPagesMovie.csproj* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-138">From Visual Studio, select **File > Open**, and then select the *RazorPagesMovie.csproj* file.</span></span>

<!-- End of VS tabs -->

---

## <a name="run-the-web-app"></a><span data-ttu-id="7c3e0-139">웹 앱 실행</span><span class="sxs-lookup"><span data-stu-id="7c3e0-139">Run the web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7c3e0-140">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c3e0-140">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="7c3e0-141">Ctrl+F5를 눌러 디버거 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-141">Press Ctrl+F5 to run without the debugger.</span></span>

  <span data-ttu-id="7c3e0-142">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-142">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="7c3e0-143">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-143">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="7c3e0-144">`localhost`가 로컬 컴퓨터의 표준 호스트 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-144">That's because `localhost` is the standard hostname for the local computer.</span></span> <span data-ttu-id="7c3e0-145">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-145">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="7c3e0-146">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-146">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="7c3e0-147">이전 이미지에서 포트 번호는 5001입니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-147">In the preceding image, the port number is 5001.</span></span> <span data-ttu-id="7c3e0-148">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-148">When you run the app, you'll see a different port number.</span></span>
  
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="7c3e0-149">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7c3e0-149">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="7c3e0-150">**Ctrl-F5** 키를 눌러서 디버거 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-150">Press **Ctrl-F5** to run without the debugger.</span></span>

  <span data-ttu-id="7c3e0-151">Visual Studio Code가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-151">Visual Studio Code starts starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5001`.</span></span> <span data-ttu-id="7c3e0-152">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-152">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="7c3e0-153">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-153">That's because `localhost` is the standard hostname for  local computer.</span></span> <span data-ttu-id="7c3e0-154">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-154">Localhost only serves web requests from the local computer.</span></span>
  
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="7c3e0-155">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="7c3e0-155">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="7c3e0-156">**실행 > 디버깅하지 않고 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-156">Select **Run > Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="7c3e0-157">Visual Studio가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-157">Visual Studio starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5001`.</span></span>

<!-- End of VS tabs -->

---

* <span data-ttu-id="7c3e0-158">앱의 홈페이지에서 **승인**을 선택하여 추적에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-158">On the app's home page, select **Accept** to consent to tracking.</span></span>

  <span data-ttu-id="7c3e0-159">이 앱은 개인 정보를 추적하지 않지만 유럽 연합의 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 준수하기 위해 필요한 경우 프로젝트 템플릿에는 동의 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-159">This app doesn't track personal information, but the project template includes the consent feature in case you need it to comply with the European Union's [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/homeGDPR2.2.png)

  <span data-ttu-id="7c3e0-161">다음 이미지에서는 추적에 동의한 후에 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-161">The following image shows the app after you give consent to tracking:</span></span>

  ![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.2.png)

## <a name="examine-the-project-files"></a><span data-ttu-id="7c3e0-163">프로젝트 파일 검사</span><span class="sxs-lookup"><span data-stu-id="7c3e0-163">Examine the project files</span></span>

<span data-ttu-id="7c3e0-164">이후 자습서에서 작업할 주요 프로젝트 폴더 및 파일에 대한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-164">Here's an overview of the main project folders and files that you'll work with in later tutorials.</span></span>

### <a name="pages-folder"></a><span data-ttu-id="7c3e0-165">페이지 폴더</span><span class="sxs-lookup"><span data-stu-id="7c3e0-165">Pages folder</span></span>

<span data-ttu-id="7c3e0-166">Razor 페이지 및 지원 파일이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-166">Contains Razor pages and supporting files.</span></span> <span data-ttu-id="7c3e0-167">각 Razor 페이지는 파일 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-167">Each Razor page is a pair of files:</span></span>

* <span data-ttu-id="7c3e0-168">Razor 구문을 사용하는 C# 코드로 HTML 태그를 포함하는 *.cshtml* 파일.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-168">A *.cshtml* file that contains HTML markup with C# code using Razor syntax.</span></span>
* <span data-ttu-id="7c3e0-169">페이지 이벤트를 처리하는 C# 코드가 포함된 *.cshtml.cs* 파일.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-169">A *.cshtml.cs* file that contains C# code that handles page events.</span></span>

<span data-ttu-id="7c3e0-170">지원 파일에는 밑줄로 시작하는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-170">Supporting files have names that begin with an underscore.</span></span> <span data-ttu-id="7c3e0-171">예를 들어 *_Layout.cshtml* 파일은 모든 페이지에 공통되는 UI 요소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-171">For example, the *_Layout.cshtml* file configures UI elements common to all pages.</span></span> <span data-ttu-id="7c3e0-172">이 파일은 페이지 맨 위에 있는 탐색 메뉴를 설정하고 페이지 맨 아래에 저작권 표시를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-172">This file sets up the navigation menu at the top of the page and the copyright notice at the bottom of the page.</span></span> <span data-ttu-id="7c3e0-173">자세한 내용은 <xref:mvc/views/layout>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-173">For more information, see <xref:mvc/views/layout>.</span></span>


### <a name="wwwroot-folder"></a><span data-ttu-id="7c3e0-174">wwwroot 폴더</span><span class="sxs-lookup"><span data-stu-id="7c3e0-174">wwwroot folder</span></span>

<span data-ttu-id="7c3e0-175">HTML 파일, JavaScript 파일 및 CSS 파일과 같은 정적 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-175">Contains static files, such as HTML files, JavaScript files, and CSS files.</span></span> <span data-ttu-id="7c3e0-176">자세한 내용은 <xref:fundamentals/static-files>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-176">For more information, see <xref:fundamentals/static-files>.</span></span>

### <a name="appsettingsjson"></a><span data-ttu-id="7c3e0-177">appSettings.json</span><span class="sxs-lookup"><span data-stu-id="7c3e0-177">appSettings.json</span></span>

<span data-ttu-id="7c3e0-178">연결 문자열과 같은 구성 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-178">Contains configuration data, such as connection strings.</span></span> <span data-ttu-id="7c3e0-179">자세한 내용은 <xref:fundamentals/configuration/index>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-179">For more information, see <xref:fundamentals/configuration/index>.</span></span>

### <a name="programcs"></a><span data-ttu-id="7c3e0-180">Program.cs</span><span class="sxs-lookup"><span data-stu-id="7c3e0-180">Program.cs</span></span>

<span data-ttu-id="7c3e0-181">프로그램의 진입점을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-181">Contains the entry point for the program.</span></span> <span data-ttu-id="7c3e0-182">자세한 내용은 <xref:fundamentals/host/web-host>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-182">For more information, see <xref:fundamentals/host/web-host>.</span></span>

### <a name="startupcs"></a><span data-ttu-id="7c3e0-183">Startup.cs</span><span class="sxs-lookup"><span data-stu-id="7c3e0-183">Startup.cs</span></span>

<span data-ttu-id="7c3e0-184">쿠키에 대한 동의 필요 여부 등 앱 동작을 구성하는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-184">Contains code that configures app behavior, such as whether it requires consent for cookies.</span></span> <span data-ttu-id="7c3e0-185">자세한 내용은 <xref:fundamentals/startup>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-185">For more information, see <xref:fundamentals/startup>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c3e0-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c3e0-186">Next steps</span></span>

<span data-ttu-id="7c3e0-187">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-187">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c3e0-188">Razor Pages 웹앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-188">Created a Razor Pages web app.</span></span>
> * <span data-ttu-id="7c3e0-189">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-189">Ran the app.</span></span>
> * <span data-ttu-id="7c3e0-190">프로젝트 파일을 검사했습니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-190">Examined the project files.</span></span>

<span data-ttu-id="7c3e0-191">시리즈의 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c3e0-191">Advance to the next tutorial in the series:</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7c3e0-192">모델 추가</span><span class="sxs-lookup"><span data-stu-id="7c3e0-192">Add a model</span></span>](xref:tutorials/razor-pages/model)
