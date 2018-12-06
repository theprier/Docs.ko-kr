---
title: ASP.NET Core에서 Razor 페이지 시작
author: rick-anderson
description: 이 자습서 시리즈는 ASP.NET Core에서 Razor Pages를 사용하는 방법을 보여 줍니다. 모델을 만들고, Razor Pages에 대한 코드를 생성하고, Entity Framework Core 및 SQL Server를 데이터 액세스에 사용하고, 검색 기능을 추가하고, 입력 유효성 검사를 추가하고, 마이그레이션을 사용하여 모델을 업데이트하는 방법을 알아봅니다.
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: ca5b134aaa0a9218bc3b0466c3448bd41e8cef8b
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450738"
---
# <a name="tutorial-get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="e10a4-104">자습서: ASP.NET Core에서 Razor Pages 시작</span><span class="sxs-lookup"><span data-stu-id="e10a4-104">Tutorial: Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="e10a4-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e10a4-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e10a4-106">이 자습서의 ASP.NET Core 2.1 버전을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-106">We recommend you follow the ASP.NET Core 2.1 version of this tutorial.</span></span> <span data-ttu-id="e10a4-107">더 많은 기능을 수행하고 다루기가 **훨씬** 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-107">It's **much** easier to follow and covers more features.</span></span> <span data-ttu-id="e10a4-108">버전 선택기에서 **ASP.NET Core 2.1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-108">Select **ASP.NET Core 2.1** in the version selector.</span></span>

![TOC의 버전 선택기](razor-pages-start/_static/v21.png)

::: moniker-end

<span data-ttu-id="e10a4-110">이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-110">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="e10a4-111">Razor 페이지는 ASP.NET Core에서 웹앱 UI를 빌드하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-111">Razor Pages is the recommended way to build UI for web apps in ASP.NET Core.</span></span>

<span data-ttu-id="e10a4-112">이 자습서는 다음 세 가지 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-112">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="e10a4-113">Windows: 이 자습서</span><span class="sxs-lookup"><span data-stu-id="e10a4-113">Windows: This tutorial</span></span>
* <span data-ttu-id="e10a4-114">macOS: [Mac용 Visual Studio로 Razor 페이지 시작](xref:tutorials/razor-pages-mac/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="e10a4-114">macOS: [Get started with Razor Pages with Visual Studio for Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span></span>
* <span data-ttu-id="e10a4-115">macOS, Linux 및 Windows: [Visual Studio Code에서 ASP.NET Core Razor 페이지 시작](xref:tutorials/razor-pages-vsc/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="e10a4-115">macOS, Linux, and Windows: [Get started with ASP.NET Core Razor Pages in Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span></span>

<span data-ttu-id="e10a4-116">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="e10a4-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

> [!NOTE]
> <span data-ttu-id="e10a4-117">ASP.NET Core 목차에 대해 제안된 새 구조의 유용성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-117">We’re testing the usability of a proposed new structure for the ASP.NET Core table of contents.</span></span>  <span data-ttu-id="e10a4-118">몇 분 동안 현재 또는 제안된 목차에서 다른 7개의 항목을 찾는 연습을 수행하는 경우 [여기를 클릭하여 연구에 참여하세요](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span><span class="sxs-lookup"><span data-stu-id="e10a4-118">If you have a few minutes to try an exercise of finding 7 different topics in the current or proposed table of contents, please [click here to participate in the study](https://dpk4xbh5.optimalworkshop.com/treejack/rps16hd5).</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="prerequisites"></a><span data-ttu-id="e10a4-119">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e10a4-119">Prerequisites</span></span>

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="e10a4-120">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e10a4-120">Create a Razor web app</span></span>

* <span data-ttu-id="e10a4-121">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-121">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="e10a4-122">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-122">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="e10a4-123">프로젝트 이름을 **RazorPagesMovie**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-123">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="e10a4-124">코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-124">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
 <span data-ttu-id="e10a4-125">![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2.1.png)</span><span class="sxs-lookup"><span data-stu-id="e10a4-125">![new ASP.NET Core Web Application](razor-pages-start/_static/np_2.1.png)</span></span>
* <span data-ttu-id="e10a4-126">드롭다운에서 **ASP.NET Core 2.1**을 선택한 다음, **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-126">Select **ASP.NET Core 2.1** in the dropdown, and then select **Web Application**.</span></span>

 ![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2_2.1.png)

<span data-ttu-id="e10a4-128">Visual Studio 템플릿은 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-128">The Visual Studio template creates a starter project:</span></span>

![솔루션 탐색기](razor-pages-start/_static/se2.1.png)

<span data-ttu-id="e10a4-130">**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5** 키를 눌러 디버거를 연결하지 않고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-130">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger.</span></span> <span data-ttu-id="e10a4-131">**승인**을 선택하여 추적에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-131">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="e10a4-132">이 앱은 개인 정보를 추적하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-132">This app doesn't track personal information.</span></span> <span data-ttu-id="e10a4-133">템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-133">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/homeGDPR.png)

<span data-ttu-id="e10a4-135">다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-135">The following image shows the app after accepting tracking:</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.1.png)

* <span data-ttu-id="e10a4-137">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-137">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="e10a4-138">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-138">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="e10a4-139">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-139">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="e10a4-140">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-140">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="e10a4-141">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-141">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="e10a4-142">이전 이미지에서 포트 번호는 5001입니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-142">In the preceding image, the port number is 5001.</span></span> <span data-ttu-id="e10a4-143">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-143">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="e10a4-144">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-144">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="e10a4-145">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-145">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/2.1/razor-pages-start.md)]

[!INCLUDE [F7](~/includes/RP/F7.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="prerequisites"></a><span data-ttu-id="e10a4-146">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e10a4-146">Prerequisites</span></span>

[!INCLUDE [Prerequisites](~/includes/net-core-prereqs-windows.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="e10a4-147">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e10a4-147">Create a Razor web app</span></span>

* <span data-ttu-id="e10a4-148">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-148">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="e10a4-149">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-149">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="e10a4-150">프로젝트 이름을 **RazorPagesMovie**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-150">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="e10a4-151">코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-151">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
  <span data-ttu-id="e10a4-152">![새 ASP.NET Core 웹 응용 프로그램](../../razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="e10a4-152">![new ASP.NET Core Web Application](../../razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="e10a4-153">드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-153">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>

  [!INCLUDE [install 2.0](~/includes/dotnetcore-on-dotnetfx-vs.md)]

<span data-ttu-id="e10a4-154">Visual Studio 템플릿은 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-154">The Visual Studio template creates a starter project:</span></span>

![솔루션 탐색기](razor-pages-start/_static/se.png)

<span data-ttu-id="e10a4-156">**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-156">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/home.png)

* <span data-ttu-id="e10a4-158">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-158">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="e10a4-159">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-159">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="e10a4-160">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-160">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="e10a4-161">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-161">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="e10a4-162">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-162">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="e10a4-163">이전 이미지에서 포트 번호는 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-163">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="e10a4-164">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-164">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="e10a4-165">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-165">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="e10a4-166">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10a4-166">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/razor-pages-start.md)]

::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="e10a4-167">다음: 모델 추가</span><span class="sxs-lookup"><span data-stu-id="e10a4-167">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)
