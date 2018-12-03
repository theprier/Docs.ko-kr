---
title: ASP.NET Core MVC 및 Visual Studio 시작
author: rick-anderson
description: ASP.NET Core MVC 및 Visual Studio를 시작하는 방법을 배웁니다.
ms.author: riande
ms.date: 10/07/2017
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: 9d50607899058c887597a3d73198552d3ef5b020
ms.sourcegitcommit: c4572be5ebb301013a5698caf9b5572b76cb2e34
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710090"
---
# <a name="get-started-with-aspnet-core-mvc-and-visual-studio"></a><span data-ttu-id="76146-103">ASP.NET Core MVC 및 Visual Studio 시작</span><span class="sxs-lookup"><span data-stu-id="76146-103">Get started with ASP.NET Core MVC and Visual Studio</span></span>

<span data-ttu-id="76146-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="76146-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="76146-105">이 자습서는 세 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-105">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="76146-106">macOS: [Mac용 Visual Studio를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="76146-106">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="76146-107">Windows: [Visual Studio를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="76146-107">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="76146-108">macOS, Linux 및 Windows: [Visual Studio Code를 사용하여 ASP.NET Core MVC 앱 만들기](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="76146-108">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span>

> [!NOTE]
> <span data-ttu-id="76146-109">ASP.NET Core 목차에 대해 제안된 새 구조의 유용성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-109">We’re testing the usability of a proposed new structure for the ASP.NET Core table of contents.</span></span>  <span data-ttu-id="76146-110">몇 분 동안 현재 또는 제안된 목차에서 다른 7개의 항목을 찾는 연습을 수행하는 경우 [여기를 클릭하여 연구에 참여하세요](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span><span class="sxs-lookup"><span data-stu-id="76146-110">If you have a few minutes to try an exercise of finding 7 different topics in the current or proposed table of contents, please [click here to participate in the study](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span></span>

## <a name="install-visual-studio-and-net-core"></a><span data-ttu-id="76146-111">Visual Studio 및 .NET Core 설치</span><span class="sxs-lookup"><span data-stu-id="76146-111">Install Visual Studio and .NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="76146-112">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="76146-112">Create a web app</span></span>

<span data-ttu-id="76146-113">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-113">From Visual Studio, select  **File > New > Project**.</span></span>

