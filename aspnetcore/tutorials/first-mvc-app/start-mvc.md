---
title: ASP.NET Core MVC 시작
author: rick-anderson
description: ASP.NET Core MVC를 시작하는 방법을 알아봅니다.
ms.author: riande
ms.date: 12/12/2018
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: c09c06f55c4179e9e2174f0063ab7387b7e4c31b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56899231"
---
# <a name="get-started-with-aspnet-core-mvc"></a><span data-ttu-id="2d646-103">ASP.NET Core MVC 시작</span><span class="sxs-lookup"><span data-stu-id="2d646-103">Get started with ASP.NET Core MVC</span></span>

<span data-ttu-id="2d646-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2d646-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="2d646-105">이 자습서에서는 ASP.NET Core MVC 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-105">This tutorial teaches the basics of building an ASP.NET Core MVC web app.</span></span>

<span data-ttu-id="2d646-106">앱은 동영상 제목의 데이터베이스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-106">The app manages a database of movie titles.</span></span> <span data-ttu-id="2d646-107">다음과 같은 작업을 수행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2d646-108">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-108">Create a web app.</span></span>
> * <span data-ttu-id="2d646-109">모델 추가 및 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="2d646-109">Add and scaffold a model.</span></span>
> * <span data-ttu-id="2d646-110">데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="2d646-110">Work with a database.</span></span>
> * <span data-ttu-id="2d646-111">검색 및 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="2d646-111">Add search and validation.</span></span>

<span data-ttu-id="2d646-112">마지막으로 동영상 데이터를 관리하고 표시할 수 있는 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-112">At the end, you have an app that can manage and display movie data.</span></span>

[!INCLUDE[](~/includes/mvc-intro/download.md)]

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="2d646-113">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2d646-113">Create a web app</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2d646-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d646-114">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="2d646-115">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-115">From Visual Studio, select  **File > New > Project**.</span></span>

