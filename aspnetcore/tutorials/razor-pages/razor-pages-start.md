---
title: "ASP.NET Core에서 Razor 페이지 시작"
author: rick-anderson
description: "ASP.NET Core에서 Razor 페이지 시작"
ms.author: riande
manager: wpickett
ms.date: 12/22/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 69a5bc439130ffacf2d267c79b1a6b0347171e49
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="1e650-103">ASP.NET Core에서 Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="1e650-103">Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="1e650-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1e650-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1e650-105">이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="1e650-106">Razor 페이지는 ASP.NET Core에서 웹앱 UI를 빌드하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-106">Razor Pages is the recommended way to build UI for web apps in ASP.NET Core.</span></span>

<span data-ttu-id="1e650-107">이 자습서는 다음 세 가지 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-107">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="1e650-108">Windows: 이 자습서</span><span class="sxs-lookup"><span data-stu-id="1e650-108">Windows: This tutorial</span></span>
* <span data-ttu-id="1e650-109">MacOS: [Mac용 Visual Studio에서 Razor 페이지 시작](xref:tutorials/razor-pages-mac/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="1e650-109">MacOS: [Getting started with Razor Pages with Visual Studio for Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span></span>
* <span data-ttu-id="1e650-110">macOS, Linux 및 Windows: [Visual Studio Code를 사용하여 ASP.NET Core에서 Razor 페이지 시작](xref:tutorials/razor-pages-vsc/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="1e650-110">macOS, Linux, and Windows: [Getting started with Razor Pages in ASP.NET Core with Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span></span>

<span data-ttu-id="1e650-111">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="1e650-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e650-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1e650-112">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="1e650-113">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="1e650-113">Create a Razor web app</span></span>

* <span data-ttu-id="1e650-114">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-114">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="1e650-115">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-115">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="1e650-116">프로젝트 이름을 **RazorPagesMovie**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-116">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="1e650-117">코드를 복사 후 붙여넣을 때 네임스페이스가 일치하도록 프로젝트 이름을 *RazorPagesMovie*로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-117">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
  <span data-ttu-id="1e650-118">![새 ASP.NET Core 웹 응용 프로그램](../../mvc/razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="1e650-118">![new ASP.NET Core Web Application](../../mvc/razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="1e650-119">드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-119">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>

  [!INCLUDE[install 2.0](../../includes/dotnetcore-on-dotnetfx-vs.md)]

<span data-ttu-id="1e650-120">Visual Studio 템플릿은 시작 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-120">The Visual Studio template creates a starter project:</span></span>

![솔루션 탐색기](razor-pages-start/_static/se.png)

<span data-ttu-id="1e650-122">**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-122">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![홈 또는 인덱스 페이지](razor-pages-start/_static/home.png)

* <span data-ttu-id="1e650-124">Visual Studio가 [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview)를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-124">Visual Studio starts [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="1e650-125">주소 표시줄에 `localhost:port#`이 표시되고 `example.com` 등은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-125">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="1e650-126">그 이유는 `localhost`가 로컬 컴퓨터의 표준 이름이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-126">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="1e650-127">Localhost는 로컬 컴퓨터의 웹 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-127">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="1e650-128">Visual Studio에서 웹 프로젝트를 만들 경우 웹 서버에는 임의 포트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-128">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="1e650-129">이전 이미지에서 포트 번호는 5000입니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-129">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="1e650-130">앱을 실행할 경우 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-130">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="1e650-131">**Ctrl+F5**(디버그 이외 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-131">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="1e650-132">대부분의 개발자는 앱을 빠르게 시작하고 변경 내용을 확인하기 위해 디버그 이외 모드를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e650-132">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

>[!div class="step-by-step"]
[<span data-ttu-id="1e650-133">다음: 모델 추가</span><span class="sxs-lookup"><span data-stu-id="1e650-133">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)

>[!div class="step-by-step"]
[<span data-ttu-id="1e650-134">다음: 모델 추가</span><span class="sxs-lookup"><span data-stu-id="1e650-134">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)
