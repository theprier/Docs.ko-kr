---
title: Mac용 Visual Studio를 사용하여 macOS에서 ASP.NET Core의 Razor 페이지 시작
author: rick-anderson
description: Mac용 Visual Studio를 사용하여 ASP.NET Core에서 Razor 페이지를 시작하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: tutorials/razor-pages-mac/razor-pages-start
ms.openlocfilehash: 8a4cc6c52684558ce9176f98205e439096e88cbf
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50089653"
---
# <a name="get-started-with-razor-pages-in-aspnet-core-on-macos-with-visual-studio-for-mac"></a><span data-ttu-id="44f05-103">Mac용 Visual Studio를 사용하여 macOS에서 ASP.NET Core의 Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="44f05-103">Get started with Razor Pages in ASP.NET Core on macOS with Visual Studio for Mac</span></span>

<span data-ttu-id="44f05-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="44f05-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="44f05-105">이 자습서에서는 ASP.NET Core Razor 페이지 웹앱을 빌드하는 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="44f05-106">이 자습서를 시작하기 전에 [Razor 페이지 소개](xref:razor-pages/index)를 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-106">We recommend you review [Introduction to Razor Pages](xref:razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="44f05-107">Razor 페이지는 ASP.NET Core에서 웹 응용 프로그램 UI를 빌드하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44f05-108">전제 조건</span><span class="sxs-lookup"><span data-stu-id="44f05-108">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-macos.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="44f05-109">Razor 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="44f05-109">Create a Razor web app</span></span>

<span data-ttu-id="44f05-110">터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-110">From a terminal, run the following commands:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new webapp -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

::: moniker-end

<span data-ttu-id="44f05-111">이전 명령은 [.NET Core CLI](/dotnet/core/tools/dotnet)를 사용하여 Razor 페이지 프로젝트를 만들고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-111">The preceding commands use the [.NET Core CLI](/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="44f05-112">브라우저를 열고 http://localhost:5000으로 이동하여 응용 프로그램을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-112">Open a browser to http://localhost:5000 to view the application.</span></span>

![홈 또는 인덱스 페이지](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE [razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="44f05-114">프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="44f05-114">Open the project</span></span>

<span data-ttu-id="44f05-115">Ctrl+C를 눌러 응용 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-115">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="44f05-116">Visual Studio에서 **파일 > 열기**를 선택하고 *RazorPagesMovie.csproj* 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-116">From Visual Studio, select **File > Open**, and then select the *RazorPagesMovie.csproj* file.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="44f05-117">앱 시작</span><span class="sxs-lookup"><span data-stu-id="44f05-117">Launch the app</span></span>

<span data-ttu-id="44f05-118">Visual Studio에서 **실행 > 디버깅하지 않고 시작**을 선택하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-118">In Visual Studio, select **Run > Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="44f05-119">Visual Studio가 [Kestrel](xref:fundamentals/servers/kestrel)을 시작하고, 브라우저를 시작하고, `http://localhost:5000`으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-119">Visual Studio starts [Kestrel](xref:fundamentals/servers/kestrel), launches a browser, and navigates to `http://localhost:5000`.</span></span>

<span data-ttu-id="44f05-120">다음 자습서에서는 프로젝트에 모델을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44f05-120">In the next tutorial, we add a model to the project.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="44f05-121">다음: 모델 추가</span><span class="sxs-lookup"><span data-stu-id="44f05-121">Next: Adding a model</span></span>](xref:tutorials/razor-pages-mac/model)
