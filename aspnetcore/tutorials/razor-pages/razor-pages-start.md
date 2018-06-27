---
title: ASP.NET Core에서 Razor 페이지 시작
author: rick-anderson
description: ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 알아봅니다. Razor 페이지는 ASP.NET Core의 웹 워크로드에 권장됩니다.
manager: wpickett
ms.author: riande
ms.date: 5/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: d7cdf7c8fac3b2ac1e526c6eeee8205068964ec9
ms.sourcegitcommit: 545ff5a632e2281035c1becec1f99137298e4f5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34582819"
---
# <a name="get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="ee091-104">ASP.NET Core에서 Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="ee091-104">Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="ee091-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ee091-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="ee091-106">이 자습서의 ASP.NET Core 2.1 버전을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-106">We recommend you follow the ASP.NET Core 2.1 version of this tutorial.</span></span> <span data-ttu-id="ee091-107">더 많은 기능을 수행하고 다루기가 **훨씬** 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-107">It's **much** easier to follow and covers more features.</span></span> <span data-ttu-id="ee091-108">버전 선택기에서 **ASP.NET Core 2.1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-108">Select **ASP.NET Core 2.1** in the version selector.</span></span>

![TOC의 버전 선택기](razor-pages-start/_static/v21.png)

::: moniker-end

<span data-ttu-id="ee091-110">이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-110">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="ee091-111">Razor 페이지는 ASP.NET Core에서 웹앱 UI를 빌드하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-111">Razor Pages is the recommended way to build UI for web apps in ASP.NET Core.</span></span>

<span data-ttu-id="ee091-112">이 자습서는 다음 세 가지 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-112">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="ee091-113">Windows: 이 자습서</span><span class="sxs-lookup"><span data-stu-id="ee091-113">Windows: This tutorial</span></span>
* <span data-ttu-id="ee091-114">MacOS: [Mac용 Visual Studio로 Razor 페이지 시작](xref:tutorials/razor-pages-mac/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="ee091-114">MacOS: [Get started with Razor Pages with Visual Studio for Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span></span>
* <span data-ttu-id="ee091-115">macOS, Linux 및 Windows: [Visual Studio Code에서 ASP.NET Core Razor 페이지 시작](xref:tutorials/razor-pages-vsc/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="ee091-115">macOS, Linux, and Windows: [Get started with ASP.NET Core Razor Pages in Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span></span>

<span data-ttu-id="ee091-116">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="ee091-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="prerequisites"></a><span data-ttu-id="ee091-117">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ee091-117">Prerequisites</span></span>

<span data-ttu-id="ee091-118">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span><span class="sxs-lookup"><span data-stu-id="ee091-118">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span></span>

## <a name="create-a-razor-web-app"></a><span data-ttu-id="ee091-119">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ee091-119">Create a Razor web app</span></span>

* <span data-ttu-id="ee091-120">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-120">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="ee091-121">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-121">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="ee091-122">프로젝트 이름을 **RazorPagesMovie**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-122">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="ee091-123">코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-123">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
 <span data-ttu-id="ee091-124">![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2.1.png)</span><span class="sxs-lookup"><span data-stu-id="ee091-124">![new ASP.NET Core Web Application](razor-pages-start/_static/np_2.1.png)</span></span>
* <span data-ttu-id="ee091-125">드롭다운에서 **ASP.NET Core 2.1**을 선택한 다음, **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-125">Select **ASP.NET Core 2.1** in the dropdown, and then select **Web Application**.</span></span>

 ![새 ASP.NET Core 웹 응용 프로그램](razor-pages-start/_static/np_2_2.1.png)

<span data-ttu-id="ee091-127">Visual Studio 템플릿은 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-127">The Visual Studio template creates a starter project:</span></span>

![솔루션 탐색기](razor-pages-start/_static/se2.1.png)

<span data-ttu-id="ee091-129">**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5** 키를 눌러 디버거를 연결하지 않고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-129">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger.</span></span> <span data-ttu-id="ee091-130">**승인**을 선택하여 추적에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-130">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="ee091-131">이 앱은 개인 정보를 추적하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-131">This app doesn't track personal information.</span></span> <span data-ttu-id="ee091-132">템플릿 생성 코드는 [GDPR(일반 데이터 보호 규정)](xref:security/gdpr)을 충족할 수 있도록 자산을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-132">The template generated code includes assets to help meet [General Data Protection Regulation (GDPR)](xref:security/gdpr).</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/homeGDPR.png)

<span data-ttu-id="ee091-134">다음 이미지에서는 추적을 승인한 후에 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-134">The following image shows the app after accepting tracking:</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/home2.1.png)

* <span data-ttu-id="ee091-136">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-136">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs the app.</span></span> <span data-ttu-id="ee091-137">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-137">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="ee091-138">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-138">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="ee091-139">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-139">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="ee091-140">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-140">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="ee091-141">이전 이미지에서 포트 번호는 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-141">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="ee091-142">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-142">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="ee091-143">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-143">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="ee091-144">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-144">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/2.1/razor-pages-start.md)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

## <a name="prerequisites"></a><span data-ttu-id="ee091-145">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ee091-145">Prerequisites</span></span>

<span data-ttu-id="ee091-146">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span><span class="sxs-lookup"><span data-stu-id="ee091-146">[!INCLUDE [](~/includes/net-core-prereqs-windows.md) [](~/includes/net-core-prereqs-windows.md)]</span></span>

## <a name="create-a-razor-web-app"></a><span data-ttu-id="ee091-147">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ee091-147">Create a Razor web app</span></span>

* <span data-ttu-id="ee091-148">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-148">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="ee091-149">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-149">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="ee091-150">프로젝트 이름을 **RazorPagesMovie**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-150">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="ee091-151">코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-151">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
  <span data-ttu-id="ee091-152">![새 ASP.NET Core 웹 응용 프로그램](../../mvc/razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="ee091-152">![new ASP.NET Core Web Application](../../mvc/razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="ee091-153">드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-153">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>

  [!INCLUDE [install 2.0](~/includes/dotnetcore-on-dotnetfx-vs.md)]

<span data-ttu-id="ee091-154">Visual Studio 템플릿은 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-154">The Visual Studio template creates a starter project:</span></span>

![솔루션 탐색기](razor-pages-start/_static/se.png)

<span data-ttu-id="ee091-156">**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-156">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/home.png)

* <span data-ttu-id="ee091-158">Visual Studio가 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-158">Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="ee091-159">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-159">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="ee091-160">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-160">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="ee091-161">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-161">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="ee091-162">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-162">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="ee091-163">이전 이미지에서 포트 번호는 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-163">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="ee091-164">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-164">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="ee091-165">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-165">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="ee091-166">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee091-166">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE [razor-pages-start](~/includes/RP/2.1/razor-pages-start.md)]

::: moniker-end

> [!div class="step-by-step"]
> [<span data-ttu-id="ee091-167">다음: 모델 추가</span><span class="sxs-lookup"><span data-stu-id="ee091-167">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)