![파일 > 새로 만들기 > 프로젝트](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="2d646-117">**새 프로젝트** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-117">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="2d646-118">왼쪽 창에서 **.NET Core**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-118">In the left pane, select **.NET Core**</span></span>
* <span data-ttu-id="2d646-119">가운데 창에서 **ASP.NET Core 웹 애플리케이션(.NET Core)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-119">In the center pane, select **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="2d646-120">프로젝트 이름을 “MvcMovie”로 지정합니다(코드를 복사할 때 네임스페이스가 일치하도록 프로젝트 이름을 “MvcMovie”로 지정해야 함).</span><span class="sxs-lookup"><span data-stu-id="2d646-120">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="2d646-121">**확인** 선택</span><span class="sxs-lookup"><span data-stu-id="2d646-121">select **OK**</span></span>

![<span data-ttu-id="2d646-122">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="2d646-122">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2-21.png)

<span data-ttu-id="2d646-123">**새 ASP.NET Core 웹 애플리케이션(.NET Core) - MvcMovie** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-123">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="2d646-124">버전 선택기 드롭다운 상자에서 **ASP.NET Core 2.2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-124">In the version selector drop-down box select **ASP.NET Core 2.2**</span></span>
* <span data-ttu-id="2d646-125">**웹 애플리케이션(모델-뷰-컨트롤러)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-125">Select **Web Application (Model-View-Controller)**</span></span>
* <span data-ttu-id="2d646-126">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-126">select **OK**.</span></span>

![<span data-ttu-id="2d646-127">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="2d646-127">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22-21.png)

<span data-ttu-id="2d646-128">Visual Studio에서는 방금 만든 MVC 프로젝트에 대한 기본 템플릿을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-128">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="2d646-129">프로젝트 이름을 입력하고 몇 가지 옵션을 선택하면 바로 앱이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-129">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="2d646-130">다음은 기본 시작 프로젝트이며 여기서 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-130">This is a basic starter project, and it's a good place to start.</span></span>

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="2d646-131">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d646-131">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="2d646-132">이 자습서에서는 VS 코드를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-132">The tutorial assumes familarity with VS Code.</span></span> <span data-ttu-id="2d646-133">자세한 내용은 [VS 코드 시작](https://code.visualstudio.com/docs) 및 [Visual Studio Code 도움말](#visual-studio-code-help)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d646-133">See [Getting started with VS Code](https://code.visualstudio.com/docs) and [Visual Studio Code help](#visual-studio-code-help) for more information.</span></span>

* <span data-ttu-id="2d646-134">[통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-134">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>
* <span data-ttu-id="2d646-135">디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-135">Change directories (`cd`) to a folder which will contain the project.</span></span>
* <span data-ttu-id="2d646-136">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-136">Run the following command:</span></span>

   ```console
   dotnet new mvc -o MvcMovie
   code -r MvcMovie
   ```

  * <span data-ttu-id="2d646-137">**이 있는 대화 상자가 나타나고 'MvcMovie'에서 빌드 및 디버그에 필요한 자산이 누락되었습니다. 추가할까요?**</span><span class="sxs-lookup"><span data-stu-id="2d646-137">A dialog box appears with **Required assets to build and debug are missing from 'MvcMovie'. Add them?**</span></span>  <span data-ttu-id="2d646-138">**예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-138">Select **Yes**</span></span>

  * <span data-ttu-id="2d646-139">`dotnet new mvc -o MvcMovie`: *MvcMovie* 폴더에 새 ASP.NET Core MVC 포로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-139">`dotnet new mvc -o MvcMovie`: creates a new ASP.NET Core MVC project in the *MvcMovie* folder.</span></span>
  * <span data-ttu-id="2d646-140">`code -r MvcMovie`: Visual Studio Code에서 *MvcMovie.csproj* 프로젝트 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-140">`code -r MvcMovie`: Loads the *MvcMovie.csproj* project file in Visual Studio Code.</span></span>

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="2d646-141">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="2d646-141">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="2d646-142">**파일** > **새 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-142">Select **File** > **New Solution**.</span></span>

  ![macOS 새 솔루션](~/tutorials/first-web-api-mac/_static/sln.png)

* <span data-ttu-id="2d646-144">**.NET Core 앱** > **ASP.NET Core** > **ASP.NET Core Web App(MVC)** > **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-144">Select **.NET Core App** > **ASP.NET Core** > **ASP.NET Core Web App (MVC)** > **Next**.</span></span>

  ![macOS 새 프로젝트 대화 상자](~/tutorials/first-mvc-app-mac/start-mvc/1.png)

* <span data-ttu-id="2d646-146">**새 ASP.NET Core Web API 구성** 대화 상자에서 \**.NET Core 2.2*라는 기본 **대상 프레임워크**를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-146">In the **Configure your new ASP.NET Core Web API** dialog, accept the default **Target Framework** of \**.NET Core 2.2*.</span></span>

* <span data-ttu-id="2d646-147">프로젝트 이름을 **MvcMovie**로 지정하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-147">Name the project **MvcMovie**, and then select **Create**.</span></span>

---  
<!-- End of VS tabs -->

### <a name="run-the-app"></a><span data-ttu-id="2d646-148">앱 실행</span><span class="sxs-lookup"><span data-stu-id="2d646-148">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2d646-149">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d646-149">Visual Studio</span></span>](#tab/visual-studio) 

<span data-ttu-id="2d646-150">**Ctrl-F5**를 선택하여 비디버그 모드에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-150">Select **Ctrl-F5** to run the app in non-debug mode.</span></span>

[!INCLUDE[](~/includes/trustCertVS.md)]

* <span data-ttu-id="2d646-151">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-151">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="2d646-152">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-152">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="2d646-153">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-153">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="2d646-154">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-154">When Visual Studio creates a web project, a random port is used for the web server.</span></span>
* <span data-ttu-id="2d646-155">Ctrl+F5(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-155">Launching the app with Ctrl+F5 (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="2d646-156">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-156">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="2d646-157">**디버그** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-157">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

  ![디버그 메뉴](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="2d646-159">**IIS Express** 단추를 선택하여 앱을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-159">You can debug the app by selecting the **IIS Express** button</span></span>

  ![IIS Express](start-mvc/_static/iis_express.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="2d646-161">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d646-161">Visual Studio Code</span></span>](#tab/visual-studio-code) 

<span data-ttu-id="2d646-162">Ctrl+F5를 눌러 디버거 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-162">Press Ctrl+F5 to run without the debugger.</span></span>

[!INCLUDE[](~/includes/trustCertVSC.md)]

  <span data-ttu-id="2d646-163">Visual Studio Code가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `https://localhost:5001`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-163">Visual Studio Code starts starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `https://localhost:5001`.</span></span> <span data-ttu-id="2d646-164">주소 표시줄에 `localhost:port:5001`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-164">The address bar shows `localhost:port:5001` and not something like `example.com`.</span></span> <span data-ttu-id="2d646-165">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-165">That's because `localhost` is the standard hostname for  local computer.</span></span> <span data-ttu-id="2d646-166">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-166">Localhost only serves web requests from the local computer.</span></span>

  <span data-ttu-id="2d646-167">Ctrl+F5(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-167">Launching the app with Ctrl+F5 (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="2d646-168">대부분의 개발자는 페이지 및 보기 변경 내용을 새로 고치기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-168">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="2d646-169">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="2d646-169">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<span data-ttu-id="2d646-170">**실행** > **디버깅하지 않고 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-170">Select **Run** > **Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="2d646-171">Mac용 Visual Studio에서 [Kestrel](xref:fundamentals/servers/index#kestrel) 서버를 시작하고, 브라우저를 실행하며, `http://localhost:port`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-171">Visual Studio for Mac starts [Kestrel](xref:fundamentals/servers/index#kestrel) server, launches a browser, and navigates to `http://localhost:port`, where *port* is a randomly chosen port number.</span></span>

[!INCLUDE[](~/includes/trustCertMac.md)]

* <span data-ttu-id="2d646-172">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-172">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="2d646-173">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-173">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="2d646-174">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-174">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="2d646-175">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-175">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="2d646-176">**실행** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-176">You can launch the app in debug or non-debug mode from the **Run** menu.</span></span>

------

* <span data-ttu-id="2d646-177">**승인**을 선택하여 추적에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-177">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="2d646-178">이 앱은 개인 정보를 추적하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-178">This app doesn't track personal information.</span></span> <span data-ttu-id="2d646-179">템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-179">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

  ![홈 또는 인덱스 페이지](start-mvc/_static/privacy.png)

  <span data-ttu-id="2d646-181">다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-181">The following image shows the app after accepting tracking:</span></span>

  ![홈 또는 인덱스 페이지](start-mvc/_static/home2.2.png)

[!INCLUDE[](~/includes/vs-vsc-vsmac-help.md)]

<span data-ttu-id="2d646-183">이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2d646-183">In the next part of this tutorial, you learn about MVC and start writing some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2d646-184">다음</span><span class="sxs-lookup"><span data-stu-id="2d646-184">Next</span></span>](adding-controller.md)  