![파일 > 새로 만들기 > 프로젝트](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="76146-115">**새 프로젝트** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-115">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="76146-116">왼쪽 창에서 **.NET Core**를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-116">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="76146-117">가운데 창에서 **ASP.NET Core 웹 응용 프로그램(.NET Core)** 을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-117">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="76146-118">프로젝트 이름을 “MvcMovie”로 지정합니다(코드를 복사할 때 네임스페이스가 일치하도록 프로젝트 이름을 “MvcMovie”로 지정해야 함).</span><span class="sxs-lookup"><span data-stu-id="76146-118">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="76146-119">**확인**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-119">Tap **OK**</span></span>

![<span data-ttu-id="76146-120">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="76146-120">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2-21.png)

<span data-ttu-id="76146-121">**새 ASP.NET Core 웹 응용 프로그램(.NET Core) - MvcMovie** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-121">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="76146-122">버전 선택기 드롭다운 상자에서 **ASP.NET Core 2.1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-122">In the version selector drop-down box select **ASP.NET Core 2.1**</span></span>
* <span data-ttu-id="76146-123">**웹 응용 프로그램(모델-뷰-컨트롤러)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-123">Select **Web Application (Model-View-Controller)**</span></span>
* <span data-ttu-id="76146-124">**확인**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-124">Tap **OK**.</span></span>

![<span data-ttu-id="76146-125">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="76146-125">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22-21.png)

<span data-ttu-id="76146-126">Visual Studio에서는 방금 만든 MVC 프로젝트에 대한 기본 템플릿을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-126">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="76146-127">프로젝트 이름을 입력하고 몇 가지 옵션을 선택하면 바로 앱이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-127">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="76146-128">다음은 기본 시작 프로젝트이며 여기서 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-128">This is a basic starter project, and it's a good place to start.</span></span>

<span data-ttu-id="76146-129">**F5** 키를 탭하여 앱을 디버그 모드에서 실행하거나 **Ctrl-F5**를 탭하여 디버그 이외 모드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-129">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<span data-ttu-id="76146-130"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![앱 실행](start-mvc/_static/1.png)</span><span class="sxs-lookup"><span data-stu-id="76146-130"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![running app](start-mvc/_static/1.png)</span></span>

* <span data-ttu-id="76146-131">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-131">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="76146-132">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-132">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="76146-133">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="76146-133">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="76146-134">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76146-134">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="76146-135">위 이미지에서 포트 번호는 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="76146-135">In the image above, the port number is 5000.</span></span> <span data-ttu-id="76146-136">브라우저의 URL에는 `localhost:5000`이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="76146-136">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="76146-137">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="76146-137">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="76146-138">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-138">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="76146-139">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-139">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="76146-140">**디버그** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-140">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![디버그 메뉴](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="76146-142">**IIS Express** 단추를 탭하여 앱을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-142">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="76146-144">기본 템플릿은 작동하는 **홈, 정보** 및 **연락처** 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-144">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="76146-145">위의 브라우저 이미지에는 이러한 링크가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-145">The browser image above doesn't show these links.</span></span> <span data-ttu-id="76146-146">브라우저 크기에 따라 탐색 아이콘을 클릭하여 링크를 표시해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-146">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![오른쪽 위의 탐색 아이콘](start-mvc/_static/2.png)

<span data-ttu-id="76146-148">디버그 모드에서 실행 중인 경우 **Shift-F5**를 탭하여 디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-148">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="76146-149">이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-149">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="76146-150">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="76146-150">Create a web app</span></span>

<span data-ttu-id="76146-151">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-151">From Visual Studio, select  **File > New > Project**.</span></span>

![파일 > 새로 만들기 > 프로젝트](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="76146-153">**새 프로젝트** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-153">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="76146-154">왼쪽 창에서 **.NET Core**를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-154">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="76146-155">가운데 창에서 **ASP.NET Core 웹 응용 프로그램(.NET Core)** 을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-155">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="76146-156">프로젝트 이름을 “MvcMovie”로 지정합니다(코드를 복사할 때 네임스페이스가 일치하도록 프로젝트 이름을 “MvcMovie”로 지정해야 함).</span><span class="sxs-lookup"><span data-stu-id="76146-156">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="76146-157">**확인**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-157">Tap **OK**</span></span>

![<span data-ttu-id="76146-158">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="76146-158">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2.png)

<span data-ttu-id="76146-159">**새 ASP.NET Core 웹 응용 프로그램(.NET Core) - MvcMovie** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-159">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="76146-160">버전 선택기 드롭다운 상자에서 **ASP.NET Core 2.-** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-160">In the version selector drop-down box select **ASP.NET Core 2.-**</span></span>
* <span data-ttu-id="76146-161">**웹 응용 프로그램(모델-보기-컨트롤러)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-161">Select **Web Application(Model-View-Controller)**</span></span>
* <span data-ttu-id="76146-162">**확인**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-162">Tap **OK**.</span></span>

![<span data-ttu-id="76146-163">새 프로젝트 대화 상자, 왼쪽 창의 .Net core, ASP.NET Core 웹</span><span class="sxs-lookup"><span data-stu-id="76146-163">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22.png)

<span data-ttu-id="76146-164">Visual Studio에서는 방금 만든 MVC 프로젝트에 대한 기본 템플릿을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-164">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="76146-165">프로젝트 이름을 입력하고 몇 가지 옵션을 선택하면 바로 앱이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-165">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="76146-166">다음은 기본 시작 프로젝트이며 여기서 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-166">This is a basic starter project, and it's a good place to start,</span></span>

<span data-ttu-id="76146-167">**F5** 키를 탭하여 앱을 디버그 모드에서 실행하거나 **Ctrl-F5**를 탭하여 디버그 이외 모드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-167">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<span data-ttu-id="76146-168"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![앱 실행](start-mvc/_static/1.png)</span><span class="sxs-lookup"><span data-stu-id="76146-168"><!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![running app](start-mvc/_static/1.png)</span></span>

* <span data-ttu-id="76146-169">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-169">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="76146-170">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-170">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="76146-171">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="76146-171">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="76146-172">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76146-172">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="76146-173">위 이미지에서 포트 번호는 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="76146-173">In the image above, the port number is 5000.</span></span> <span data-ttu-id="76146-174">브라우저의 URL에는 `localhost:5000`이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="76146-174">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="76146-175">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="76146-175">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="76146-176">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-176">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="76146-177">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-177">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="76146-178">**디버그** 메뉴 항목에서 앱을 디버그 또는 디버그 이외 모드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-178">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![디버그 메뉴](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="76146-180">**IIS Express** 단추를 탭하여 앱을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-180">You can debug the app by tapping the **IIS Express** button</span></span>

![IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="76146-182">기본 템플릿은 작동하는 **홈, 정보** 및 **연락처** 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-182">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="76146-183">위의 브라우저 이미지에는 이러한 링크가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-183">The browser image above doesn't show these links.</span></span> <span data-ttu-id="76146-184">브라우저 크기에 따라 탐색 아이콘을 클릭하여 링크를 표시해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76146-184">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![오른쪽 위의 탐색 아이콘](start-mvc/_static/2.png)

<span data-ttu-id="76146-186">디버그 모드에서 실행 중인 경우 **Shift-F5**를 탭하여 디버깅을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-186">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="76146-187">이 자습서의 다음 부분에서는 MVC에 대해 알아보고 일부 코드 작성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="76146-187">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="76146-188">다음</span><span class="sxs-lookup"><span data-stu-id="76146-188">Next</span></span>](adding-controller.md)  
