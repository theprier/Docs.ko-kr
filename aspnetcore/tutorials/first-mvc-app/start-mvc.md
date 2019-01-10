---
title: ASP.NET Core MVC 시작
author: rick-anderson
monikerRange: '>= aspnetcore-2.2'
description: ASP.NET Core MVC를 시작하는 방법을 알아봅니다.
ms.author: riande
ms.date: 12/12/2018
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: cfce3b5792a5d0673bae5ddbba9e2d4d515a6279
ms.sourcegitcommit: 4e87712029de2aceb1cf2c52e9e3dda8195a5b8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53381805"
---
# <a name="get-started-with-aspnet-core-mvc"></a><span data-ttu-id="38cfe-103">ASP.NET Core MVC 시작</span><span class="sxs-lookup"><span data-stu-id="38cfe-103">Get started with ASP.NET Core MVC</span></span>

<span data-ttu-id="38cfe-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="38cfe-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

https://docs.microsoft.com/en-us/visualstudio/ide/visual-studio-ide?view=vs-2017

<span data-ttu-id="38cfe-105">이 자습서에서는 ASP.NET Core MVC 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-105">This tutorial teaches the basics of building an ASP.NET Core MVC web app.</span></span>

<span data-ttu-id="38cfe-106">앱은 동영상 제목의 데이터베이스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-106">The app manages a database of movie titles.</span></span> <span data-ttu-id="38cfe-107">다음과 같은 작업을 수행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38cfe-108">웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-108">Create a web app.</span></span>
> * <span data-ttu-id="38cfe-109">모델 추가 및 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="38cfe-109">Add and scaffold a model.</span></span>
> * <span data-ttu-id="38cfe-110">데이터베이스 작업</span><span class="sxs-lookup"><span data-stu-id="38cfe-110">Work with a database.</span></span>
> * <span data-ttu-id="38cfe-111">검색 및 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="38cfe-111">Add search and validation.</span></span>

<span data-ttu-id="38cfe-112">마지막으로 동영상 데이터를 관리하고 표시할 수 있는 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-112">At the end, you have an app that can manage and display movie data.</span></span>

[!INCLUDE[](~/includes/mvc-intro/download.md)]

> [!NOTE]
> <span data-ttu-id="38cfe-113">ASP.NET Core 목차에 대해 제안된 새 구조의 유용성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-113">We’re testing the usability of a proposed new structure for the ASP.NET Core table of contents.</span></span>  <span data-ttu-id="38cfe-114">몇 분 동안 현재 또는 제안된 목차에서 다른 7개의 항목을 찾는 연습을 수행하는 경우 [여기를 클릭하여 연구에 참여하세요](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82).</span><span class="sxs-lookup"><span data-stu-id="38cfe-114">If you have a few minutes to try an exercise of finding 7 different topics in the current or proposed table of contents, please [click here to participate in the study](https://dpk4xbh5.optimalworkshop.com/treejack/aa11wn82).</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="38cfe-115">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="38cfe-115">Create a web app</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="38cfe-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38cfe-116">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="38cfe-117">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-117">From Visual Studio, select  **File > New > Project**.</span></span>

![파일 > 새로 만들기 > 프로젝트](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="38cfe-119">**새 프로젝트** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-119">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="38cfe-120">왼쪽 창에서 **.NET Core**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-120">In the left pane, select **.NET Core**</span></span>
* <span data-ttu-id="38cfe-121">가운데 창에서 **ASP.NET Core 웹 애플리케이션(.NET Core)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-121">In the center pane, select **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="38cfe-122">프로젝트 이름을 “MvcMovie”로 지정합니다(코드를 복사할 때 네임스페이스가 일치하도록 프로젝트 이름을 “MvcMovie”로 지정해야 함).</span><span class="sxs-lookup"><span data-stu-id="38cfe-122">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="38cfe-123">**확인** 선택</span><span class="sxs-lookup"><span data-stu-id="38cfe-123">select **OK**</span></span>

![<span data-ttu-id="38cfe-124">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="38cfe-124">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2-21.png)

<span data-ttu-id="38cfe-125">**새 ASP.NET Core 웹 애플리케이션(.NET Core) - MvcMovie** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-125">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="38cfe-126">버전 선택기 드롭다운 상자에서 **ASP.NET Core 2.2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-126">In the version selector drop-down box select **ASP.NET Core 2.2**</span></span>
* <span data-ttu-id="38cfe-127">**웹 애플리케이션(모델-뷰-컨트롤러)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-127">Select **Web Application (Model-View-Controller)**</span></span>
* <span data-ttu-id="38cfe-128">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-128">select **OK**.</span></span>

![<span data-ttu-id="38cfe-129">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="38cfe-129">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22-21.png)

<span data-ttu-id="38cfe-130">Visual Studio에서는 방금 만든 MVC 프로젝트에 대한 기본 템플릿을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-130">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="38cfe-131">프로젝트 이름을 입력하고 몇 가지 옵션을 선택하면 바로 앱이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-131">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="38cfe-132">다음은 기본 시작 프로젝트이며 여기서 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-132">This is a basic starter project, and it's a good place to start.</span></span>

<span data-ttu-id="38cfe-133">**Ctrl-F5**를 선택하여 비디버그 모드에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-133">Select **Ctrl-F5** to run the app in non-debug mode.</span></span>

* <span data-ttu-id="38cfe-134">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-134">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="38cfe-135">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-135">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="38cfe-136">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-136">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="38cfe-137">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-137">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="38cfe-138">위 이미지에서 포트 번호는 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-138">In the image above, the port number is 5000.</span></span> <span data-ttu-id="38cfe-139">브라우저의 URL에는 `localhost:5000`이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-139">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="38cfe-140">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-140">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="38cfe-141">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-141">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="38cfe-142">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-142">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="38cfe-143">**디버그** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-143">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![디버그 메뉴](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="38cfe-145">**IIS Express** 단추를 선택하여 앱을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-145">You can debug the app by selecting the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="38cfe-147">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="38cfe-147">Visual Studio Code</span></span>](#tab/visual-studio-code)

<span data-ttu-id="38cfe-148">이 자습서에서는 VS 코드를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-148">The tutorial assumes familarity with VS Code.</span></span> <span data-ttu-id="38cfe-149">자세한 내용은 [VS 코드 시작](https://code.visualstudio.com/docs) 및 [Visual Studio Code 도움말](#visual-studio-code-help)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38cfe-149">See [Getting started with VS Code](https://code.visualstudio.com/docs) and [Visual Studio Code help](#visual-studio-code-help) for more information.</span></span>

* <span data-ttu-id="38cfe-150">[통합 터미널](https://code.visualstudio.com/docs/editor/integrated-terminal)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-150">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal).</span></span>
* <span data-ttu-id="38cfe-151">디렉터리(`cd`)를 프로젝트를 포함하는 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-151">Change directories (`cd`) to a folder which will contain the project.</span></span>
* <span data-ttu-id="38cfe-152">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-152">Run the following command:</span></span>

   ```console
   dotnet new mvc -o MvcMovie
   code -r MvcMovie
   ```

  * <span data-ttu-id="38cfe-153">**이 있는 대화 상자가 나타나고 'MvcMovie'에서 빌드 및 디버그에 필요한 자산이 누락되었습니다. 추가할까요?**</span><span class="sxs-lookup"><span data-stu-id="38cfe-153">A dialog box appears with **Required assets to build and debug are missing from 'MvcMovie'. Add them?**</span></span>  <span data-ttu-id="38cfe-154">**예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-154">Select **Yes**</span></span>

  * <span data-ttu-id="38cfe-155">`dotnet new mvc -o MvcMovie`: *MvcMovie* 폴더에 새 ASP.NET Core MVC 포로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-155">`dotnet new mvc -o MvcMovie`: creates a new ASP.NET Core MVC project in the *MvcMovie* folder.</span></span>
  * <span data-ttu-id="38cfe-156">`code -r MvcMovie`: Visual Studio Code에서 *MvcMovie.csproj* 프로젝트 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-156">`code -r MvcMovie`: Loads the *MvcMovie.csproj* project file in Visual Studio Code.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="38cfe-157">앱 시작</span><span class="sxs-lookup"><span data-stu-id="38cfe-157">Launch the app</span></span>

* <span data-ttu-id="38cfe-158">**Ctrl-F5** 키를 눌러서 디버거 없이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-158">Press **Ctrl-F5** to run without the debugger.</span></span>

  <span data-ttu-id="38cfe-159">Visual Studio Code가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5001`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-159">Visual Studio Code starts starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5001`.</span></span> <span data-ttu-id="38cfe-160">주소 표시줄에 `localhost:port:5001`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-160">The address bar shows `localhost:port:5001` and not something like `example.com`.</span></span> <span data-ttu-id="38cfe-161">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-161">That's because `localhost` is the standard hostname for  local computer.</span></span> <span data-ttu-id="38cfe-162">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-162">Localhost only serves web requests from the local computer.</span></span>

  <span data-ttu-id="38cfe-163">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-163">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="38cfe-164">대부분의 개발자는 페이지 및 보기 변경 내용을 새로 고치기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-164">Many developers prefer to use non-debug mode to refresh the page and view changes.</span></span>

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="38cfe-165">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="38cfe-165">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="38cfe-166">**파일** > **새 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-166">Select **File** > **New Solution**.</span></span>

  ![macOS 새 솔루션](~/tutorials/first-web-api-mac/_static/sln.png)

* <span data-ttu-id="38cfe-168">**.NET Core 앱** > **ASP.NET Core** > **ASP.NET Core Web App(MVC)** > **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-168">Select **.NET Core App** > **ASP.NET Core** > **ASP.NET Core Web App (MVC)** > **Next**.</span></span>

  ![macOS 새 프로젝트 대화 상자](~/tutorials/first-mvc-app-mac/start-mvc/1.png)

* <span data-ttu-id="38cfe-170">**새 ASP.NET Core Web API 구성** 대화 상자에서 \**.NET Core 2.2*라는 기본 **대상 프레임워크**를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-170">In the **Configure your new ASP.NET Core Web API** dialog, accept the default **Target Framework** of \**.NET Core 2.2*.</span></span>

* <span data-ttu-id="38cfe-171">프로젝트 이름을 **MvcMovie**로 지정하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-171">Name the project **MvcMovie**, and then select **Create**.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="38cfe-172">앱 시작</span><span class="sxs-lookup"><span data-stu-id="38cfe-172">Launch the app</span></span>

<span data-ttu-id="38cfe-173">**실행** > **디버깅하지 않고 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-173">Select **Run** > **Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="38cfe-174">Mac용 Visual Studio에서 [Kestrel](xref:fundamentals/servers/index#kestrel) 서버를 시작하고, 브라우저를 실행하며, `http://localhost:port`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-174">Visual Studio for Mac starts [Kestrel](xref:fundamentals/servers/index#kestrel) server, launches a browser, and navigates to `http://localhost:port`, where *port* is a randomly chosen port number.</span></span>

* <span data-ttu-id="38cfe-175">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-175">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="38cfe-176">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-176">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="38cfe-177">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-177">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="38cfe-178">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-178">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="38cfe-179">**실행** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-179">You can launch the app in debug or non-debug mode from the **Run** menu.</span></span>

---  
<!-- End of VS tabs -->

* <span data-ttu-id="38cfe-180">**승인**을 선택하여 추적에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-180">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="38cfe-181">이 앱은 개인 정보를 추적하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-181">This app doesn't track personal information.</span></span> <span data-ttu-id="38cfe-182">템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-182">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

  ![홈 또는 인덱스 페이지](start-mvc/_static/privacy.png)

  <span data-ttu-id="38cfe-184">다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-184">The following image shows the app after accepting tracking:</span></span>

  ![홈 또는 인덱스 페이지](start-mvc/_static/home2.2.png)

[!INCLUDE[](~/includes/vs-vsc-vsmac-help.md)]

<span data-ttu-id="38cfe-186">이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="38cfe-186">In the next part of this tutorial, you learn about MVC and start writing some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="38cfe-187">다음</span><span class="sxs-lookup"><span data-stu-id="38cfe-187">Next</span></span>](adding-controller.md)  
